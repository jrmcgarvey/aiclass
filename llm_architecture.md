# How Large Language Models Work: Tokens, Embeddings, and Attention

## 1. Tokenization: Breaking Text into Pieces

When a large language model (LLM) processes text, it does not operate on raw characters or whole words. Instead, text is first converted into **tokens** — the atomic units of meaning the model works with. A tokenizer is a separate, static component sitting in front of the neural network itself, acting as a pre-processing step.

For typical LLMs using modern tokenization schemes, English text runs at roughly 3–4 characters per token, or about 1.3 tokens per word. A useful rule of thumb is that 100 tokens corresponds to approximately 75 words, and a typical page of prose contains 400–600 tokens.

Common words like "the", "is", and "a" are often represented as single tokens. Longer or rarer words get split into sub-word fragments — "tokenization" might become three or four tokens. Punctuation, whitespace, and numbers also consume tokens, often inefficiently.

---

## 2. How the Tokenizer Vocabulary is Built

The tokenizer maintains a fixed vocabulary — a dictionary of all known tokens. For modern LLMs such as Claude or GPT-4, this vocabulary contains roughly **100,000 tokens**. This vocabulary is determined once during tokenizer construction and does not change during model training or inference. It lives entirely outside the neural network itself.

The most widely used method for building this vocabulary is **Byte Pair Encoding (BPE)**, a purely statistical, algorithmic process requiring no neural network. BPE works as follows:

1. Start with individual bytes (the 256 possible values of UTF-8 encoding) as the initial vocabulary.
2. Count all adjacent pairs in a large training corpus.
3. Merge the most frequent pair into a new token.
4. Repeat until the target vocabulary size is reached.

The result is entirely data-driven — nobody decides what a token is. The training corpus decides, by frequency. Common words naturally emerge as single tokens; rare words remain as fragments. Because the process starts with raw bytes rather than characters, every possible text in any language can always be represented — the tokenizer can never fail.

At inference time, tokenization replays the learned merge rules in priority order (most frequent merges first) on new text. This is deterministic: the same input always produces the same token sequence.

---

## 3. A Multilingual Vocabulary

The tokenizer's ~100,000 token vocabulary is shared across all languages, not reserved for English alone. Languages well-represented in the training corpus (primarily English) receive efficient tokenization, with common words becoming single tokens. Languages with less training data receive less efficient coverage — words may decompose into many byte-level fragments, consuming more tokens to represent the same information.

This explains an apparent paradox: English alone might be well-served by 30,000–50,000 tokens, yet 100,000 tokens suffices for many languages combined. Several factors make this possible:

- Romance languages (Spanish, French, Italian) share vocabulary roots and word fragments, so tokens serve multiple languages.
- Scripts like Chinese and Japanese use a relatively small set of high-frequency characters that map efficiently to tokens.
- Less common languages fall back to byte-level tokenization — inefficient but functional.

The 100,000 token vocabulary is an engineering compromise. Models designed for strong multilingual coverage sometimes use larger vocabularies (Llama 3, for example, expanded to 128,000 tokens partly for this reason).

---

## 4. Embedding Vectors: Giving Tokens Meaning

Once text is tokenized, each token is mapped to an **embedding vector** — a list of floating point numbers, typically 4,096 values long for a large model. These vectors are the model's internal representation of each token.

The embedding table is a matrix of size (vocabulary_size × embedding_dimension) — for example, 100,000 × 4,096. Each row corresponds to one token. This table is initialized randomly at the start of training (typically using a Gaussian distribution) and learned during training through gradient descent.

The 4,096-dimensional length is an engineering tradeoff rather than a linguistically derived number. More dimensions provide more capacity to encode nuance but require more parameters and compute. What gets encoded in these dimensions — after training — includes semantic relationships ("dog" and "puppy" end up with similar vectors), syntactic tendencies, domain associations, and relational structure. The famous example: king − man + woman ≈ queen emerges naturally from training, not from explicit design.

