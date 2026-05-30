---
marp: true
theme: ai-course
paginate: false
---

<!-- _class: title -->

<div class="accent-bar"></div>
<div class="deco-panel"><div class="circle3"></div></div>

<div class="title-content">

<p class="course-label">Technical Foundations</p>

# How LLMs Work<br>Part 1: Architecture

## From raw text to a thinking machine — step by step

</div>

<div class="title-footer">Tokens &nbsp;·&nbsp; Embeddings &nbsp;·&nbsp; Position &nbsp;·&nbsp; Attention &nbsp;·&nbsp; Neurons & Layers</div>

---

<!-- _class: overview-grid -->

<div class="header-label">Artificial Intelligence for Lay People &nbsp;·&nbsp; Week N</div>

## Session Overview
# What We'll Cover Today

<div class="grid-container">
  <div class="grid-card">
    <div class="grid-number">1</div>
    <div class="grid-text">
      <div class="grid-title">Tokens</div>
      <div class="grid-subtitle">How text is broken into manageable pieces</div>
    </div>
  </div>
  <div class="grid-card">
    <div class="grid-number">2</div>
    <div class="grid-text">
      <div class="grid-title">Embeddings</div>
      <div class="grid-subtitle">Giving words a location in meaning-space</div>
    </div>
  </div>
  <div class="grid-card">
    <div class="grid-number">3</div>
    <div class="grid-text">
      <div class="grid-title">Position</div>
      <div class="grid-subtitle">Why word order matters, and how it is encoded</div>
    </div>
  </div>
  <div class="grid-card">
    <div class="grid-number">4</div>
    <div class="grid-text">
      <div class="grid-title">Attention</div>
      <div class="grid-subtitle">How words notice and influence each other</div>
    </div>
  </div>
  <div class="grid-card">
    <div class="grid-number">5</div>
    <div class="grid-text">
      <div class="grid-title">Neurons & Layers</div>
      <div class="grid-subtitle">The neural network machinery underneath</div>
    </div>
  </div>
  <div class="grid-card">
    <div class="grid-number" style="background:var(--card-bg);color:var(--muted);">→</div>
    <div class="grid-text">
      <div class="grid-title" style="color:var(--muted);">Next Session</div>
      <div class="grid-subtitle">Training · Gradient Descent · Fine-Tuning · Inference</div>
    </div>
  </div>
</div>

<footer>Artificial Intelligence for Lay People &nbsp;·&nbsp; Week N</footer>

---

<!-- _class: content technical -->

<div class="header-label">Artificial Intelligence for Lay People &nbsp;·&nbsp; Week N</div>

## Tokens
# The Goldilocks Problem

**Whole Words — Too many**
Hundreds of thousands of words in English alone — plus slang, technical terms, new coinages. An unmanageably large dictionary.

**Tokens — Just right**
50,000–100,000 chunks covering virtually any text. Common words get one token. Rare words split into meaningful pieces.

**Single Letters — Too few**
Letters carry almost no meaning alone. The letter 'b' tells you nothing. Processing letter-by-letter loses all structure.

<footer>Artificial Intelligence for Lay People &nbsp;·&nbsp; Week N</footer>

---

<!-- _class: content technical -->

<div class="header-label">Artificial Intelligence for Lay People &nbsp;·&nbsp; Week N</div>

## Tokens
# What Tokens Look Like — and a Surprising Side Effect

**Sample tokens from a typical model:**

`the` &nbsp; `cat` &nbsp; `sat` &nbsp; `on` &nbsp; `un` &nbsp; `believ` &nbsp; `able` &nbsp; `ing` &nbsp; `pre` &nbsp; `John` &nbsp; `!` &nbsp; `2024`

<small>■ Whole words &nbsp;&nbsp; ■ Sub-word fragments &nbsp;&nbsp; ■ Names &nbsp;&nbsp; ■ Other</small>

---

**A surprising side effect — How many r's in *strawberry*?**

The model never sees individual letters. It sees tokens: `straw` + `berry`

To count letters, the model must reason about what is *inside* each token — indirectly. It often gets it wrong.

<div class="callout">Each token is assigned a unique ID number. From here on, the model works entirely with numbers.</div>

