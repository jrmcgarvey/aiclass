# Neural Networks and Visual Recognition: From Biology to Deep Learning and Large Language Models

## Introduction

Today's lesson -- we might spill over to next week -- will attempt to explain how current AI systems work.  We will start with visual recognition.  Large language models proved to be harder. Note: Most of the techniques described in what follows has been superseded or refined, so you will not see the current state of the art.

Please be warned, this is pretty technical stuff.

One of the most compelling ways to understand modern neural networks is to trace their origins — from early neuroscience experiments on cats, through the first practical applications in reading handwritten digits, to the deep learning revolution that shapes artificial intelligence today. This document follows that arc, using the history of visual recognition as a thread to illuminate the core ideas behind convolutional neural networks and deep learning.

---

# Some Basic Neural Network Concepts

---

## Forward Propagation in a Neural Network

You start with input data, which is represented as a collection of vectors.  A vector is an ordered list of numbers.  For an image, a vector might be the RGB (red-green-blue) value of a given pixel.  For text being processed by an LLM, each vector might be some collection of numbers assigned to a textual element in the input (a word or part of a word).

The first layer then applies a transformation.  One part of the transformation is matrix multiplication. A matrix is a rectangular array of numbers. Information from various subsets of vectors in the input is combined, and multiplied by the matrix.  This combines the information to derive information about the input -- e.g. there is an edge at this point in the image, or this word is the subject in the sentence. Several matrices are used at each stage to do this combination.  Then, an activation function is applied.  The activation function determines if something has been learned, and conveys a level of confidence about the derived information.  A transformed series of vectors are then passed to the next layer, where the process repeats, using a different set of matrices.

Each number in each of the matrices is a "weight", or a parameter of the model.  At the outset, these weights are randomly assigned -- just numbers chosen from a range, according to some distribution function that might assign middle range numbers more often than ones at the edge of the range.  As there can be many layers to the model, and many matrices at each layer, there can be many weights -- hundreds of billions in current LLMs for example.

## The Very End

The collection then is mapped to a collection of "logit".  For image recognition, this is the likelihood that the image is, say, a cat, or a house, or a car.  For text processing in an LLM, this is the likelihood that a given next word or part of a word appears in the output.  The mappings themselves are "learned", that is, there are a collection of weights to give the resulting probability.  Then a softmax function is applied, which converts the logits so that they add up to 100%.  The model then might conclude that the image is a cat, with 93% probability or something like that.

One problem is that the softmax function always makes the logits add to 100%.  This is equivalent to the assertion that whatever image is being observed, it is certain to belong to one of the known object categories.  If you show the AI something it hasn't seen before, it will never return, "Beats the heck out of me."  It will return some probabilities for several categories in the model.

## The Error Function

The end product is some assertion about the input.  For example, is the image a cat, and how certain? For text, is the next word "actually"? During training, the model will return an erroneous value a certain percent of the time.  This is the error function.  For visual recognition, supervised learning is used: a set of images that have been labeled by humans as belonging to a fixed list of categories.  For LLMs, the initial training data is just the text found on the Internet, not labeled in any way, so this is unsupervised training.

## Adjusting the Weights

Initially, the values in the weights are randomly assigned -- random, that is, with in a range and with a particular distribution.  For example, if the Gaussian (bell shaped) distribution were used, most of the weights will be chosen from the middle of the range.  (The Guassian distribution is not used -- there are better choices.) The neural network must "learn" a better set of weights, ones that will reduce the error function.

## Which Weights are to Blame? How Should the Values be Changed?

Imagine a plastic relief map of a mountain range — the kind where you can feel the peaks and valleys with your hand. Every point has a height. Your goal is to find the lowest point in the landscape — the bottom of the deepest valley. You are blindfolded. You can only feel the slope immediately beneath your feet. A reasonable strategy is to feel which direction is most steeply downhill, take a careful step in that direction, stop and feel again. Repeat.

This is **gradient descent**. The height at any point on the map represents the error of the model — how wrong its predictions are. The goal of training is to find the combination of weights that minimises this error. The slope at any point is the **gradient** — a measure of how steeply the error is changing. The model follows the gradient downhill, adjusting its weights in small steps.

A real topographic map has two dimensions. The landscape of a large language model has **billions** of dimensions — one for each weight in the model. This is impossible to visualise, but the principle is exactly the same. At each step of training, the model calculates the gradient across all those dimensions simultaneously and takes a small step in the direction that most reduces error.

The step size is kept deliberately small, controlled by a parameter called the **learning rate**. Large steps risk overshooting a good valley and ending up somewhere worse. The model rarely finds the single lowest point in the entire landscape — it finds *a* valley that is good enough. Remarkably, researchers have found that many different valleys produce models of similar quality, which is why different training runs starting from different random initialisations produce models that perform comparably despite having quite different weights.

To calculate the gradient across billions of parameters, the model uses a technique called **backpropagation** — sending the error signal backward through all the layers using the chain rule of calculus to determine how much each weight contributed to the error. This calculation — performed billions of times across a vast training dataset — is what makes training so computationally demanding, requiring specialised hardware running for weeks or months.

Backpropagation uses the chain rule from calculus.  The process of forward propagation is, basically, the application of a series of functions:

x -> f(x) applies layer 1.

x -> g(f(x)) applies layer 2.

x -> h(g(f(x))) applies layer 3.  The chain rule from calculus prescribes how to combine the derivatives of functions f, g, and h so as to compute the gradient.  You get the derivative of the later levels first, and propagate back.

The gradient then says which weights are to be adjusted.  Then the revised data is run on the training data to compute a new error function, and gradually the weights improve.

## An Aside: Why the Market Valuation of Nvidia is 5.2 Trillion Dollars

Nvidia makes graphics processing units (GPUs).  When people started using personal computers, they wanted to play video games.  Compelling graphics required a lot of computation.  GPUs do this processing in parallel.  A standard CPU can do the same computations, but without much parallelism.  GPUs can't replace CPUs, because they don't do conditional branching well.  (Conditional branching says, if the result of the previous operation is X, do the following, otherwise do Y.)  GPUs just do a prescribed series of operations, operating in parallel on a collection of inputs, which is good for video games, but when neural networks emerged, GPUs happened to be good for the operations described above, because of the parallelism they provide.  Nvidia made a good business of supporting the video gamers, but AI has proved lucrative at a very different scale.

Computation of the gradient is very costly -- especially so for LLMs.  LLMs may have hundreds of billions of weights, and the gradient has to be computed for each.  After each training run, the process must be repeated.

In a data center used for AI, those GPUs run hot and wear out fast.  The people running the data centers have to keep buying more.

---

# Neural Networks for Visual Recognition

---

## The Biological Foundation: Hubel and Wiesel

Before any computer scientist wrote a line of neural network code, two neurophysiologists at Harvard Medical School were recording electrical signals from individual neurons in the brains of anesthetized cats. **David Hubel** and **Torsten Wiesel** began this work in the late 1950s, and their discoveries would eventually win them the Nobel Prize in Physiology or Medicine in 1981.

Their key paper — *"Receptive fields, binocular interaction and functional architecture in the cat's visual cortex"* (*Journal of Physiology*, 1962) — built on their first publication from 1959 and remains one of the most cited papers in neuroscience. The experimental setup was elegant: project patterns of light onto a cat's retina and record which neurons in the visual cortex fire in response.