It is worth noting a philosophical subtlety here. What the embeddings capture is perhaps best described as **distributional meaning** — the statistical shadow that meaning casts on language, based on patterns of use across billions of text examples. Whether this constitutes genuine semantic understanding in the philosophical sense (as Searle's Chinese Room argument questions) remains genuinely unresolved.

---

## 5. Positional Encoding

A pure embedding vector conveys what a token is, but not where it appears in the sequence. Position matters enormously — "dog bites man" and "man bites dog" contain the same tokens in different orders.

Positional information is added to each token's embedding vector before it enters the neural network. Crucially, this is not a single number appended to the vector — it is a full vector of the same dimensionality (4,096), added element-wise to the embedding:

```
input_vector = embedding_vector + positional_vector
```

Early Transformer models used sinusoidal positional encodings — fixed mathematical functions using sine and cosine waves at different frequencies across the vector dimensions, encoding fine-grained and coarse-grained position simultaneously. Later models used learned positional embeddings, where each position gets a trainable vector analogous to token embeddings.

Modern models (including likely Claude) use **RoPE — Rotary Position Embedding**. Rather than adding position to the embedding upfront, RoPE encodes position as a rotation applied inside the attention mechanism. The mathematics work out so that only the *relative distance* between tokens is captured, not their absolute positions. This is more useful in practice, since what matters is usually "how far apart are these two tokens?" rather than "what is each token's absolute index?"

---

## 6. The Attention Mechanism

After embedding and positional encoding, each token has a 4,096-dimensional vector. The attention mechanism's job is to let each token gather information from other tokens in the sequence — allowing "it" to find its antecedent, a verb to locate its subject, and so on.

To compute attention, each token's vector is linearly projected into three new vectors:

- **Q (Query):** "What am I looking for?"
- **K (Key):** "What do I contain / advertise?"
- **V (Value):** "What do I contribute if selected?"

These projections are produced by multiplying the token vector by three learned weight matrices. For each token, its Q vector is compared against every other token's K vector via a dot product, producing a scalar relevance score. These scores are normalized via softmax into weights summing to 1.0, then used to compute a weighted sum of all V vectors. The result is a new vector for each token — same dimensionality as the input — but now enriched with contextual information drawn from across the sequence.

---

## 7. Multi-Head Attention

Rather than performing attention once at full dimensionality, modern Transformers use **multi-head attention**: the attention process runs in parallel across many independent heads, typically 32–96 per layer.

The 4,096-dimensional vector is split across heads — with 64 heads, each operates in a 64-dimensional subspace. Each head independently computes Q, K, V projections and attention in its subspace. The outputs of all heads are then concatenated back to 4,096 dimensions and passed through a final linear projection that mixes the heads together.

The key benefit is that different heads can specialize in different kinds of relationships simultaneously — one head tracking coreference ("it" → "animal"), another tracking syntactic structure, another tracking semantic similarity. These specializations emerge from training rather than being explicitly programmed.

---

## 8. One Complete Transformer Layer

Multi-head attention is one half of a Transformer layer. The complete cycle for each layer is:

1. **Input:** 4,096-dimensional vector per token
2. **Layer normalization** (stabilizes training)
3. **Multi-head attention** — split, attend, concatenate, project
4. **Residual connection** — add the original input back to the attention output
5. **Layer normalization** again
6. **Feed Forward Network (FFN)** — expand 4,096 → 16,384, apply non-linearity (GeLU), compress 16,384 → 4,096
7. **Residual connection** — add the pre-FFN vector back
8. **Output:** 4,096-dimensional vector per token, refined with context

The residual connections are essential — they allow each layer to learn a *correction* to the representation rather than rewriting it entirely, and they allow gradients to flow cleanly through many layers during training.

The FFN's expanded middle layer (16,384 units) is where the closest analog to classical neurons appears — each unit computes a weighted sum of inputs and applies a non-linear activation. The attention mechanism itself is pure linear algebra (matrix multiplications), with non-linearity introduced only by the softmax over attention scores.

This entire layer is stacked 32–96 times in a large model, each pass further refining the token representations.

---

## 9. From Final Vector to Output Token

After all layers, each token position holds a 4,096-dimensional vector. To generate the next token, only the **last token's vector** is used — it encodes the model's full contextual understanding of the entire preceding sequence.

This vector is projected up to vocabulary size (100,000 dimensions) via a matrix multiplication, producing a **logit** (raw score) for every token in the vocabulary. Softmax converts these into a probability distribution — every token gets a probability, all summing to 1.0.

A token is then sampled from this distribution. The sampling strategy is controllable:
- **Greedy decoding:** always pick the highest probability token
- **Temperature sampling:** flatten or sharpen the distribution to control randomness
- **Top-k / Top-p sampling:** restrict sampling to the most probable tokens

The output projection matrix (4,096 → 100,000) is often the **transpose of the input embedding matrix** — the model enters and exits through the same representational space. The new token is appended to the sequence and the entire forward pass repeats to generate the next token.

---

## 10. Pre-Training: Learning from Text

During pre-training, the model is trained on enormous text corpora using **next-token prediction** as the objective. For each position in the training text, the model predicts the token that actually appeared next, and the difference between prediction and reality is measured by a loss function (cross-entropy).

**Gradient descent** then adjusts all the model's parameters to reduce this loss — the embedding table, the Q/K/V projection matrices, the FFN weights, the layer normalization parameters, and the output projection. This is a purely statistical process: no human labels, no explicit rules, just the model learning to predict what comes next across billions of examples.

The complete set of learned parameters for a large model includes:

- Token embedding matrix (100,000 × 4,096)
- Per layer (repeated 32–96 times):
  - Q, K, V projection matrices (4,096 × 4,096 each)
  - Output projection matrix (4,096 × 4,096)
  - Layer normalization scale (gamma) and bias (beta) vectors
  - FFN expansion matrix (4,096 × 16,384) and bias
  - FFN compression matrix (16,384 × 4,096) and bias
- Final layer normalization parameters
- Output projection matrix (often shared with the embedding table)

For a 64-layer model this amounts to tens or hundreds of billions of parameters.

---

## 11. Fine-Tuning: Aligning to Human Preferences

Pre-training produces a model that predicts text well but does not necessarily follow instructions or behave helpfully. Fine-tuning aligns the model with human preferences — but this requires evaluating entire responses rather than individual token predictions, which demands a different approach.

The dominant technique is **RLHF — Reinforcement Learning from Human Feedback**, applied in stages:

**Stage 1 — Supervised Fine Tuning (SFT):** Human writers produce examples of ideal prompt/response pairs. The model trains on these using standard next-token prediction, getting it into the right behavioral ballpark.

**Stage 2 — Reward Model Training:** Human raters compare multiple responses to the same prompt and rank them. These rankings train a separate neural network — the **reward model** — to output a scalar quality score for any prompt/response pair. The reward model learns to predict human preference.

**Stage 3 — Reinforcement Learning (PPO):** The LLM generates responses, the reward model scores them, and those scores are used as a reward signal to update the LLM via Proximal Policy Optimization. To prevent the model from drifting too far from its pre-trained state (catastrophic forgetting), a **KL divergence penalty** anchors the updated model to the original.

A simpler and increasingly popular alternative is **DPO — Direct Preference Optimization**, which skips the separate reward model and trains directly on preference pairs ("response A was preferred over response B"), achieving similar results with less complexity.

All fine-tuning adjusts the same parameters as pre-training, via gradient descent.

---

## 12. Parameter-Efficient Fine-Tuning with LoRA

Fine-tuning all parameters of a large model is computationally expensive. **LoRA — Low Rank Adaptation** offers a practical alternative:

Rather than updating a full weight matrix W (of size 4,096 × 4,096), LoRA inserts two small matrices alongside it:
- **A matrix:** 4,096 × r
- **B matrix:** r × 4,096

where r (the "rank") is a small number, typically 4–64. The original weights W are frozen; only A and B are trained. The effective weight used during the forward pass becomes W + BA.

Since r << 4,096, this is dramatically fewer parameters — perhaps 0.1–1% of the original model. LoRA is typically applied to the Q, K, V, and output projection matrices in each attention layer, and sometimes to FFN weights as well. Despite its simplicity, it captures most of the benefit of full fine-tuning at a small fraction of the compute cost.