<footer>Artificial Intelligence for Lay People &nbsp;·&nbsp; Week N</footer>

---

<!-- _class: content technical -->

<div class="header-label">Artificial Intelligence for Lay People &nbsp;·&nbsp; Week N</div>

## Embeddings
# Giving Words a Location in Meaning-Space

**The idea** — Each token is placed at a location in a mathematical space — like a map. Words with similar meanings end up near each other:

- *cat* and *kitten* are neighbors
- *king* and *queen* are neighbors
- *cat* and *nuclear reactor* are far apart

**Why this matters** — The geometry of the space encodes relationships. The model doesn't just know that words exist — it knows how they *relate* to each other, by how close or far apart they are in this space.

**The map starts random** — At the start of training, every token is placed at a random location drawn from a bell-curve distribution centered on zero. At this point, *cat* and *nuclear reactor* are equally likely to be neighbors. Pure chance.

Training on trillions of words gradually moves every token to where it belongs — until the geometry reflects the structure of language.

<footer>Artificial Intelligence for Lay People &nbsp;·&nbsp; Week N</footer>

---

<!-- _class: content technical -->

<div class="header-label">Artificial Intelligence for Lay People &nbsp;·&nbsp; Week N</div>

## Embeddings
# From Two Dimensions to Thousands

A real map has 2 dimensions. An embedding space has thousands. Each additional dimension is another axis along which tokens can be similar or different — capturing grammar, formality, emotional tone, subject matter, and properties we don't even have names for.

| Model size | Dimensions |
|---|---|
| Small model | 768 |
| Medium model | 1,536 |
| Large model | 4,096+ |

**Key insight** — Each token's location is stored as a list of numbers — one per dimension. A large model might store each token as a list of 4,096 numbers. This list is called the token's **embedding vector**.

By the end of training, the geometry of this space encodes a remarkable amount of human knowledge about language and meaning.

<footer>Artificial Intelligence for Lay People &nbsp;·&nbsp; Week N</footer>

---

<!-- _class: content technical -->

<div class="header-label">Artificial Intelligence for Lay People &nbsp;·&nbsp; Week N</div>

## Position
# Word Order Matters — and the Model Needs to Be Told

**The problem** — The model processes all tokens simultaneously. It has no built-in sense of order.

> *The dog chased the boy.*
> *The boy chased the dog.*

Same tokens. Completely different meaning.

**The solution** — Each token gets a second vector — a *position tag* — added to its embedding. Position 1's tag is always the same regardless of which word sits there. The combined vector carries both *what the word means* and *where it sits* in the sentence.

**Meaning + position = a unique combined vector.** The two instances of "the" in a sentence now have *different* combined vectors — because they sit in different positions. The model can tell them apart.

<footer>Artificial Intelligence for Lay People &nbsp;·&nbsp; Week N</footer>

---

<!-- _class: content technical -->

<div class="header-label">Artificial Intelligence for Lay People &nbsp;·&nbsp; Week N</div>

## Attention
# Every Word Gets to Ask: How Relevant Are You to Me?

**How attention works** — Every token looks at every other token in the sentence and asks: *how relevant are you to me?* The answers are collected and used to build a richer, context-aware representation of each token.

**Example: *"The bank of the river was steep."***

The word *bank* looks across the sentence and finds *river* highly relevant. This shifts its meaning away from finance and toward geography. Without attention, *bank* would carry its most common meaning regardless of context.

> Thick connection = strong attention &nbsp;·&nbsp; Thin connection = weak attention
>
> *"bank"* pays strong attention to *"river"* — resolving the ambiguity.

**The key insight** — Attention is not fixed. It is *computed fresh* for every sentence. The same word pays attention to different neighbors depending on what surrounds it.

<footer>Artificial Intelligence for Lay People &nbsp;·&nbsp; Week N</footer>

---

<!-- _class: content technical -->

<div class="header-label">Artificial Intelligence for Lay People &nbsp;·&nbsp; Week N</div>

## Attention
# Multiple Attention Heads — Looking for Different Relationships

Rather than one attention pass, the model runs several in parallel — each learning to notice different kinds of relationships.

