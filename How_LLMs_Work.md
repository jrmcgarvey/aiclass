# How Large Language Models Work

*An exposition of the technical ideas underlying modern AI language systems*

---

## Contents

1. Tokens — What the Model Reads
2. Embeddings — Giving Words a Location in Meaning-Space
3. Positional Encoding — Word Order Matters
4. Attention — Words Noticing Each Other
5. Neurons, Layers, and the Feed-Forward Network
6. Training — Finding the Valley Floor
7. Fine-Tuning — From Text Predictor to Helpful Assistant
8. Inference — Generating a Response
9. Capabilities, Limitations, and Where This Is Heading

---

## 1. Tokens — What the Model Reads

When a large language model reads text, it does not read words the way you do, and it does not read letter by letter either. Instead it breaks text into chunks called **tokens**.

Why not whole words? English alone contains hundreds of thousands of words — and that is before adding slang, technical terms, foreign words, misspellings, and new coinages. A dictionary large enough to cover everything would be unmanageably large, and the model would struggle with any word it had not seen before.

Why not single letters? Letters carry almost no meaning on their own. The letter "b" tells you almost nothing. Processing text one letter at a time would be like trying to understand a novel one brushstroke at a time.

Tokens are a middle ground. A typical model uses a vocabulary of roughly 50,000 to 100,000 tokens — a manageable number that can represent virtually any text. Common words like "the" or "cat" become a single token. Less common words get broken into meaningful pieces: "unbelievable" might become "un," "believ," and "able." Punctuation and spaces are tokens too.

Notice that some tokens are whole words, some are word-fragments that carry meaning (prefixes like "un-" or "pre-," suffixes like "-ing"), and some are punctuation or numbers. The model has never seen the word "unbelievable" — but because it knows "un-," "believ," and "-able" from thousands of other words, it can handle it anyway. This is one of the key efficiencies of the token approach: a model that knows sub-word fragments can generalise to words it has never seen before.

This also explains a curious limitation: if you ask a model to count the letters in *strawberry*, it may get it wrong. The model never sees individual letters — it sees tokens like "straw" and "berry," and has to reason about the letters inside them indirectly. It often fails at exactly these simple character-level tasks, while succeeding at far more complex semantic ones.

The tokenisation process itself is not arbitrary. Before a model is trained, a separate **tokeniser training phase** runs on a large corpus of text to determine the optimal vocabulary using an algorithm called Byte Pair Encoding (BPE). The process begins with individual characters, then iteratively merges the most frequent adjacent pairs — "t" and "h" merge to "th," then "th" and "e" to "the," and so on — until a target vocabulary size is reached, typically between 32,000 and 128,000 tokens. This produces a vocabulary that represents common words as single tokens and rare words as sequences of meaningful fragments.

Once tokenised, each token is assigned a unique identification number. From this point on, the model works entirely with numbers, not text.

---

## 2. Embeddings — Giving Words a Location in Meaning-Space

Once text has been broken into tokens and each token given an ID number, the model needs to do something more powerful than just number them. It needs to represent **meaning**. The tool it uses for this is called an **embedding**.

Each token is placed at a location in a mathematical space — think of it as a map. On this map, tokens with similar meanings end up near each other. "Cat" and "kitten" are neighbours. "Cat" and "automobile" are far apart. "King" and "queen" are close together, and their relationship to each other mirrors the relationship between "man" and "woman." The geometry of the map encodes meaning in a structural way: relationships between words are preserved as spatial relationships between points.

A real map has only two dimensions — north-south and east-west. The embedding space in a large language model has thousands of dimensions. This is impossible to visualise, but the principle is the same: each additional dimension is another axis along which tokens can be similar or different, capturing grammar, formality, emotional tone, subject matter, and countless other properties we do not even have names for. Each token is represented by its location in this space as a list of numbers — one number per dimension. For a large model this might be a list of 4,096 numbers. This list is called the token's **embedding vector**.

### Random initialisation

At the beginning of training, every token is placed at a random location, with the coordinates drawn from a statistical distribution — a bell curve centred on zero, of the kind that will be familiar to anyone who has encountered the Gaussian or normal distribution. At this point the map is meaningless. "Cat" and "nuclear reactor" are equally likely to be neighbours — pure chance. The model has no idea yet that they are unrelated.

This is why training on enormous amounts of text is necessary: the model needs to encounter "cat" and "kitten" together in millions of contexts before it learns to move them close to each other on the map. Training gradually shifts every token's location — through billions of tiny adjustments — until the geometry of the space reflects the structure of human language. By the end of training, the embedding map is a rich, structured representation of meaning, built entirely from patterns in text.