A famous discovery came almost by accident. Hubel and Wiesel had placed a small black dot on a glass slide, hoping it would excite cortical neurons the way spots of light excited retinal neurons. It largely did not. But the *edge* of the glass slide, as it was inserted into the projector at a particular angle, caused a neuron to fire dramatically. This observation led them to the foundational finding: cortical neurons respond not to spots of light, but to **oriented edges and bars**, and only when those stimuli appear at the right position and angle in the visual field.

### Simple Cells and Complex Cells

Hubel and Wiesel identified two broad classes of neurons that are directly relevant to how we now build artificial visual systems:

**Simple cells** respond to an edge or bar of light at a specific orientation *and* a specific location in the visual field. Move the edge to a different part of the image, and the cell goes silent. Tilt the edge a few degrees from the cell's preferred orientation, and the response weakens. Each simple cell is, in effect, a very precise local detector.

**Complex cells** are one step more abstract. They also prefer edges at a specific orientation, but they respond to that edge *wherever* it appears within a broader region of the visual field. They have given up positional specificity in exchange for a kind of location tolerance.

This two-level hierarchy — precise local detectors feeding into more tolerant, abstract detectors — is not merely a curiosity of cat neuroanatomy. It became the architectural blueprint for convolutional neural networks.

---

In visual recognition, an image is represented as a grid of pixels.  For the first layer of the neural network, there is a "neuron" for each pixels, and it observes the grayscale or RedGreenBlue (RGB) value for what is in a given pixel.  Then, the values for that pixel are combined with the values from some related set of pixels -- perhaps some neigboring pixels.  This combination is done by the values in the set of pixels (a vector) by a matrix (a rectangular array of numbers).  Each number in the matrix is a "weight". Then, an activation function determines what information (a number or a vector) should be passed on.  This is passed on as a "channel".  To stick with the case of color images, you start with 3 channels per pixel, those being the RGB values.  Then the channel value is added, to make a longer vector.  There are a few matrices to apply at each stage, so each stage adds a number of channels.  This expands the amount of information per pixel -- but this is compressed back down, by "pooling" the result.  So, the next layer may have fewer "neurons", but each has more information to work with.  

### What Information is Stored in Each Channel?

Roughly speaking, it is a report about something in the image.  In the early layers, it might be a horizontal edge, a vertical edge, or a diagonal edge.  In the later layers, it is not clear exactly what is being stored -- maybe something about a texture, or a replicated pattern, or a shape.

## The Convolution Idea

To understand why Hubel and Wiesel's findings translated so directly into computer vision, it helps to first appreciate the problem that earlier approaches could not solve.

### Why Fully Connected Networks Fail on Images

Consider a modest 200×200 grayscale image: 40,000 pixels. If every pixel connects to every neuron in the next layer — a *fully connected* layer — and that layer has 1,000 neurons, we already have 40 million parameters in the first layer alone. This is computationally expensive, prone to overfitting, and fundamentally wasteful, because it ignores something obvious about images: **meaningful structure is local**.

A horizontal edge is defined by the relationship between a few neighboring pixels, not between a pixel in the top-left corner and one at the bottom-right. A cat's eye looks like a cat's eye whether it appears in the upper portion of the image or the lower. Fully connected networks have no way to exploit these properties without learning them redundantly for every position.

### Filters and Weight Sharing

A **convolutional filter** (or kernel) is a small grid of weights — typically 3×3 or 5×5. Rather than connecting to the whole image, it slides across the image one small patch at a time. At each position, it computes a dot product between its weights and the underlying pixel values. The result is written into an output grid called a **feature map**.

Consider a simple 3×3 filter:

```
-1  -1  -1
 0   0   0
 1   1   1
```

Where this filter slides over a region where pixel values transition from dark (top) to bright (bottom), the dot product yields a large positive number — the filter "fires." Where the image is uniform, the result is near zero. This particular filter detects horizontal edges, and it does so *wherever they appear*, because the same weights slide across the entire image.

This is called **weight sharing**: instead of 40 million parameters for the first layer, a single 3×3 filter has just 9. In a network with many filters per layer, this is an enormous reduction in complexity — and a direct computational analog of Hubel and Wiesel's simple cells.

**Pooling layers** then play the role of complex cells: they summarize filter responses over a small neighborhood, introducing tolerance to small shifts in position.

### Learned Feature Hierarchies

In a deep convolutional network, you use not one filter but many — typically dozens per layer — and you stack multiple layers. The key insight is that you do not design these filters by hand. Backpropagation learns them from data. And what the network learns, reliably and across many different architectures, mirrors the biological hierarchy Hubel and Wiesel described:

- **Early layers** learn low-level features: oriented edges, color gradients, simple textures
- **Middle layers** combine these into corners, curves, and simple shapes
- **Later layers** respond to complex patterns: eyes, wheels, faces, entire objects

The convolutional architecture encodes a useful *inductive bias* — a built-in assumption that visual patterns are local and repeatable — rather than forcing the network to discover this from scratch. It is the right architecture for images precisely because it mirrors the actual structure of visual information.

---

## LeCun and the First Practical Success

The most famous early application of convolutional networks came from **Yann LeCun** at Bell Labs in the late 1980s and early 1990s. LeCun developed **LeNet**, a convolutional neural network trained to recognize handwritten digits, which the United States Postal Service deployed to automatically sort mail by reading ZIP codes.

This was remarkable for several reasons. First, it was a *real-world deployment* of neural networks at a time when they were largely academic curiosities. Second, it demonstrated end-to-end training via backpropagation: rather than hand-engineering features and feeding them to a classifier, the entire network — convolutional layers, pooling layers, and final classification — was trained jointly from raw pixel values to digit labels.

The dataset used, **MNIST**, consists of 70,000 28×28 grayscale images of handwritten digits (0–9). It remains a standard benchmark to this day and is the basis for many introductory tutorials and classroom exercises. A student with a few hours and basic Python knowledge can build a network that achieves over 98% accuracy on MNIST — experiencing, in compressed form, exactly what LeCun accomplished.

The conceptual shift LeNet embodied — from engineered features to *learned* features — is arguably the central idea of the entire deep learning era. Before LeNet, computer vision required human experts to write rules: look for this kind of edge here, this kind of curve there. LeNet demonstrated that a network could discover its own features, and that those learned features could be more powerful than anything hand-crafted.

---

## The Dark Years and the Comeback: Hinton and Deep Belief Networks

LeNet was a proof of concept, but through the 1990s and 2000s neural networks lost ground to other methods for most practical tasks. The core problem was depth. Backpropagation worked well for shallow networks, but training networks with many layers ran into two serious obstacles:

**Vanishing gradients**: The error signal propagated backward through many layers shrinks exponentially. By the time it reaches the early layers, it is essentially zero. Those layers do not learn.

**Poor initialization**: Networks initialized with random weights would get stuck in bad regions of the loss landscape and fail to train effectively.

The result was a practical ceiling on the number of layers that could be usefully trained, which in turn limited the complexity of features the network could learn.

### Boltzmann Machines and the Energy Landscape