**Head 1 — Grammatical relationships**
Which word is the subject? Which is the object? How do verb tenses relate?

**Head 2 — Semantic relationships**
Which words share a topic or domain? What is this passage about?

**Head 3 — Reference tracking**
When the text says "it" — what does it refer to? Connecting pronouns to nouns across distance.

The outputs of all heads are combined into a single **rich, context-aware token vector** — carrying grammatical role, semantic meaning, and referential links simultaneously.

<div class="callout">Large models run 32 to 128 attention heads per layer — each discovering its own type of relationship in the data.</div>

<footer>Artificial Intelligence for Lay People &nbsp;·&nbsp; Week N</footer>

---

<!-- _class: content technical -->

<div class="header-label">Artificial Intelligence for Lay People &nbsp;·&nbsp; Week N</div>

## Neurons & Layers
# The Neural Network Machinery

**What is a neuron?** A neuron is a very simple computing unit:

1. Receives numbers as input
2. Multiplies each by a **weight** — its importance score
3. Adds the results together
4. Passes the sum through an **activation function** — enabling complex pattern learning

The connections between neurons *are* the weights — the parameters adjusted during training. A large model has **hundreds of billions** of these weights.

**What is a layer?** Every layer contains two steps in sequence:

1. *Attention* — tokens look at each other and gather context
2. *Feed-Forward Network* — each token is processed individually through a small neural network

Between steps, **Layer Normalization** keeps the numbers stable and prevents runaway growth.

<footer>Artificial Intelligence for Lay People &nbsp;·&nbsp; Week N</footer>

---

<!-- _class: content technical -->

<div class="header-label">Artificial Intelligence for Lay People &nbsp;·&nbsp; Week N</div>

## Neurons & Layers
# Layers of Processing — Stacked Deep

**How deep?** Large models have 96 or more layers. Each layer adds another round of refinement. By the final layer, each token's vector carries a remarkably rich representation of its meaning in context.

| Layer | What happens |
|---|---|
| Layer 1 | Basic pattern recognition — punctuation, common phrases |
| Layer 2–10 | Grammatical structure begins to emerge |
| Layer 10–50 | Semantic relationships, topic, tone |
| Layer 50–96+ | Abstract reasoning, long-range dependencies, nuance |

**The key insight** — No single layer "understands" anything. Understanding — if we can call it that — emerges from the *accumulated refinement* of many simple operations stacked on top of each other.

<div class="callout">The model has no explicit rules. Everything it knows about language is encoded in the geometry of the embedding space and the values of the weights — learned from data alone.</div>

<footer>Artificial Intelligence for Lay People &nbsp;·&nbsp; Week N</footer>

---

<!-- _class: content technical -->

<div class="header-label">Artificial Intelligence for Lay People &nbsp;·&nbsp; Week N</div>

## Summary
# What We Have Built — and What Comes Next

The pipeline so far:

| Stage | What it does |
|---|---|
| **Text** | Raw input — characters and words |
| **Tokens** | Text split into numbered chunks (50k–100k vocabulary) |
| **Embeddings** | Each token placed in high-dimensional meaning-space |
| **Position** | Order encoded — meaning + location combined |
| **Attention** | Every token gathers context from every other token |
| **Layers** | 96+ rounds of attention + feed-forward refinement |

**The machine now exists** — but it is full of random numbers and cannot do anything useful yet.

*Next session:* **How the model learns** — Training, Gradient Descent, Fine-Tuning, and Inference.

> We have built the machine. Next time we fill it with knowledge.

<footer>Artificial Intelligence for Lay People &nbsp;·&nbsp; Week N</footer>

---

<!-- _class: closing -->

<div class="accent-bar"></div>
<div class="deco-panel"></div>

<div class="closing-content">

<p class="course-label">Technical Foundations</p>

# See you next session.

## Next time: Training, Gradient Descent, Fine-Tuning, and Inference

<p class="muted">How does the machine learn? How does it generate a response? We will find out.</p>

</div>

<div class="closing-footer">Tokens &nbsp;·&nbsp; Embeddings &nbsp;·&nbsp; Position &nbsp;·&nbsp; Attention &nbsp;·&nbsp; Neurons & Layers</div>