The embedding vectors are not fixed at initialisation; they are among the parameters that are updated during training. Along with all the other weights in the model, they start random and become meaningful through the learning process.

---

## 3. Positional Encoding — Word Order Matters

We now have an embedding vector for each token that encodes its meaning. But there is a problem. The model processes all the tokens in a sentence simultaneously, not one at a time the way you read. This means it has no built-in sense of order. Left to itself, it would treat "the dog chased the boy" and "the boy chased the dog" as identical — the same tokens, just shuffled. Word order is obviously critical to meaning.

The solution is straightforward in concept: before processing begins, each token gets a second piece of information attached to it — its **position** in the sentence. Token 1 gets a "position 1" tag, token 2 gets a "position 2" tag, and so on. This positional information is represented as another vector — another list of numbers — and it is simply added to the embedding vector. The result is a single combined vector that captures both *what* the token means and *where* it appears.

A few things are worth noting. The position vectors are completely independent of the tokens themselves. Position 3's vector is always the same, whether the word sitting in slot 3 is "cat" or "democracy." It is the slot that gets tagged, not the word. Like the embedding vectors, position vectors start as random numbers at the beginning of training and are gradually adjusted as the model learns — the model figures out for itself what positional information is useful.

The practical consequence is vivid: even if the word "the" appears twice in a sentence, each instance gets a different combined vector because each sits in a different position slot. The model can tell them apart. Without positional encoding, "the dog chased the boy" and "the boy chased the dog" would look identical. With it, they are clearly distinct.

More recent models, including most frontier systems in 2025, use a more sophisticated approach called **Rotary Positional Embeddings (RoPE)**. Instead of adding a position vector, RoPE applies a mathematical rotation to the token's meaning vector based on its position. This makes it easier for the model to understand the *relative* distance between words — which is more important for grammar and meaning than absolute position — and scales better to very long sequences.

---

## 4. Attention — Words Noticing Each Other

We now have a vector for each token that encodes both its meaning and its position. The next step is the heart of the modern language model: a mechanism called **attention**. This is where the model figures out how the tokens in a sentence relate to each other.

### How attention works

Every token gets to look at every other token in the sentence and ask: *how relevant are you to me?* The answers are collected and used to build a richer, context-aware representation of each token.

Consider the sentence: *"The bank of the river was steep."* The word "bank" is ambiguous — it could mean a financial institution or the edge of a river. Attention resolves this. The token "bank" looks across the sentence and finds "river" highly relevant. That relevance shifts the effective meaning of "bank" away from finance and toward geography. By the time the model is done processing this sentence, the vector representing "bank" has been updated to reflect its meaning in this specific context — not just its general dictionary meaning.

This is what makes the Transformer architecture so powerful compared to earlier approaches. Earlier models read text sequentially, like a person reading, and had difficulty connecting a word to another word far away in a long sentence. Attention operates on the whole sentence at once, and distance is no obstacle.

### Multiple attention heads

In practice, this attention process is run not once but many times in parallel — each run with slightly different settings, looking for different kinds of relationships. One pass might focus on grammatical relationships: which word is the subject, which is the object, how do verb tenses relate? Another might focus on semantic relationships: which words share a topic or domain? Another might track references: when the text says "it," what does it refer to? These parallel passes are called **attention heads**, and their results are combined before moving on.

The different heads do not converge to the same solution because they are initialised with different random values and trained to look for different patterns. Research has confirmed that in trained models, different attention heads tend to specialise in different types of linguistic relationships — though this specialisation emerges from training, not from explicit programming.

The output of attention is a new, enriched vector for each token — one that reflects not just what that token means in isolation, but what it means given everything around it. You can think of it as the difference between looking up a word in a dictionary and understanding it in a sentence.

---

## 5. Neurons, Layers, and the Feed-Forward Network

It is worth pausing here to connect the Transformer architecture to the broader concept of a neural network.

### What is a neuron?

A **neuron** in a neural network is a very simple computing unit. It receives a set of numbers as input, multiplies each one by a **weight** — its own personal measure of how important that input is — adds the results together, and then passes the sum through an **activation function**. The activation function introduces a small but crucial non-linearity: rather than passing the number straight through, it squashes or bends it in some way. This seemingly minor step is what allows a network of neurons to learn complex, subtle patterns rather than just simple straight-line relationships.

Neurons are connected in **layers**. The output of one layer becomes the input of the next. In the Transformer architecture, there are typically many such layers — perhaps 96 in a large model — stacked on top of each other. Each layer processes the token vectors it receives and passes enriched versions forward to the next layer.