**Geoffrey Hinton** (along with colleagues including Ruslan Salakhutdinov) introduced a different approach in a landmark 2006 paper: training **Deep Belief Networks** by stacking **Restricted Boltzmann Machines** (RBMs).  He shared a Nobel Prize for this, in physics as it happens, because of the way he leveraged the thermodynamic ideas of Boltzmann. 


### Layer-Wise Pretraining

Hinton's crucial insight was to train a Deep Belief Network greedily, one layer at a time:

1. Train an RBM on the raw input data. It learns first-level features.
2. Treat the hidden activations of that RBM as input data, and train a new RBM on top. It learns second-level features.
3. Repeat for as many layers as desired.
4. Fine-tune the whole stack jointly using backpropagation.

This **layer-wise pretraining** solved the initialization problem. Each layer arrives at the fine-tuning stage already encoding meaningful structure, rather than starting from random noise. The error signal from backpropagation then had a much shorter, well-prepared path to travel.

More importantly, this work demonstrated that deep networks — networks with many layers — could be trained successfully and would produce richer, more powerful representations than shallow ones. At a moment when much of the field had given up on depth, Hinton's paper reopened the question.

### The Successor Technologies

It is worth noting that RBMs and Deep Belief Networks themselves were fairly short-lived as the dominant approach. Within a few years, researchers found that the training problems Hinton had solved with pretraining could be addressed more simply through:

- **ReLU activations** --  This is an optimization of the activation function previously described
- **Better weight initialization** schemes -- choosing a good distribution curve for the randomly assigned weights.
- **Dropout** regularization -- When a neural net won't recognize anything that doesn't exactly match the training data, thats "overfitting", and this technique addresses the problem.

These ingredients, combined with large datasets and GPU computing power, produced **AlexNet** in 2012 — a deep convolutional network trained on the ImageNet dataset of 1.2 million images that dramatically outperformed all other entries in that year's ImageNet competition. AlexNet used none of the Boltzmann machinery. But it would not have been built without the conceptual groundwork Hinton's work had laid: the conviction that depth was the right direction, and that learned hierarchical representations were worth pursuing.

---

## The Arc of the Story

Tracing this history reveals a coherent set of ideas that have persisted from Hubel and Wiesel's cat experiments to today's vision transformers:

**Local structure matters.** Visual features are defined by relationships between nearby pixels, not distant ones. This insight, first demonstrated neurophysiologically, is encoded in the convolutional layer.

**Hierarchies of abstraction.** The visual system — biological and artificial — builds complex representations by composing simpler ones. Edges combine into shapes; shapes combine into objects. This principle runs from simple and complex cells through LeNet to ResNet and beyond.

**Features should be learned.** Rather than hand-crafting the intermediate representations, we should provide the network with enough data and capacity and let it discover the representations that work. LeCun demonstrated this for convolutional networks; the deep learning era has confirmed it at every scale since.

**Depth is essential.** Hinton's contribution was to show, at a moment of skepticism, that deep networks could be trained and that they learned qualitatively richer representations than shallow ones. The specific mechanism he used is less important than the door it reopened.

These ideas, rooted partly in biology, partly in mathematics, and partly in the pragmatic engineering of early systems like LeNet, form the conceptual foundation of virtually all modern visual AI.

---

## Further Exploration

If you are interested in building their own digit-recognition network can start with the **3Blue1Brown neural networks series**, which provides beautiful visual explanations alongside an interactive MNIST demo:

- [3Blue1Brown: But what is a Neural Network?](https://www.3blue1brown.com/lessons/neural-networks)

For a hands-on coding introduction, good starting points include:

- Michael Nielsen's free online book *Neural Networks and Deep Learning*, which builds MNIST from scratch in Python and NumPy
- The TensorFlow.js MNIST codelab, which runs entirely in the browser with no installation required
- The DigitalOcean tutorials for building the same network in either TensorFlow or PyTorch

You can do this stuff on your laptop: no data center required.  Your neural network might be able to recognize handwritten numbers, but not cats.  Is anyone in this class that nerdy?  Even if you aren't, you may want to view the video "But What is a Neural Network" described above.

The original Hubel and Wiesel papers are freely accessible and surprisingly readable. Their 1959 paper — *"Receptive fields of single neurones in the cat's striate cortex"* (*Journal of Physiology* 148, 574–591) — is a model of careful experimental science and worth at least a browse for anyone curious about the biological origin of these ideas.

---

# Large Language Models: The Birth of the AI Chatbot

---

## Language is Hard

Language conveys the patterns of thought, or at least the patterns of verbal thought.  It is inherently complicated.  Consider the web of meaning around the word "dog".  Related words:

- puppy
- noun (usually)
- hound
- mammal
- carnivore
- bite
- run
- pant
- pet

Now consider the use of the word in the sentence: Is it subject or object?  Is the subsequent use of "it" a reference to the dog, or something else in the prompt?  How does "brown dog" differ from "dog"?  If the word "May" is used, is it the month, or a person's name, or a modal verb, as in "may go"? In a typical paragraph, many words interact to construct the meaning to be conveyed.  

These problems were sticky.  It took a while to figure them out.  The critical moment was the 2017 publication of "Attention is All You Need" by Ashish Vaswani and other researchers working at Google.  What they came up with is complicated. It is not obvious how they derived these ideas.  What follows below is a description of the architecture described by that paper.  In this step, as in many of the refinements of AI before and since, researchers have proceeded by intuition and experiment, as well as analysis.

---

## 1. Tokens — What the Model Reads

When a large language model reads text, it does not read words the way you do, and it does not read letter by letter either. Instead it breaks text into chunks called **tokens**.

Why not whole words? English alone contains hundreds of thousands of words — and that is before adding slang, technical terms, foreign words, misspellings, and new coinages. A dictionary large enough to cover everything would be unmanageably large, and the model would struggle with any word it had not seen before, or words it has seen too rarely to derive meaning.

Why not single letters? Letters carry almost no meaning on their own. The letter "b" tells you almost nothing. Processing text one letter at a time would be like trying to understand a painting one brushstroke at a time.

Tokens are a middle ground. A typical model uses a vocabulary of roughly 50,000 to 100,000 tokens — a manageable number that can represent virtually any text. Common words like "the" or "cat" become a single token. Less common words get broken into meaningful pieces: "unbelievable" might become "un," "believ," and "able." Punctuation and spaces are tokens too.

Notice that some tokens are whole words, some are word-fragments that carry meaning (prefixes like "un-" or "pre-," suffixes like "-ing"), and some are punctuation or numbers. The model may never have seen the word "unbelievable" — but because it knows "un-," "believ," and "-able" from thousands of other words, it can handle it anyway. This is one of the key efficiencies of the token approach: a model that knows sub-word fragments can generalise to words it has never seen before.

This also explains a curious limitation: if you ask a model to count the letters in *strawberry*, it may get it wrong. The model never sees individual letters — it sees tokens like "straw" and "berry," and has to reason about the letters inside them indirectly. It often fails at exactly these simple character-level tasks, while succeeding at far more complex semantic ones.

The tokenisation process itself is not arbitrary. Before a model is trained, a separate **tokeniser training phase** runs on a large corpus of text to determine the optimal vocabulary using an algorithm called Byte Pair Encoding (BPE). The process begins with individual characters, then iteratively merges the most frequent adjacent pairs — "t" and "h" merge to "th," then "th" and "e" to "the," and so on — until a target vocabulary size is reached, typically between 32,000 and 128,000 tokens. This produces a vocabulary that represents common words as single tokens and rare words as sequences of meaningful fragments.

English can be represented fairly well using a dictionary of 30,000 to 50,000 tokens.  A dictionary of 150,000 tokens seems to suffice for all languages that are common on the Internet.  LLMs don't do well with languages that don't appear frequently on the Internet.

Once tokenised, each token is assigned a unique identification number. From this point on, the model works entirely with numbers, not text -- but as we'll see, the number maps to a vector, as described in the embedding layer below.  The tokenizing layer uses no neural network.  It is a one time statistical analysis of all Internet text.

For an image, each pixel is associated with a "neuron" in the first layer of the model.  For a prompt of text passed to an LLM, each token in the promt is associated with a neuron.

---

## 2. Tokens and Embeddings: The LLM Input Layer

Tokens cannot be fed directly into a neural network, because unlike pixel values, words have no natural numeric representation. The first layer of an LLM must therefore construct one.

This is done via an **embedding layer**. Each token is looked up in a learned table, and the result is a vector — a list of hundreds or thousands of floating-point numbers. In many models, a typical embedding vector is about 4000 numbers.  Unlike pixel values, which are read directly from the image, these embedding vectors are **learned during training**.  That is, the numbers in the vector are initially assigned entirely randomly, and the vector for "dog" probably doesn't start out close to the vector for "puppy" in the embedding space. The network adjusts them so that tokens with similar meanings end up with similar vectors — geometrically close to each other in the high-dimensional space the vectors inhabit. So "king" and "queen" end up closer together than "king" and "bicycle."  The values of the numbers in each vector are weights to be adjusted by computing an error function and gradient descent.

This is a fundamental difference from visual recognition: pixel values describe physical reality directly, while embedding vectors describe semantic relationships — and the network figures out what those relationships should be through training.  I am using the word "semantic" advisedly here, as I don't really think it fits.  Semantic meaning associates a word like "dog" with real world objects that are dogs.  An LLM doesn't have any knowledge of real world objects.  So, instead of "semantic" meaning, it might be better to say "distributional" meaning: how does the distribution of the word fit with observed patterns of the language?

---

## 3. Positional Encoding

An embedding vector captures what a token means, but not where it appears in the sequence. The word "not" means something very different at different positions in a sentence. LLMs need to encode this positional information explicitly.

For each position in the sequence, a **positional encoding vector** is computed and added element-wise to the token's embedding vector. The result is a single combined vector per token that encodes both identity and position.

The original scheme, introduced in the "Attention Is All You Need" paper, uses sine and cosine functions at different frequencies to generate the positional vectors. This has an intuitive resemblance to a Fourier decomposition: low-frequency components capture broad positional information (early versus late in the sequence), while high-frequency components capture fine-grained position (the exact slot). A useful analogy is a clock: the second hand, minute hand, and hour hand each complete their cycles at different rates, and together they encode time unambiguously. The sinusoidal positional encoding does the same thing across the dimensions of the vector.

An important property of this scheme is that it preserves information about relative distance between tokens — the network can recover not just where each token is, but how far apart any two tokens are — which is valuable for understanding grammatical and semantic relationships.

Each embedding vector and the position vector are of the same length.  These are combined by adding them together.  After combining embeddings and positional encodings, the result is a set of N vectors — one per token in the prompt — which serves as the starting state for the transformer.

---

## 4. The Attention Mechanism

The attention mechanism is the heart of the transformer. It allows every token to gather information from every other token in the sequence, so that each token's representation can reflect its full context.

(As well as providing the basis for LLMs, attention based mechanisms have now displaced convolutional networks for visual recognition.  They can recognize more patterns in a visual image than convolutional networks, as they are not constrained to particular pixel neiborhood.  The hooves on a horse may be widely separated within an image, but those parts of the image are related in determining what the image represents.)

### Queries, Keys, and Values

Each token's vector is transformed into three derived vectors through learned weight matrices:

- **Query (Q):** what this token is looking for
- **Key (K):** what this token advertises about itself
- **Value (V):** what this token will contribute if selected

These are simply linear transformations — matrix multiplications — and the Q, K, and V vectors are typically lower-dimensional than the original input vectors.  

This step and each of those that follow use matrices that are initiallized, at the start, to *entirely random* values.  Again, these are weights, some of the parameters of the model.  You can see how typical LLMs these days end up with hundreds of billions of parameters, meaning hundreds of billions of weights.  And, the value for each of these weights must be optimized, again by computing an error function and using gradient descent -- lots of electricity.

### Computing Attention Scores

For each token, its Q vector is compared against the K vector of every other token (including itself) by computing the dot product. A high dot product indicates that the two tokens are highly relevant to each other. This produces a matrix of scores — every token against every token.

The scores are scaled by dividing by the square root of the vector dimension, to prevent the values from growing too large. They are then passed through a softmax function, which converts them into weights that sum to 1 — a kind of learned probability distribution over the sequence.

### Producing the Output

Each token's output vector is then computed as a weighted sum of all the Value vectors, where the weights are the attention scores just computed. A token's output is therefore dominated by the Value vectors of whichever tokens it attended to most strongly. This is how "bank" in "river bank" learns to attend to "river" and update its representation accordingly.

### Multi-Head Attention

Rather than performing this process once, the transformer performs it multiple times in parallel — each time using different learned Q, K, V matrices. Each parallel run is called an **attention head**, and different heads can learn to attend to different kinds of relationships: syntactic structure, semantic similarity, coreference, and so on.

The outputs of all heads are concatenated and then projected back to the original vector dimension via another learned matrix. The dimensionality entering and leaving the multi-head attention block is therefore the same.

---

## 5. The Feed-Forward Layer

After the attention step, each token has gathered contextual information from across the sequence. But the attention mechanism is essentially a weighted averaging operation — good at routing information, but limited in its ability to transform that information in complex, nonlinear ways. The feed-forward layer provides that transformative capacity.

Each token's vector is passed independently through a small neural network consisting of two linear transformations with a nonlinearity between them. Crucially, there is **no communication between tokens** at this stage — each token is processed entirely on its own.

### Why the Expansion?

The first linear transformation projects each vector into a higher-dimensional space.  In the original "Attention is All You Need" paper, the vector was made four times larger. This expansion provides more "analysis knobs" for the network to work with, giving it room to capture subtle distinctions in meaning that would be lost in a lower-dimensional representation.

### Why the Nonlinearity?

The nonlinearity — typically ReLU, which sets any negative value in a computed vector to zero — is essential. Without it, stacking linear transformations one after another is mathematically equivalent to a single linear transformation, no matter how many layers you add. The nonlinearity breaks this collapse by allowing different neurons to switch on or off depending on the input, creating piecewise behavior. This is what allows the network to represent sharp, conditional, threshold-like relationships — the kind that meaning actually involves.

### The Compression Step

The second linear transformation projects back down to the original vector dimension. This is a learned compression: the network decides what to preserve and what to discard from the richer intermediate representation.

### Residual Connection and Normalization

After both the attention block and the feed-forward block, the original input vector is added back to the output — a **residual connection**. This means the network learns adjustments and refinements to the representation rather than recomputing it from scratch, which makes training much more stable. A Layer Normalization step follows, adjusting the values in each vector to a consistent scale to prevent any dimension from dominating.

The full sequence within each transformer layer is therefore:

1. Multi-head attention
2. Add residual + normalize
3. Feed-forward expand (linear)
4. Nonlinearity (ReLU)
5. Feed-forward compress (linear)
6. Add residual + normalize

A clean way to summarize the division of labor: **attention handles communication between tokens** — which tokens should influence which — while the **feed-forward layer handles computation within each token** — what to do with the information once gathered. That alternation is the heartbeat of the transformer.

---

## 6. Stacking Layers

The block described above — attention followed by feed-forward, with residual connections and normalization — constitutes one transformer layer. In practice this block is stacked many times. The original "Attention Is All You Need" paper used 6 layers; modern large models use far more.

The number of layers, the vector dimension size, and the number of attention heads are the three main dials for scaling up a model, and together they largely determine the total parameter count. As a rough guide:

- GPT-2 (largest version): 48 layers
- GPT-3: 96 layers
- LLaMA 2 70B: 80 layers
- Frontier models (GPT-4, Claude, Gemini): not publicly disclosed, estimated 100–200 layers

Each layer refines the token representations further. Early layers tend to capture syntactic and local relationships; later layers capture more abstract, semantic, and long-range relationships — loosely analogous to how early layers in visual recognition detect edges while later layers detect objects.

---

## 7. Training and Gradient Descent

The architecture — the number of layers, vector dimensions, attention heads — is fixed before training begins. What training adjusts is exclusively the **weights**: all the learned matrices for embeddings, Q/K/V projections, feed-forward transformations, and so on.

LLMs are trained on all the text available on the Internet.  This is unsupervised training.  Nothing is labeled up front, as was the case for visual recognition.  The text is just passed to the LLM as is.  Then the LLM discovers the patterns.

Training proceeds by gradient descent:

1. Feed a training example through the network (the forward pass)
2. Compare the output to the correct answer using a loss function — for LLMs, typically how well the model predicted the next token
3. Compute the gradient — how much each weight contributed to the error
4. Nudge every weight slightly in the direction that reduces the error (the backward pass, via backpropagation)
5. Repeat billions of times across an enormous dataset

In practice, **stochastic gradient descent** is used: rather than computing the gradient across the entire dataset before taking a step, a step is taken after each small batch of examples. This is both computationally necessary and beneficial, as the noise in batch-by-batch updates helps the model avoid getting stuck in poor solutions.

The backward pass is roughly twice as expensive as the forward pass, making training significantly more costly than inference. This is why training frontier models requires thousands of GPUs running for months, at a cost of tens or hundreds of millions of dollars.

The residual connections play an important role early in training: when the learned transformations are still essentially random noise, the signal flows through the residual connections largely unchanged, and the network effectively behaves like a shallower model. The layers gradually learn to contribute useful transformations as training progresses.

---

## 8. Fine-Tuning with LoRA

After pre-training, models are refined through fine-tuning — using human feedback and reinforcement learning to shape the model's behavior toward being helpful, accurate, and safe. Without fine-tuning, the LLM will predict the next series of tokens, sure, but with no particular purpose or goal.  It will just blather on in meaningful sentences, but it will not complete the task or request.

Fine tuning steers the model to do the following:

- First and formost, complete the task.  That might mean just answering a question, but it might mean creating a computer program or performing some other function.
- Second, seem friendly and helpful.  The AI teams want you to like interacting with their chatbots.  Unfortunately, as we know, it is often dangerous to help someone, if they are planning something bad or unfortunate.
- Third, don't do dangerous stuff.  Don't convey information that will put weapons of mass destruction into the wrong hands.  Don't allow child sexual abuse.  Etc.  These are "guardrails", all established by fine tuning.  They work very poorly.

The challenge is doing fine tuning without destabilizing the vast knowledge encoded in the pre-trained weights.

The most widely used solution is **LoRA** (Low-Rank Adaptation). Rather than modifying the original weight matrices directly, LoRA freezes all pre-trained weights and adds a small parallel structure alongside each matrix it targets.

The mechanism is elegant. Instead of adding a full-sized matrix — which would have as many parameters as the original — LoRA adds two much smaller matrices A and B, where A is tall and thin and B is short and wide. Their product A×B has the same dimensions as the original weight matrix but far fewer parameters, because the rank of the product is much smaller than the full matrix. This is the "low rank" in LoRA.

At the start of fine-tuning, A and B are initialized so that their product is zero — meaning the modification has no effect. Only A and B are updated during fine-tuning; the original matrix remains frozen. The effective weight used in the forward pass is the original matrix plus A×B.

LoRA is typically applied to the Q and V matrices in the attention mechanism, based on the intuition that these matrices most directly control what the model pays attention to, and are therefore the highest-leverage targets for behavioral adjustment. This choice is informed by empirical experimentation rather than strict theoretical derivation — a pattern common throughout the field, where experiment leads and theory follows.


---

## 9. Reasoning

"Reasoning" in modern LLMs refers to a technique applied at inference time, not during training. The core idea is **chain-of-thought**: rather than jumping straight to a final answer, the model generates a sequence of intermediate tokens — visible working steps — before producing its response.

This works because each token the model generates becomes part of the context for generating the next token. By writing out intermediate steps, the model effectively gives itself scratch paper: each step can build on previous steps, allowing the model to tackle problems too complex to solve in a single forward pass. More tokens means more computation, which is why reasoning models are slower and more expensive — they are deliberately generating many more tokens before arriving at an answer.

More sophisticated variants go beyond linear chains of thought. **Beam search** keeps multiple candidate sequences in play simultaneously, pruning low-probability branches as generation proceeds. **Tree search** allows genuine backtracking — exploring a branching space of reasoning paths and abandoning dead ends. **Self-consistency** generates multiple independent reasoning chains for the same problem and takes a majority vote on the final answer, exploiting the fact that correct reasoning paths tend to converge even when they differ in their route.

The frontier reasoning systems are believed to combine these approaches — searching over possible reasoning paths while also learning to evaluate which paths are promising. The details of specific implementations are not publicly disclosed.

The key insight is that reasoning is not a new mechanism but a clever exploitation of the existing token-by-token generation process: using the model's own output as extended context for continued computation, and optionally exploring multiple such continuations before committing to an answer.  But, it makes use of an LLM more expensive.  Before the use of reasoning, answers from the LLM were not as good, but they didn't require that much CPU, as all the heavy processing was done during the training of the model.  Now, everyday use of an LLM is CPU intensive as well.


## 10. An Aside: The Chinese Strategy

Various Chinese companies and academic groups are competing with US companies for AI leadership.  During the Biden administration, this competition was seen as a security threat.  Therefore, sale of the most powerful GPU chips to Chinese entities was forbidden.

This approach may not have worked.  The Chinese could still have rented time on data centers outside China to do their AI development.  In any case, President Trump cut a deal with China to allow access to the powerful chips.  (I will avoid an editorial aside.)

So, what happened? The Chinese didn't buy any.  For two reasons: (1) They are making great progress developing their own AI chips, and they want strong technological expertise in this area. (2) Instead of dedicating ever more electricity and data centers to the task of AI development, they have focused on making the process more efficient.  The DeepSeek LLM was released by a Chinese group a couple of years ago, and it gave results that were competitive with the best American LLMs, at a fraction of the development cost.

---

# A Guide to Modern AI Architectures and Their Applications

---

## Chapter 1: A Taxonomy of Neural Networks

At its core, a neural network is a system of interconnected nodes — loosely inspired by neurons in the brain — that learns to transform inputs into outputs by adjusting the strength of connections through exposure to data. But this single description covers an enormous variety of architectures, each evolved to suit a different kind of problem. Understanding which architecture fits which task is one of the foundational insights of modern AI.

### Feedforward Networks and Autoencoders

The simplest and oldest form is the feedforward network, in which data flows in one direction — from input, through one or more hidden layers, to output. The multilayer perceptron (MLP) is the canonical example. It excels at tabular data, regression, and classification tasks where the inputs have no special spatial or temporal structure: predicting house prices from a list of features, for instance, or classifying a patient's test results.

A close relative, the autoencoder, is a feedforward network trained to compress its input down to a compact internal representation and then reconstruct it. The bottleneck forces the network to learn efficient summaries of the data — making autoencoders useful for anomaly detection (inputs that compress poorly are unusual) and representation learning (the compressed form can be used as a rich feature vector for other tasks).

### Convolutional Networks

Convolutional neural networks (CNNs) were designed for data with spatial structure, particularly images. Their central insight is weight sharing: rather than learning separate parameters for every position in the input, a CNN uses a small filter — a grid of learned numbers — that slides across the entire input. The same filter detects the same feature (an edge, a curve, a texture) wherever it appears. This makes CNNs extraordinarily parameter-efficient and gives them a natural form of translation invariance.

CNNs are the workhorses of computer vision: image classification, object detection, and segmentation. The same idea applied to one-dimensional sequences — temporal convolutional networks — makes them competitive with recurrent architectures for audio and time-series data.

### Recurrent Networks

Where feedforward networks treat each input independently, recurrent neural networks (RNNs) maintain a hidden state that carries information forward through a sequence. This makes them natural for language, speech, and any domain where the meaning of the current input depends on what came before.

Basic RNNs struggled with long sequences because gradients vanish as they propagate back through many time steps. Long short-term memory networks (LSTMs) and their simpler cousin, the gated recurrent unit (GRU), solved this with explicit gating mechanisms that learn what to remember and what to forget. Sequence-to-sequence models — encoder-decoder pairs built from LSTMs — were the dominant architecture for machine translation before transformers displaced them.

### Transformers

The transformer is currently the dominant architecture for the majority of AI tasks. Its core innovation is self-attention: every position in a sequence can directly attend to every other position, weighting each by learned relevance. Unlike RNNs, this operation is fully parallelizable, which enabled training on vastly larger datasets and produced the large language models that have reshaped the field.

Two main variants have emerged. Encoder-only models (the BERT family) read the full sequence bidirectionally and excel at understanding tasks: classification, named entity recognition, search. Decoder-only models (the GPT family) generate text autoregressively and are the basis for conversational AI. Vision Transformers (ViT) apply the same attention mechanism to image patches rather than tokens and are now competitive with CNNs for many vision tasks.

### Generative Models

A separate family of architectures is concerned not with classifying or predicting, but with generating new data. Generative Adversarial Networks (GANs) pit a generator against a discriminator in an adversarial game: the generator tries to produce realistic images; the discriminator tries to detect fakes. This dynamic produces very sharp outputs but is notoriously difficult to train.

Diffusion models — the basis of Stable Diffusion, DALL-E, and Midjourney — have largely superseded GANs for image generation. They learn to reverse a process of systematic noise addition, and are discussed in detail in Chapter 3. Variational autoencoders (VAEs) learn a smooth, structured latent space that can be sampled and interpolated, making them useful for controlled generation and the compression stage that sits inside many diffusion pipelines.

### Specialist and Hybrid Architectures

Several important architectures address domains where the above do not naturally fit. Graph neural networks (GNNs) handle data defined as graphs — molecular structures, social networks, knowledge graphs — by having nodes iteratively pass messages to their neighbors. Reinforcement learning networks, typically MLPs or CNNs, learn policies and value functions through trial and error with reward signals, and underlie systems like AlphaGo and modern robotics.

Spiking neural networks communicate through discrete spikes in time rather than continuous values, placing them closer to biological neurons. They are efficient on specialized neuromorphic hardware but remain largely a research area. State space models — of which Mamba is the most prominent recent example — aim to replace transformers for very long sequences by using recurrent-style state updates that can nonetheless be parallelized during training.

In practice, the most capable modern systems combine several of these ideas. Vision-language models run a ViT alongside a transformer language model. Generative image models use transformer backbones. Reinforcement learning is layered atop pretrained transformers in the RLHF process that aligns conversational AI. The boundaries between these families are, increasingly, permeable.

---

---

## Chapter 3: Diffusion Models and the Art of Structured Unmaking

### Learning to Denoise

The central idea of a diffusion model is counterintuitive: rather than training a network to draw images, train it to un-destroy them. The training process begins with real images from a large dataset and systematically corrupts each one by adding Gaussian noise across a sequence of many small steps. After roughly a thousand steps, following a carefully designed noise schedule, every image — regardless of its content — has been reduced to something statistically indistinguishable from pure random noise. Content has been fully erased.

At each intermediate step along this degradation, the network is presented with the noisy image and asked a single question: what noise was added here? The network does not need to reconstruct the full clean image; it only needs to estimate the noise component at this particular level of corruption. This is a much simpler regression problem, and it can be learned reliably.

The loss function is correspondingly simple. If ε is the actual noise added and ε_θ is the network's prediction, the training objective is to minimize the mean squared difference between them across all timesteps and all training images. Over millions of such training examples, the network learns a rich internal model of what natural images look like at every scale and level of abstraction — not by memorizing images, but by learning what distinguishes signal from noise in them.

### Reversing the Process

Generation is the reverse of training. A fresh sample of pure Gaussian noise is drawn — a random image with no structure — and the denoising network is applied iteratively. At each step, the network estimates the noise present in the current image, and a small fraction of that estimated noise is subtracted. After all steps are completed, a coherent image has emerged from what began as randomness.

The critical insight is that the network never generates pixels directly. It makes a series of small corrections, each removing a tiny amount of noise, each guided by everything it learned during training about the statistical structure of natural images. The image is not constructed from a template or assembled from parts. It coalesces, step by step, from structured noise removal.

An important practical refinement is that generation does not happen in the space of raw pixels. Running a thousand denoising steps on a full-resolution image would be computationally prohibitive. Modern systems such as Stable Diffusion work in a compressed latent space: a variational autoencoder first encodes the image into a representation roughly sixty-four times smaller in area, diffusion happens in that compact space, and a decoder expands the result back to full resolution. This is what makes high-quality image generation feasible on consumer hardware.

### Guiding Generation with Text

A diffusion model trained without conditioning generates images that reflect the distribution of the training data but cannot be steered toward a specific subject. Text-to-image generation requires a mechanism for injecting the semantic content of a prompt into the denoising process.

This is accomplished through a text encoder — typically CLIP, a model trained to embed images and their text descriptions into a shared vector space. A prompt like "a knight riding a dragon over a neon-lit cyberpunk city at sunset" is encoded into a vector that captures its semantic content. At every denoising step, this vector is fed into the network via cross-attention, where it influences which directions the denoiser corrects toward. The noise removal is no longer neutral — it systematically favors image states consistent with the prompt.

The strength of this influence is controlled by the guidance scale parameter. A high guidance scale produces images that closely match the literal prompt but may be garish or oversaturated, because the model is being pushed into an extreme corner of the probability distribution. A lower value yields more natural-looking images that interpret the prompt more loosely. The right value depends on the specificity of the prompt and the desired aesthetic.

### The Latent Space and Novel Images

A question that naturally arises: if the model was trained on specific images, how can it generate a "knight riding a dragon over a cyberpunk city" — an image that certainly did not appear in any training set?

The answer is that the model was never trained to remember images. It was trained to understand the structure of visual information. All those millions of training images were not stored; they were compressed into the weights of the network as a rich statistical model of what patterns, textures, lighting conditions, spatial relationships, and object appearances tend to occur in natural and man-made imagery.

This internal model can be thought of geometrically as a latent space: a high-dimensional mathematical space in which nearby points correspond to visually similar concepts. Dragon scales and reptile skin are neighbors. Neon glow and rain-slicked pavement are neighbors. Sunset orange and warm backlighting are neighbors. The CLIP text encoder places the prompt's meaning as a point in this same space.

The novel prompt lands in a region of the latent space that no training image directly occupies — but it is surrounded by well-learned concepts on all sides. The denoising process navigates toward that region, synthesizing visual elements from all the neighboring concept clusters simultaneously. The result is an image that has never existed, built from a visual grammar that was thoroughly learned.

This compositionality is powerful but imperfect. Simple combinations work reliably; unusual structural relationships between unfamiliar pairings can fail. The model may understand dragons and knights separately but struggle to correctly render one astride the other, because that particular spatial relationship was not common in training data. Techniques such as attention weighting, negative prompting, and iterative refinement exist largely to address such compositional failures.

---

## Chapter 6: Generating the Unprecedented — How Diffusion Models Compose Novel Images

*This chapter revisits the question raised in Chapter 3 from a different angle: not how diffusion models work mechanically, but how they produce images of things that never existed in their training data.*

### The Latent Space Revisited

When a diffusion model is trained on millions of images, it does not store those images in any recoverable form. What it acquires is a parametric model of the statistical structure of visual data — encoded in the billions of numerical weights of the denoising network. These weights collectively represent something like a map of the space of plausible images.

This map can be thought of geometrically. Every possible image corresponds to a point in a very high-dimensional space. The training process causes the network to learn which regions of this space contain natural, coherent images (dense with training examples) and which regions do not (sparse, far from any training example). The denoising process can be understood as a learned vector field that, at every point in this space, points toward the nearest dense region — the nearest plausible image.

Within the space of plausible images, concepts cluster. Images containing dragon scales cluster near images containing reptile skin and metallic armor. Images containing neon-lit streets cluster near images containing rain, urban nightscapes, and saturated artificial color. Sunset imagery clusters near warm-toned skies and silhouetted horizons. These clusters overlap and interpenetrate in complex ways across hundreds of dimensions.

### Composition Without Recall

When a novel prompt arrives — "a knight riding a dragon over a neon-lit cyberpunk city at sunset" — the CLIP text encoder places its meaning as a point in the same space. This point lies in a region that no training image occupies, but it is surrounded by the dense clusters corresponding to each component concept.

The conditioned denoising process navigates toward this point. At each step, the denoiser makes a correction that moves the current image state toward regions of the space that are simultaneously consistent with armor, with reptilian scales and wings, with neon and wet pavement, and with warm sunset lighting. None of these constraints requires recalling a specific training image. Each is a direction in the learned vector field, and the denoising trajectory follows the resultant of all of them.

The result is a genuinely novel image — one that synthesizes visual elements from many concept neighborhoods without copying any of them. The illumination on the armor reflects not a memorized photograph but the learned relationship between metallic surfaces and directional warm light. The texture of the scales reflects not a stored image of a reptile but the statistical patterns that distinguish scale texture from smooth skin from rough stone.

### What Remains Difficult

This process is powerful but not unlimited. Compositionality — correctly rendering the spatial and relational structure of a prompt, not just its component concepts — is where current diffusion models most commonly fail.

Generating "a red ball to the left of a blue cube" reliably is harder than generating either object alone, because training images rarely depicted those objects in explicitly labeled spatial relationships. Generating "a knight riding a dragon" requires correctly modeling the rider-mount relationship: scale, posture, point of contact, physical plausibility. This kind of structural composition requires understanding that exceeds the statistical co-occurrence of visual patterns.

The guidance scale parameter, discussed in Chapter 3, represents one attempt to steer around this: by amplifying the text conditioning signal, it pushes the denoising process more forcefully toward prompt-consistent regions. But this comes at the cost of naturalness — high guidance produces oversaturated, almost hallucinatory images in which the model has been pushed into an extreme corner of the probability distribution.

Iterative refinement techniques, attention weighting in the cross-attention layers, and inpainting — generating only specific regions of an image while conditioning on the rest — are among the practical tools that practitioners use to achieve compositional precision. The underlying challenge remains an active area of research, connected to broader questions about whether deep learning systems can achieve the kind of structured, relational reasoning that humans apply effortlessly to novel descriptions.

---


## Chapter 4: Artificial Vision in Motion — Self-Driving Cars

### The Full Stack

A self-driving vehicle is not a single AI system but a tightly integrated pipeline of AI and classical engineering components, each solving a distinct subproblem, with the outputs of each stage feeding the next. Understanding this stack reveals both the sophistication of the engineering and the reasons why full autonomy has proven so difficult to achieve.

The pipeline begins with sensors. A fully capable autonomous vehicle typically carries four complementary sensing modalities. Cameras provide rich color and texture information across a 360-degree field but perform poorly in rain, fog, and darkness. LiDAR fires pulses of laser light and measures the return time to construct a precise three-dimensional point cloud of the surroundings — accurate and lighting-independent but expensive, and degraded by heavy precipitation. Radar is cheap, penetrates weather reliably, and measures the velocity of detected objects with high accuracy, though its spatial resolution is too coarse to distinguish object shapes. GPS combined with high-definition maps provides centimeter-level positional accuracy when satellite signal is strong and supplies pre-built knowledge of road geometry, lane markings, and speed limits.

The diversity is deliberate. Each sensor has distinct failure modes; the system is designed so that any single sensor can fail without disabling the car. That redundancy comes at significant hardware cost, which has become a significant point of differentiation between competing approaches to the problem.

### Perception

Sensor data from all modalities must first be fused into a unified representation of the scene. This sensor fusion step is more complex than it might appear: the sensors run at different frequencies, have different spatial coordinate frames, and have different latencies. Transformer architectures have become the approach of choice here, treating each sensor's output as a sequence of tokens that cross-attend to each other, learning which information from which sensor is most relevant in any given driving context.

From the fused representation, three parallel perception tasks proceed. Object detection assigns bounding boxes and class labels to every vehicle, pedestrian, cyclist, and obstacle in the scene. CNNs trained on massive datasets of labeled driving footage do this reliably in good conditions, using architectures such as YOLO for cameras and PointPillars for LiDAR point clouds. Semantic segmentation labels every pixel of every camera image with a category — road surface, lane marking, sidewalk, vegetation, building — giving the car a fine-grained understanding of the drivable space. Localization matches current sensor readings against the stored HD map to determine the car's precise position and heading, typically to within a few centimeters.

### Prediction and Planning

Knowing the current state of the scene is necessary but not sufficient. The system must anticipate the near-future behavior of every other agent — where will that cyclist be in three seconds? Will that pedestrian at the corner step into the road? This trajectory prediction problem is among the hardest in the stack because human behavior is governed by social conventions and intentions that are not directly observable.

Modern prediction models use transformers or graph neural networks that represent each agent as a node in a graph and reason over the interactions between them. A pedestrian facing the road, near a crosswalk, who has been glancing toward oncoming traffic, is likely about to cross. The output of such a model is not a single predicted trajectory for each agent but a probability distribution over several plausible futures. Planning must then navigate safely across all plausible futures simultaneously, not just the most likely one.

Planning itself is organized into three nested levels. Route planning is essentially navigation: select a path through the road network from origin to destination. Behavior planning makes higher-level tactical decisions at each moment: when to change lanes, when to yield, when to proceed through an intersection, how to react to an unusual obstacle. Motion planning works out the precise trajectory — the curve through space and the speed profile along it — that the vehicle should execute over the next few seconds, subject to both physical constraints (steering geometry, tire friction limits) and comfort constraints (passengers notice sudden lateral accelerations even when mechanically safe).

The final stage, control, translates the planned trajectory into actual commands to the vehicle's actuators: steering angle, throttle percentage, brake pressure. This stage is typically implemented with classical feedback controllers — PID controllers and model predictive control — rather than neural networks, because these methods are well-understood, formally analyzable, and certifiable for safety.

### The Modular vs. End-to-End Debate

The pipeline described above represents what might be called the modular philosophy: each stage of reasoning is implemented as a distinct, interpretable, testable component. Waymo is the clearest exponent of this approach. Its advantage is that engineers can isolate failures — if the car behaves unexpectedly, it is possible to examine the output of each stage and determine where the reasoning went wrong.

Tesla has pursued a substantially different philosophy, using end-to-end neural networks that take camera pixels as input and produce driving commands as output, with the intermediate representations learned rather than designed. The argument for this approach is that human engineers cannot anticipate all the intermediate representations that matter; learning them from data may produce a richer internal model than hand-engineered modules can.

Both approaches have made remarkable progress. The fundamental challenge for both is the long tail of rare situations: the child who runs into the road between parked cars, the construction zone laid out in a way no training example anticipated, the driver ahead behaving in an inexplicable way. No finite training set covers all such cases, and the consequences of failure are severe.

---

## Chapter 5: Waymo, Tesla, and the Meaning of Autonomy

### The SAE Scale

Discussion of self-driving cars is often confused by imprecise use of the term "autonomous." The Society of Automotive Engineers has defined a six-level taxonomy that provides useful precision:

| Level | Description | Human role |
|---|---|---|
| 0 | No automation | Driver performs all tasks |
| 1 | Driver assistance | Single aids, such as adaptive cruise control |
| 2 | Partial automation | Car manages steering and speed; human must supervise continuously |
| 3 | Conditional automation | Car manages driving; may request human takeover |
| 4 | High automation | Fully driverless within a defined operational domain |
| 5 | Full automation | Fully driverless in all conditions without restriction |

A legally and commercially critical threshold lies between Level 2 and Level 3. Below Level 3, the human driver retains legal responsibility at all times. At Level 3 and above, the manufacturer assumes responsibility for the vehicle's behavior during autonomous operation. This distinction has powerfully shaped how companies position their products.

### Waymo: Onboard Intelligence, Not Cloud Dependence

Waymo operates fully driverless paid robotaxi services across San Francisco, Los Angeles, Phoenix, and Austin — true Level 4 operation within those cities' defined operational domains. A common misconception is that Waymo vehicles rely on cloud computing for their real-time decisions, a natural assumption given that Waymo is an Alphabet company. This is incorrect.

All time-critical decisions — perception, prediction, and planning — are executed onboard, in the vehicle, by a purpose-built computer processing the sensor data in real time. The physics of the situation demand this: a cellular round-trip to a data center and back introduces hundreds of milliseconds of latency. A pedestrian stepping into the road at 30 miles per hour covers several feet in that time. Real-time driving cannot tolerate network-dependent latency.

The cloud is used — but for different purposes: training new models on aggregated fleet data, distributing software updates, remote monitoring of the fleet, and providing human assistance in edge cases where the car has encountered a situation outside its operational domain and has safely stopped to await guidance. A cellular outage would not cause a Waymo vehicle to stop or behave unsafely; it operates self-sufficiently.

Each Waymo vehicle carries camera, LiDAR, and radar arrays together with the onboard computer that processes their output. This sensor suite is expensive, which has constrained Waymo's scaling relative to camera-only competitors.

### Tesla: A Different Bet

Tesla's consumer "Full Self-Driving" product is officially classified as a Level 2 system. The driver must remain attentive and ready to intervene at all times; the system provides assistance but does not assume responsibility. Tesla's own documentation states this clearly, even as the product's name has attracted regulatory scrutiny for implying a capability it does not yet have.

Tesla's technical bet differs from Waymo's in two important respects. First, camera-only sensing: Tesla argues that humans navigate complex environments using only eyes, and that sufficient camera data — drawn from millions of customer vehicles driving millions of miles daily — can train a system to do the same, making expensive LiDAR unnecessary. Second, end-to-end neural networks: Tesla has progressively replaced its hand-engineered perception and planning modules with learned representations, arguing that the network can discover better internal representations than engineers can design.

Tesla launched a commercial Robotaxi service in Austin, Texas in mid-2025, initially with a safety employee present in the passenger seat. By early 2026, the service was operating in Austin without any Tesla employee in the vehicle — genuine Level 4 operation within that geofenced area. The service has since expanded in limited form to San Francisco, though California regulations required a safety driver to remain seated there.

### Safety and the Long Road Ahead

Waymo has published comparative safety analyses showing significant advantages over human-driven vehicles across metrics including injury-causing crashes per mile, crashes involving pedestrians and cyclists, and crashes resulting in serious injury. These figures reflect millions of fully driverless miles across multiple cities.

No equivalent independently verified dataset yet exists for Tesla's Robotaxi at comparable scale, given its recent and more limited deployment. The coming years will produce the data needed to make meaningful comparisons between the two technical philosophies.

Neither company has solved the problem. Level 5 — full automation under any conditions anywhere — remains a distant goal. The challenge is not the typical driving that both systems handle well; it is the unbounded variety of atypical situations that the physical world generates without warning. Both the modular and end-to-end approaches are ultimately attempts to build systems robust enough to handle that long tail. The question of which approach gets there first, and at what scale, remains genuinely open.

---
