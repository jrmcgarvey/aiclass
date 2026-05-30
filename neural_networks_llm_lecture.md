# Neural Networks and Large Language Models: From Visual Recognition to Reasoning

## 1. Visual Recognition: The Input Layer

In a neural network designed for visual recognition, the input layer is straightforward and concrete. Each neuron in the input layer corresponds directly to a single pixel in the image. For a grayscale image, each pixel contributes a single number representing its brightness, typically on a scale from 0 to 255. For a color image, each pixel contributes three numbers — one each for the red, green, and blue channels. So a 64×64 color image produces an input layer of 64 × 64 × 3 = 12,288 values.

This one-to-one mapping — one neuron per pixel — is transparent and intuitive. The numbers in the input layer are given directly by physical reality. There is no transformation, no abstraction, no ambiguity. This simplicity makes visual recognition a useful starting point before moving to the more abstract machinery of language models.

---

## 2. Tokens and Embeddings: The LLM Input Layer

For large language models (LLMs), the input unit is not a pixel but a **token** — roughly a word or word-fragment. However, tokens cannot be fed directly into a neural network, because unlike pixel values, words have no natural numeric representation. The first layer of an LLM must therefore construct one.

This is done via an **embedding layer**. Each token is looked up in a learned table, and the result is a vector — a list of hundreds or thousands of floating-point numbers. Unlike pixel values, which are read directly from the image, these embedding vectors are **learned during training**. The network adjusts them so that tokens with similar meanings end up with similar vectors — geometrically close to each other in the high-dimensional space the vectors inhabit. So "king" and "queen" end up closer together than "king" and "bicycle."

This is a fundamental difference from visual recognition: pixel values describe physical reality directly, while embedding vectors describe semantic relationships — and the network figures out what those relationships should be through training.

---

## 3. Positional Encoding

An embedding vector captures what a token means, but not where it appears in the sequence. The word "not" means something very different at different positions in a sentence. LLMs need to encode this positional information explicitly.

For each position in the sequence, a **positional encoding vector** is computed and added element-wise to the token's embedding vector. The result is a single combined vector per token that encodes both identity and position.

The original scheme, introduced in the "Attention Is All You Need" paper, uses sine and cosine functions at different frequencies to generate the positional vectors. This has an intuitive resemblance to a Fourier decomposition: low-frequency components capture broad positional information (early versus late in the sequence), while high-frequency components capture fine-grained position (the exact slot). A useful analogy is a clock: the second hand, minute hand, and hour hand each complete their cycles at different rates, and together they encode time unambiguously. The sinusoidal positional encoding does the same thing across the dimensions of the vector.

An important property of this scheme is that it preserves information about relative distance between tokens — the network can recover not just where each token is, but how far apart any two tokens are — which is valuable for understanding grammatical and semantic relationships.

After combining embeddings and positional encodings, the result is a set of N vectors — one per token in the prompt — which serves as the starting state for the transformer.

---

## 4. The Attention Mechanism

The attention mechanism is the heart of the transformer. It allows every token to gather information from every other token in the sequence, so that each token's representation can reflect its full context.

### Queries, Keys, and Values

Each token's vector is transformed into three derived vectors through learned weight matrices:

- **Query (Q):** what this token is looking for
- **Key (K):** what this token advertises about itself
- **Value (V):** what this token will contribute if selected

These are simply linear transformations — matrix multiplications — and the Q, K, and V vectors are typically lower-dimensional than the original input vectors.

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

The first linear transformation projects each vector into a higher-dimensional space — four times larger in the original paper. This expansion provides more "analysis knobs" for the network to work with, giving it room to capture subtle distinctions in meaning that would be lost in a lower-dimensional representation.

### Why the Nonlinearity?

The nonlinearity — typically ReLU, which sets any negative value to zero — is essential. Without it, stacking linear transformations one after another is mathematically equivalent to a single linear transformation, no matter how many layers you add. The nonlinearity breaks this collapse by allowing different neurons to switch on or off depending on the input, creating piecewise behavior. This is what allows the network to represent sharp, conditional, threshold-like relationships — the kind that meaning actually involves.

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

After pre-training, models are refined through fine-tuning — using human feedback and reinforcement learning to shape the model's behavior toward being helpful, accurate, and safe. The challenge is doing this without destabilizing the vast knowledge encoded in the pre-trained weights.

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

The key insight for students is that reasoning is not a new mechanism but a clever exploitation of the existing token-by-token generation process: using the model's own output as extended context for continued computation, and optionally exploring multiple such continuations before committing to an answer.