The connections between neurons are the weights — and these weights are precisely the parameters adjusted during training. A large language model may have billions of such weights. Learning, in a neural network, means finding the right values for all of them.

### Inside each Transformer layer

Within each layer of a Transformer, there are two main components working in sequence. First, the attention mechanism — where tokens look at each other and update their vectors. Second, a **feed-forward network** — a small, conventional neural network that processes each token's updated vector independently, adding another round of refinement.

If attention is the step where tokens gather context from their neighbours, the feed-forward network is the step where each token privately digests that context and updates its own representation. Unlike attention, which mixes information across the sequence, the feed-forward network operates on each token independently. Recent interpretability research suggests these feed-forward layers function as a kind of key-value memory: the first layer recognises patterns or concepts, and the second layer provides the associated knowledge or semantic update. In most large language models, the feed-forward layers account for roughly two-thirds of the total parameter count — they are where most of the model's factual knowledge is stored.

Between the attention and feed-forward steps, a process called **layer normalisation** stabilises the numbers, preventing them from growing too large or collapsing too small as they pass through many layers.

By the time the token vectors have passed through all the layers, they carry a remarkably rich representation of meaning — shaped by context, position, grammatical role, and the accumulated patterns of everything the model has been trained on.

---

## 6. Training — Finding the Valley Floor

We have now described the architecture of a large language model — tokens, embeddings, position encoding, attention, and layers of neurons. The crucial question remains: how does the model learn? How do all those billions of random starting weights get adjusted into something that can understand and generate language?

### The starting point

Every parameter in the model starts as a random number. The embedding vectors, the attention weights, the weights of every neuron in every layer — all random. At this point the model is useless.

### The training loop

Training proceeds by feeding the model enormous quantities of text — drawn from books, websites, code repositories, and other written material — and asking it to do one thing repeatedly: **predict the next token**.

The process works like this. The model is shown a sequence of tokens and, using all its current weights, runs the full machinery — embeddings, position encoding, attention, feed-forward networks — and produces a **probability distribution** across its entire vocabulary. It is essentially placing a bet: "I think the next token is most likely X, somewhat likely Y, unlikely Z," and so on for every token in the vocabulary.

That prediction is then compared to the *actual* next token as it appears in the original text. This comparison is captured by a **loss function** — a single number representing how wrong the model was. A confident correct prediction produces a low loss. A confident wrong prediction produces a high loss. The loss function is smooth and continuous — which is mathematically crucial, because it means the loss has a slope that can be followed downhill.

### Gradient descent: the topographic map analogy

Imagine a plastic relief map of a mountain range — the kind where you can feel the peaks and valleys with your hand. Every point has a height. Your goal is to find the lowest point in the landscape — the bottom of the deepest valley. You are blindfolded. You can only feel the slope immediately beneath your feet. A reasonable strategy is to feel which direction is most steeply downhill, take a careful step in that direction, stop and feel again. Repeat.

This is **gradient descent**. The height at any point on the map represents the error of the model — how wrong its predictions are. The goal of training is to find the combination of weights that minimises this error. The slope at any point is the **gradient** — a measure of how steeply the error is changing. The model follows the gradient downhill, adjusting its weights in small steps.

A real topographic map has two dimensions. The landscape of a large language model has **billions** of dimensions — one for each weight in the model. This is impossible to visualise, but the principle is exactly the same. At each step of training, the model calculates the gradient across all those dimensions simultaneously and takes a small step in the direction that most reduces error.

The step size is kept deliberately small, controlled by a parameter called the **learning rate**. Large steps risk overshooting a good valley and ending up somewhere worse. The model rarely finds the single lowest point in the entire landscape — it finds *a* valley that is good enough. Remarkably, researchers have found that many different valleys produce models of similar quality, which is why different training runs starting from different random initialisations produce models that perform comparably despite having quite different weights.

To calculate the gradient across billions of parameters, the model uses a technique called **backpropagation** — sending the error signal backward through all the layers using the chain rule of calculus to determine how much each weight contributed to the error. This calculation — performed billions of times across a vast training dataset — is what makes training so computationally demanding, requiring specialised hardware running for weeks or months.

### Unsupervised learning at massive scale

Crucially, this learning is **unsupervised**. The correct answer for every prediction is simply the next token as it actually appears in the original text. No human beings are labelling data or writing correct answers. This means the model can be trained on essentially anything written — the contents of the internet, digitised books, scientific papers — without any human preparation beyond basic cleaning. This is what makes pre-training feasible at the scale required to produce capable models.

After enough iterations across enough text, something remarkable happens. The random landscape of weights has been sculpted — through billions of tiny adjustments — into a model that has internalised the patterns, facts, grammar, reasoning styles, and accumulated knowledge present in human writing. It is not yet a helpful assistant. But it is a remarkably powerful predictor of human language.

---

## 7. Fine-Tuning — From Text Predictor to Helpful Assistant

After pre-training, the model is extraordinary in a narrow sense. But it is not a helpful assistant. If you type "What is the capital of France?" it might respond by generating more questions in the same style — because that is what follows questions in the text it was trained on. It completes patterns. It does not answer. Pre-training produces a brilliant mimic. Fine-tuning turns the mimic into a colleague.

### Why fine-tuning requires specifically created data

Pre-training was unsupervised — the correct answer was always just the next token in existing text. Fine-tuning is different. We are trying to teach the model to respond well to prompts, and "responding well" is a human judgement that cannot be extracted automatically from raw text. This is why fine-tuning requires **prompt and response pairs** — examples of a user saying something and an ideal assistant response following it. These pairs must be created deliberately, either by human writers or by using a more capable model to generate candidate responses that human reviewers then evaluate and refine.

Because the training data has to be created rather than harvested from the internet, it is far more expensive to produce. Fortunately, far less of it is needed. Pre-training requires trillions of tokens. Fine-tuning can produce meaningful results with thousands of high-quality examples — because the model is not learning language from scratch, it is learning how to apply what it already knows in a new context.

### Reinforcement Learning from Human Feedback (RLHF)

The most influential fine-tuning approach goes one step further. Rather than simply showing the model correct responses, human raters are asked to compare pairs of model responses and indicate which one is better. These preferences are used to train a separate model — called a **reward model** — that learns to predict which responses humans will prefer. The language model is then trained to maximise this reward.

This approach allows the model to be steered toward subtler qualities that are hard to capture in a simple right-or-wrong training example: qualities like being appropriately concise, acknowledging uncertainty, maintaining a consistent persona, or declining to assist with harmful requests. RLHF is the technique behind much of what makes modern AI assistants feel helpful rather than merely knowledgeable.

### The risk of synthetic data loops

Fine-tuning increasingly relies on synthetic data — responses generated by a stronger model, used to train a weaker one. This raises a real concern: if a model is trained iteratively on its own unverified outputs, errors, biases, and a lack of diversity can echo and amplify — a phenomenon researchers call **model collapse**. In practice, several strategies are used to prevent this: teacher-student verification (a stronger model filters out low-quality outputs before they enter training), mixing real human-generated data with synthetic data to prevent drift, and using multiple models to generate data for each other to introduce diversity. The risk is real, but the safeguards have so far been sufficient to make synthetic data a productive tool.

---

## 8. Inference — Generating a Response

We have now described how the model is built and trained. What actually happens when you type something and press send?

### One token at a time

The model does not compose a response the way a human writer might — thinking ahead, sketching an outline, then filling it in. It generates its response **one token at a time**, from left to right, with no ability to go back and revise.

The process works like this. The model takes your input — your prompt — and runs it through all its layers: embeddings, position encoding, attention, feed-forward networks. At the end of this process it produces a probability distribution across its entire vocabulary. It selects a token, appends it to the growing response, and then runs the whole process again with the slightly longer input. And again. And again, until it produces a token that signals the response is complete.

### Temperature and controlled randomness

The model does not always pick the single most probable next token. If it did, responses would be repetitive and mechanical — the model would always take the most predictable path. Instead, there is a controlled element of randomness. The model **samples** from its probability distribution, meaning that likely tokens are chosen often but not always, and less likely tokens get occasional chances.

The degree of randomness is controlled by a parameter called **temperature**. A low temperature makes the model cautious and predictable — it sticks close to its most probable choices. A high temperature makes it more adventurous — it reaches further down the probability list, producing more surprising and sometimes more creative output, at the cost of occasionally going off track. Temperature is exposed as a user-adjustable setting in many AI interfaces.

### The context window

The model can only consider a limited amount of text at once. Everything it knows about the current conversation — the prompt, its previous responses, any background instructions — must fit within this limit, called the **context window**. Early models had context windows of a few thousand tokens. Current large models can handle hundreds of thousands, with some approaching one million.

Beyond this limit, earlier parts of the conversation fall out of view — the model has no memory of them. This is worth understanding as a user. A model does not have persistent memory the way a human does. Each conversation starts fresh. What feels like memory within a conversation is simply the context window: the model can see everything in the current exchange, but nothing from previous sessions unless it has been explicitly provided.

### Extended reasoning

Modern models are increasingly asked to reason through complex problems before producing a final response. This is visible as the "thinking" pause you may have noticed in systems like OpenAI's o1 or Google's Gemini. This extended reasoning is still, at its core, the same process — one token at a time. But the model is generating intermediate reasoning steps, evaluating them, and sometimes backtracking, before arriving at a final answer.

The extra time represents genuine additional computation — more tokens generated, more passes through the network. The result is generally a more reliable answer for complex problems. In terms of the Tree of Thoughts framework, the model is exploring multiple branches of reasoning simultaneously, evaluating each, and following the most promising path. Modern implementations do this internally through reinforcement learning, rather than as an external prompting strategy — the model has been trained to deliberate, not just instructed to.

---

## 9. Capabilities, Limitations, and Where This Is Heading

### What these models are genuinely good at

The breadth of capability that emerges from the training process is, by any historical measure, remarkable. Models trained in this way can write, summarise, translate, explain, argue, code, and reason across an enormous range of topics. They can shift register from technical to casual, match a requested style, and maintain coherence across long exchanges.

This breadth is not because the models were explicitly taught each of these skills. It emerges from the sheer scale of pre-training. A model that has predicted enough human text has absorbed the patterns underlying all of these activities. Fine-tuning then makes these latent capabilities accessible in a conversational form.

Particularly impressive is what might be called **analogical transfer** — the ability to apply patterns learned in one domain to a novel problem in another. A model trained simultaneously on mathematics, law, medicine, literature, and engineering can draw unexpected connections across these fields in ways that a narrow specialist cannot.

### What these models cannot do reliably

**Hallucination.** Models sometimes state falsehoods with complete confidence. When predicting the next token, the most statistically likely sequence is not always the true one. This is a consequence of the fundamental architecture — not a straightforward bug that will be easily fixed. The model has no separate fact-checking mechanism; it generates what its training predicts should come next, and that is sometimes wrong.

**No genuine reasoning from first principles.** When a model solves a logic puzzle or a mathematics problem, it is drawing on patterns in its training data — it has seen many similar problems and learned what correct solutions look like. For genuinely novel problems with no learned patterns to fall back on, it can fail in unexpected and sometimes embarrassing ways.

**Knowledge cutoff.** The training data was collected up to a certain date. Events after that date are unknown to the model unless provided in the conversation.

**No persistent memory.** Each conversation starts fresh. The model has no recollection of previous sessions unless explicitly shown them.

**Inherited bias.** A model trained on human-generated text absorbs the biases present in that text. Fine-tuning efforts mitigate this but do not eliminate it.

### The rapidly expanding frontier

**Reasoning models.** The most recent generation of models — including systems from OpenAI, Google, and Anthropic — spend additional time generating intermediate reasoning steps before producing a final answer. This "thinking before answering" approach produces meaningfully better results on complex problems in mathematics, coding, and logic. The visible pause in some AI interfaces represents genuine additional computation, not delay.

**Multimodal models.** Current leading models can process not just text but images, audio, and in some cases video. The architecture is recognisable — inputs of different types are converted into token-like representations and processed by the same Transformer machinery. Vision Transformers divide images into "patches" that are treated like text tokens; audio is converted into a spectrogram and processed similarly. The result is a single model that can reason across modalities — understanding that a photograph of a dog and the sound of a bark refer to the same concept.

**Agentic systems.** Models are increasingly being used not just to answer questions but to take sequences of actions toward a goal — browsing the web, writing and executing code, managing files, interacting with external services. The model serves as a reasoning engine, planning a sequence of steps and executing them one at a time. Tool use is implemented entirely through token prediction: the model generates a structured token sequence representing a command, the surrounding software recognises it, executes it, and returns the result as new input to the model.

### A closing observation

The architecture described throughout this document was largely established in a single landmark paper published in 2017, titled "Attention Is All You Need." The core insight — that attention mechanisms operating on token embeddings, trained by predicting the next token at massive scale, could produce systems of extraordinary capability — has proven more powerful than almost anyone anticipated at the time.

Every increase in scale — more parameters, more training data, more compute — has so far continued to produce improvements, sometimes in capabilities that were not anticipated or explicitly trained for. Whether this scaling continues to yield returns, and what those returns might look like, is one of the most consequential open questions in science and technology today.

What we do know is that understanding the basic architecture is essential for thinking clearly about both the promise and the risks of these systems. They are not magic, and they are not human. They are something genuinely new: a technology that has absorbed an extraordinary amount of human knowledge and learned to apply it in ways that are often useful, sometimes surprising, and occasionally wrong.

---

*Document generated from a technical exposition developed across two class sessions on large language models.*
