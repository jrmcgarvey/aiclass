---
marp: true
theme: ai-course
paginate: false
html: true
---

<!-- _class: title -->
<div class="accent-bar"></div>
<div class="deco-panel"><span class="circle3"></span></div>
<div class="title-content">

# How AI Systems Work

## From Biology to Large Language Models

<br>

<span class="muted">Class sessions 4 and 5. Technical, but not too bad.</span>

</div>
<div class="title-footer">UNDERSTANDING ARTIFICIAL INTELLIGENCE</div>

---

<!-- _class: overview-grid -->
<div class="header-label">COURSE OVERVIEW</div>
<div class="grid-container">
  <div class="grid-card">
    <div class="grid-number" style="background:var(--cat-technical)">1</div>
    <div class="grid-text">
      <div class="grid-title">Basic Concepts</div>
      <div class="grid-subtitle">Weights, layers, gradient descent</div>
    </div>
  </div>
  <div class="grid-card">
    <div class="grid-number" style="background:var(--cat-technical)">2</div>
    <div class="grid-text">
      <div class="grid-title">Visual Recognition</div>
      <div class="grid-subtitle">From cat neurons to AlexNet</div>
    </div>
  </div>
  <div class="grid-card">
    <div class="grid-number" style="background:var(--cat-progress)">3</div>
    <div class="grid-text">
      <div class="grid-title">Large Language Models</div>
      <div class="grid-subtitle">Transformers, attention, training</div>
    </div>
  </div>
  <div class="grid-card">
    <div class="grid-number" style="background:var(--cat-progress)">4</div>
    <div class="grid-text">
      <div class="grid-title">A Taxonomy</div>
      <div class="grid-subtitle">The neural network family tree</div>
    </div>
  </div>
  <div class="grid-card">
    <div class="grid-number" style="background:var(--cat-alignment)">5</div>
    <div class="grid-text">
      <div class="grid-title">Image Generation</div>
      <div class="grid-subtitle">Diffusion models &amp; novel images</div>
    </div>
  </div>
  <div class="grid-card">
    <div class="grid-number" style="background:var(--cat-social)">6</div>
    <div class="grid-text">
      <div class="grid-title">Self-Driving Cars</div>
      <div class="grid-subtitle">Waymo, Tesla, the full stack</div>
    </div>
  </div>
</div>

---

<!-- _class: divider technical -->
<div class="divider-content">

# 1

<div class="rule"></div>

## Basic Neural Network Concepts

<span class="reading-label">Session One</span>
</div>

---

<!-- _class: technical -->
<div class="header-label">BASIC CONCEPTS</div>

## 1.1 Forward Propagation

- Input is a collection of **vectors** — ordered lists of numbers
  - Image → RGB values per pixel
  - Text → numbers assigned to each word or word-fragment
- Each layer applies a **matrix multiplication**, combining information across inputs
- Then an **activation function** — introduces nonlinearity so complex patterns can be learned
- Result is passed to the next layer; repeat

<div class="callout"><strong>Key idea:</strong> data flows forward, layer by layer, each layer building a richer representation of the input.</div>

---

<!-- _class: technical -->
<div class="header-label">BASIC CONCEPTS</div>

## 1.1 What Are Weights?

- Every number in every matrix is a **weight** — a parameter of the model
- At the start of training: **randomly assigned**
- A large language model may have **hundreds of billions** of weights
- Training's entire job: find better values for all of them

<br>

<svg viewBox="0 0 820 200" xmlns="http://www.w3.org/2000/svg" style="width:100%;max-height:190px">
  <!-- Input nodes -->
  <circle cx="80" cy="60" r="22" fill="#2A3247" stroke="#4EC9C0" stroke-width="2"/>
  <circle cx="80" cy="120" r="22" fill="#2A3247" stroke="#4EC9C0" stroke-width="2"/>
  <circle cx="80" cy="180" r="22" fill="#2A3247" stroke="#4EC9C0" stroke-width="2"/>
  <!-- Hidden layer 1 -->
  <circle cx="260" cy="45" r="22" fill="#2A3247" stroke="#5CB85C" stroke-width="2"/>
  <circle cx="260" cy="105" r="22" fill="#2A3247" stroke="#5CB85C" stroke-width="2"/>
  <circle cx="260" cy="165" r="22" fill="#2A3247" stroke="#5CB85C" stroke-width="2"/>
  <!-- Hidden layer 2 -->
  <circle cx="440" cy="45" r="22" fill="#2A3247" stroke="#5CB85C" stroke-width="2"/>
  <circle cx="440" cy="105" r="22" fill="#2A3247" stroke="#5CB85C" stroke-width="2"/>
  <circle cx="440" cy="165" r="22" fill="#2A3247" stroke="#5CB85C" stroke-width="2"/>
  <!-- Output nodes -->
  <circle cx="620" cy="80" r="22" fill="#2A3247" stroke="#F0A500" stroke-width="2"/>
  <circle cx="620" cy="150" r="22" fill="#2A3247" stroke="#F0A500" stroke-width="2"/>
  <!-- Connections input->h1 (sample) -->
  <line x1="102" y1="65" x2="238" y2="50" stroke="#4EC9C0" stroke-width="1" stroke-opacity="0.4"/>
  <line x1="102" y1="70" x2="238" y2="108" stroke="#4EC9C0" stroke-width="1" stroke-opacity="0.4"/>
  <line x1="102" y1="120" x2="238" y2="48" stroke="#4EC9C0" stroke-width="1" stroke-opacity="0.4"/>
  <line x1="102" y1="122" x2="238" y2="107" stroke="#4EC9C0" stroke-width="1" stroke-opacity="0.4"/>
  <line x1="102" y1="124" x2="238" y2="163" stroke="#4EC9C0" stroke-width="1" stroke-opacity="0.4"/>
  <line x1="102" y1="178" x2="238" y2="108" stroke="#4EC9C0" stroke-width="1" stroke-opacity="0.4"/>
  <line x1="102" y1="180" x2="238" y2="164" stroke="#4EC9C0" stroke-width="1" stroke-opacity="0.4"/>
  <!-- Connections h1->h2 -->
  <line x1="282" y1="48" x2="418" y2="48" stroke="#5CB85C" stroke-width="1" stroke-opacity="0.4"/>
  <line x1="282" y1="52" x2="418" y2="108" stroke="#5CB85C" stroke-width="1" stroke-opacity="0.4"/>
  <line x1="282" y1="107" x2="418" y2="48" stroke="#5CB85C" stroke-width="1" stroke-opacity="0.4"/>
  <line x1="282" y1="108" x2="418" y2="107" stroke="#5CB85C" stroke-width="1" stroke-opacity="0.4"/>
  <line x1="282" y1="110" x2="418" y2="164" stroke="#5CB85C" stroke-width="1" stroke-opacity="0.4"/>
  <line x1="282" y1="164" x2="418" y2="107" stroke="#5CB85C" stroke-width="1" stroke-opacity="0.4"/>
  <line x1="282" y1="166" x2="418" y2="164" stroke="#5CB85C" stroke-width="1" stroke-opacity="0.4"/>
  <!-- Connections h2->output -->
  <line x1="462" y1="48" x2="598" y2="82" stroke="#F0A500" stroke-width="1" stroke-opacity="0.4"/>
  <line x1="462" y1="107" x2="598" y2="84" stroke="#F0A500" stroke-width="1" stroke-opacity="0.4"/>
  <line x1="462" y1="109" x2="598" y2="150" stroke="#F0A500" stroke-width="1" stroke-opacity="0.4"/>
  <line x1="462" y1="164" x2="598" y2="148" stroke="#F0A500" stroke-width="1" stroke-opacity="0.4"/>
  <!-- Labels -->
  <text x="80" y="198" text-anchor="middle" fill="#8D96A8" font-size="13" font-family="Calibri,sans-serif">Input</text>
  <text x="260" y="198" text-anchor="middle" fill="#8D96A8" font-size="13" font-family="Calibri,sans-serif">Hidden 1</text>
  <text x="440" y="198" text-anchor="middle" fill="#8D96A8" font-size="13" font-family="Calibri,sans-serif">Hidden 2</text>
  <text x="620" y="198" text-anchor="middle" fill="#8D96A8" font-size="13" font-family="Calibri,sans-serif">Output</text>
  <!-- Weight label -->
  <text x="170" y="28" text-anchor="middle" fill="#4EC9C0" font-size="13" font-family="Calibri,sans-serif" font-style="italic">← each line is a weight →</text>
  <!-- Arrow -->
  <text x="730" y="115" text-anchor="middle" fill="#F0A500" font-size="28" font-family="Calibri,sans-serif">🐱 93%</text>
</svg>

---

<!-- _class: technical -->
<div class="header-label">BASIC CONCEPTS</div>

## 1.2 The Output Layer

- All layers feed into a set of **logits** — one raw score per possible category
- A **softmax function** converts logits to probabilities that sum to 100%
- The model commits to its best guess — and a confidence level

<br>

> ⚠️ Softmax always picks *something*. Show the model a penguin when it only knows cats, dogs, and cars — it will still return a confident (wrong) answer.

---

<!-- _class: technical -->
<div class="header-label">BASIC CONCEPTS</div>

## 1.3 The Loss Function

- During training, the model is often **wrong**
- The **loss function** measures how wrong, across a batch of examples
- **Supervised learning** (images): compare output to human-labeled correct answer
- **Self-supervised learning** (LLMs): the text itself supplies the answer — predict the next word, check against what actually came next
  - No human labeling needed
  - Billions of checkable predictions per training run

---

<!-- _class: technical -->
<div class="header-label">BASIC CONCEPTS</div>

## 1.4 Gradient Descent — The Landscape

Imagine a mountain range. You are blindfolded. Goal: find the lowest valley.

- Feel the slope under your feet
- Step in the most downhill direction
- Repeat

**This is gradient descent.** Height = loss. Slope = gradient.

<svg viewBox="0 0 780 200" xmlns="http://www.w3.org/2000/svg" style="width:100%;max-height:185px;display:block;margin:0 auto">
  <!-- Background -->
  <rect width="780" height="200" fill="#1A1F2E" rx="6"/>
  <!-- Mountain terrain path -->
  <path d="M0,180 C40,178 60,170 90,130 C110,105 125,95 150,80 C170,68 185,65 200,85
           C215,100 225,115 245,100 C265,85 280,50 310,30 C330,18 345,15 365,35
           C380,50 390,70 410,85 C430,98 445,92 465,75
           C480,62 490,55 510,70 C530,85 545,105 565,120
           C585,135 600,140 625,125 C645,112 660,100 685,115
           C705,128 720,150 750,160 C765,165 775,168 780,170
           L780,200 L0,200 Z"
        fill="#2A3247" stroke="#4EC9C0" stroke-width="1.5"/>
  <!-- Highlight the deepest valley -->
  <circle cx="310" cy="30" r="7" fill="#F0A500" stroke="#F0A500" stroke-width="2"/>
  <text x="310" y="20" text-anchor="middle" fill="#F0A500" font-size="11" font-family="Calibri,sans-serif">global min</text>
  <!-- A local valley -->
  <circle cx="465" cy="75" r="6" fill="#4EC9C0" stroke="#4EC9C0" stroke-width="2"/>
  <text x="500" y="68" fill="#4EC9C0" font-size="11" font-family="Calibri,sans-serif">good enough</text>
  <!-- Descent arrow -->
  <path d="M200,85 C215,82 230,78 245,72 C258,67 272,55 290,42" stroke="#E8EDF5" stroke-width="2" fill="none" stroke-dasharray="5,3"/>
  <polygon points="290,42 282,52 298,50" fill="#E8EDF5"/>
  <!-- Blindfolded figure -->
  <circle cx="200" cy="78" r="9" fill="#8D96A8"/>
  <line x1="196" y1="76" x2="204" y2="76" stroke="#1A1F2E" stroke-width="2"/>
  <!-- Axis label -->
  <text x="390" y="195" text-anchor="middle" fill="#8D96A8" font-size="12" font-family="Calibri,sans-serif">← one dimension of billions →</text>
</svg>

---

<!-- _class: technical -->
<div class="header-label">BASIC CONCEPTS</div>

## 1.4 Gradient Descent — Key Points

- The loss landscape has **billions of dimensions** — one per weight
- A real model finds *a* good valley, rarely the single best one
- Many different valleys give models of similar quality
- Step size = **learning rate** — too large and you overshoot

<br>

**Backpropagation** computes the gradient:
- Uses the chain rule from calculus
- Sends the error signal *backward* through each layer
- Determines each weight's contribution to the loss
- ~2× more expensive than the forward pass

---

<!-- _class: technical -->
<div class="header-label">BASIC CONCEPTS</div>

## 1.5 Why Nvidia?

- Neural network training = enormous numbers of **matrix multiplications**, done in parallel
- GPUs were built for video games — parallelism is their whole design
- CPUs can do the same math, but one operation at a time
- AI training turned out to need *exactly* what GPUs provide
- Training a frontier LLM: thousands of GPUs, months of runtime, hundreds of millions of dollars

<div class="callout">Nvidia built a great gaming business. Then AI arrived at a different scale entirely.</div>

---

<!-- _class: divider technical -->
<div class="divider-content">

# 2

<div class="rule"></div>

## Neural Networks for Visual Recognition

<span class="reading-label">Session One</span>
</div>

---

<!-- _class: technical -->
<div class="header-label">VISUAL RECOGNITION</div>

## 2.1 Hubel & Wiesel — The Cat Experiments

- Harvard Medical School, late 1950s
- Recorded signals from individual neurons in anesthetized cats' visual cortex
- **Nobel Prize in Physiology or Medicine, 1981**

**The accidental discovery:**
Projecting a dot of light → neurons didn't care. The *edge* of a glass slide moving at a particular angle → one neuron fired dramatically.

**Finding:** cortical neurons respond to **oriented edges**, not spots of light — and only at the right position and angle.

---

<!-- _class: technical -->
<div class="header-label">VISUAL RECOGNITION</div>

## 2.1 Simple Cells and Complex Cells

<div style="display:grid;grid-template-columns:1fr 1fr;gap:24px;margin-top:8px">
<div>

**Simple cells**
- Respond to an edge at a *specific orientation* AND *specific location*
- Move the edge → cell goes silent
- Like a very precise local detector

</div>
<div>

**Complex cells**
- Also prefer a specific orientation
- But respond wherever that edge appears in a broader region
- Trade positional precision for location tolerance

</div>
</div>

<div class="callout">This two-level hierarchy — precise detectors feeding tolerant ones — became the blueprint for convolutional neural networks.</div>

---

<!-- _class: technical -->
<div class="header-label">VISUAL RECOGNITION</div>

## 2.2 Channels and Layers

<svg viewBox="0 0 820 230" xmlns="http://www.w3.org/2000/svg" style="width:100%;max-height:220px">
  <!-- Stage 1: Input image -->
  <rect x="10" y="40" width="80" height="80" rx="4" fill="#2A3247" stroke="#4EC9C0" stroke-width="1.5"/>
  <text x="50" y="85" text-anchor="middle" fill="#4EC9C0" font-size="11" font-family="Calibri,sans-serif">Image</text>
  <text x="50" y="138" text-anchor="middle" fill="#8D96A8" font-size="11" font-family="Calibri,sans-serif">3 channels</text>
  <text x="50" y="152" text-anchor="middle" fill="#8D96A8" font-size="10" font-family="Calibri,sans-serif">(R, G, B)</text>
  <!-- Arrow -->
  <polygon points="102,80 94,75 94,85" fill="#E8EDF5"/>
  <line x1="90" y1="80" x2="103" y2="80" stroke="#E8EDF5" stroke-width="1.5"/>
  <!-- Filter icon -->
  <rect x="108" y="58" width="44" height="44" rx="3" fill="#1A1F2E" stroke="#5CB85C" stroke-width="1.5"/>
  <line x1="108" y1="72.7" x2="152" y2="72.7" stroke="#5CB85C" stroke-width="0.8" stroke-opacity="0.5"/>
  <line x1="108" y1="87.3" x2="152" y2="87.3" stroke="#5CB85C" stroke-width="0.8" stroke-opacity="0.5"/>
  <line x1="122.7" y1="58" x2="122.7" y2="102" stroke="#5CB85C" stroke-width="0.8" stroke-opacity="0.5"/>
  <line x1="137.3" y1="58" x2="137.3" y2="102" stroke="#5CB85C" stroke-width="0.8" stroke-opacity="0.5"/>
  <text x="130" y="118" text-anchor="middle" fill="#5CB85C" font-size="10" font-family="Calibri,sans-serif">3×3 filter</text>
  <text x="130" y="130" text-anchor="middle" fill="#5CB85C" font-size="10" font-family="Calibri,sans-serif">(slides across)</text>
  <!-- Arrow -->
  <polygon points="165,80 157,75 157,85" fill="#E8EDF5"/>
  <line x1="152" y1="80" x2="166" y2="80" stroke="#E8EDF5" stroke-width="1.5"/>
  <!-- Layer 1 output -->
  <rect x="168" y="25" width="60" height="110" rx="4" fill="#2A3247" stroke="#5CB85C" stroke-width="1.5"/>
  <text x="198" y="88" text-anchor="middle" fill="#5CB85C" font-size="11" font-family="Calibri,sans-serif">64</text>
  <text x="198" y="102" text-anchor="middle" fill="#5CB85C" font-size="11" font-family="Calibri,sans-serif">channels</text>
  <text x="198" y="148" text-anchor="middle" fill="#8D96A8" font-size="10" font-family="Calibri,sans-serif">edges, colors</text>
  <!-- Arrow -->
  <polygon points="242,80 234,75 234,85" fill="#E8EDF5"/>
  <line x1="228" y1="80" x2="243" y2="80" stroke="#E8EDF5" stroke-width="1.5"/>
  <text x="255" y="76" text-anchor="middle" fill="#8D96A8" font-size="9" font-family="Calibri,sans-serif">pool</text>
  <text x="255" y="88" text-anchor="middle" fill="#8D96A8" font-size="9" font-family="Calibri,sans-serif">↓ size</text>
  <polygon points="268,80 260,75 260,85" fill="#E8EDF5"/>
  <line x1="255" y1="80" x2="269" y2="80" stroke="#E8EDF5" stroke-width="1.5"/>
  <!-- Layer 2 output -->
  <rect x="272" y="15" width="60" height="130" rx="4" fill="#2A3247" stroke="#5CB85C" stroke-width="1.5"/>
  <text x="302" y="85" text-anchor="middle" fill="#5CB85C" font-size="11" font-family="Calibri,sans-serif">128</text>
  <text x="302" y="99" text-anchor="middle" fill="#5CB85C" font-size="11" font-family="Calibri,sans-serif">channels</text>
  <text x="302" y="160" text-anchor="middle" fill="#8D96A8" font-size="10" font-family="Calibri,sans-serif">corners, curves</text>
  <!-- Arrow -->
  <polygon points="346,80 338,75 338,85" fill="#E8EDF5"/>
  <line x1="332" y1="80" x2="347" y2="80" stroke="#E8EDF5" stroke-width="1.5"/>
  <text x="358" y="76" text-anchor="middle" fill="#8D96A8" font-size="9" font-family="Calibri,sans-serif">pool</text>
  <text x="358" y="88" text-anchor="middle" fill="#8D96A8" font-size="9" font-family="Calibri,sans-serif">↓ size</text>
  <polygon points="370,80 362,75 362,85" fill="#E8EDF5"/>
  <line x1="358" y1="80" x2="371" y2="80" stroke="#E8EDF5" stroke-width="1.5"/>
  <!-- Layer 3 output -->
  <rect x="374" y="5" width="60" height="150" rx="4" fill="#2A3247" stroke="#5CB85C" stroke-width="1.5"/>
  <text x="404" y="82" text-anchor="middle" fill="#5CB85C" font-size="11" font-family="Calibri,sans-serif">256</text>
  <text x="404" y="96" text-anchor="middle" fill="#5CB85C" font-size="11" font-family="Calibri,sans-serif">channels</text>
  <text x="404" y="170" text-anchor="middle" fill="#8D96A8" font-size="10" font-family="Calibri,sans-serif">shapes, textures</text>
  <!-- Arrow -->
  <polygon points="448,80 440,75 440,85" fill="#E8EDF5"/>
  <line x1="434" y1="80" x2="449" y2="80" stroke="#E8EDF5" stroke-width="1.5"/>
  <!-- Final layer -->
  <rect x="452" y="35" width="60" height="90" rx="4" fill="#2A3247" stroke="#F0A500" stroke-width="1.5"/>
  <text x="482" y="82" text-anchor="middle" fill="#F0A500" font-size="11" font-family="Calibri,sans-serif">deep</text>
  <text x="482" y="96" text-anchor="middle" fill="#F0A500" font-size="11" font-family="Calibri,sans-serif">features</text>
  <text x="482" y="140" text-anchor="middle" fill="#8D96A8" font-size="10" font-family="Calibri,sans-serif">eyes, wheels...</text>
  <!-- Arrow to output -->
  <polygon points="526,80 518,75 518,85" fill="#E8EDF5"/>
  <line x1="512" y1="80" x2="527" y2="80" stroke="#E8EDF5" stroke-width="1.5"/>
  <!-- Output probabilities -->
  <rect x="530" y="30" width="140" height="100" rx="4" fill="#1A1F2E" stroke="#F0A500" stroke-width="1"/>
  <text x="600" y="52" text-anchor="middle" fill="#8D96A8" font-size="11" font-family="Calibri,sans-serif">cat</text>
  <rect x="548" y="58" width="104" height="10" rx="2" fill="#F0A500"/>
  <text x="658" y="68" fill="#F0A500" font-size="11" font-family="Calibri,sans-serif">93%</text>
  <text x="600" y="88" text-anchor="middle" fill="#8D96A8" font-size="11" font-family="Calibri,sans-serif">dog</text>
  <rect x="548" y="94" width="18" height="10" rx="2" fill="#8D96A8"/>
  <text x="572" y="104" fill="#8D96A8" font-size="11" font-family="Calibri,sans-serif">5%</text>
  <text x="600" y="118" text-anchor="middle" fill="#8D96A8" font-size="11" font-family="Calibri,sans-serif">car</text>
  <rect x="548" y="124" width="8" height="10" rx="2" fill="#8D96A8"/>
  <text x="562" y="134" fill="#8D96A8" font-size="11" font-family="Calibri,sans-serif">2%</text>
  <!-- Title annotation -->
  <text x="300" y="215" text-anchor="middle" fill="#8D96A8" font-size="12" font-family="Calibri,sans-serif">More channels, smaller spatial size — richer representation at each layer</text>
</svg>

---

<!-- _class: technical -->
<div class="header-label">VISUAL RECOGNITION</div>

## 2.3 The Convolution Idea

**The problem with fully-connected networks on images:**
- 200×200 image = 40,000 pixels
- Connect every pixel to 1,000 neurons → **40 million parameters** in layer one
- Wasteful: a horizontal edge is *local* — defined by a few neighboring pixels, not all of them

**The solution — convolutional filters:**
- A small grid of weights (e.g. 3×3 = just 9 numbers)
- **Slides across the entire image** — same weights, every position
- Detects the same feature wherever it appears → **weight sharing**

<div class="callout">This is the computational equivalent of Hubel & Wiesel's simple cells: local, position-sensitive detectors.</div>

---

<!-- _class: technical -->
<div class="header-label">VISUAL RECOGNITION</div>

## 2.3 A Filter in Action

<svg viewBox="0 0 780 240" xmlns="http://www.w3.org/2000/svg" style="width:100%;max-height:225px">
  <!-- Image grid (8x6) -->
  <g transform="translate(20,20)">
    <!-- Dark rows (top) -->
    <rect x="0" y="0" width="30" height="30" fill="#1A1F2E" stroke="#3A4255" stroke-width="0.5"/>
    <rect x="30" y="0" width="30" height="30" fill="#1A1F2E" stroke="#3A4255" stroke-width="0.5"/>
    <rect x="60" y="0" width="30" height="30" fill="#1A1F2E" stroke="#3A4255" stroke-width="0.5"/>
    <rect x="90" y="0" width="30" height="30" fill="#1A1F2E" stroke="#3A4255" stroke-width="0.5"/>
    <rect x="120" y="0" width="30" height="30" fill="#1A1F2E" stroke="#3A4255" stroke-width="0.5"/>
    <rect x="0" y="30" width="30" height="30" fill="#1A1F2E" stroke="#3A4255" stroke-width="0.5"/>
    <rect x="30" y="30" width="30" height="30" fill="#1A1F2E" stroke="#3A4255" stroke-width="0.5"/>
    <rect x="60" y="30" width="30" height="30" fill="#1A1F2E" stroke="#3A4255" stroke-width="0.5"/>
    <rect x="90" y="30" width="30" height="30" fill="#1A1F2E" stroke="#3A4255" stroke-width="0.5"/>
    <rect x="120" y="30" width="30" height="30" fill="#1A1F2E" stroke="#3A4255" stroke-width="0.5"/>
    <!-- Transition row -->
    <rect x="0" y="60" width="30" height="30" fill="#2A3247" stroke="#3A4255" stroke-width="0.5"/>
    <rect x="30" y="60" width="30" height="30" fill="#2A3247" stroke="#3A4255" stroke-width="0.5"/>
    <rect x="60" y="60" width="30" height="30" fill="#2A3247" stroke="#3A4255" stroke-width="0.5"/>
    <rect x="90" y="60" width="30" height="30" fill="#2A3247" stroke="#3A4255" stroke-width="0.5"/>
    <rect x="120" y="60" width="30" height="30" fill="#2A3247" stroke="#3A4255" stroke-width="0.5"/>
    <!-- Light rows (bottom) -->
    <rect x="0" y="90" width="30" height="30" fill="#8D96A8" stroke="#3A4255" stroke-width="0.5"/>
    <rect x="30" y="90" width="30" height="30" fill="#8D96A8" stroke="#3A4255" stroke-width="0.5"/>
    <rect x="60" y="90" width="30" height="30" fill="#8D96A8" stroke="#3A4255" stroke-width="0.5"/>
    <rect x="90" y="90" width="30" height="30" fill="#8D96A8" stroke="#3A4255" stroke-width="0.5"/>
    <rect x="120" y="90" width="30" height="30" fill="#8D96A8" stroke="#3A4255" stroke-width="0.5"/>
    <rect x="0" y="120" width="30" height="30" fill="#E8EDF5" stroke="#3A4255" stroke-width="0.5"/>
    <rect x="30" y="120" width="30" height="30" fill="#E8EDF5" stroke="#3A4255" stroke-width="0.5"/>
    <rect x="60" y="120" width="30" height="30" fill="#E8EDF5" stroke="#3A4255" stroke-width="0.5"/>
    <rect x="90" y="120" width="30" height="30" fill="#E8EDF5" stroke="#3A4255" stroke-width="0.5"/>
    <rect x="120" y="120" width="30" height="30" fill="#E8EDF5" stroke="#3A4255" stroke-width="0.5"/>
    <!-- Highlight the filter window -->
    <rect x="30" y="30" width="90" height="90" fill="none" stroke="#4EC9C0" stroke-width="2.5" stroke-dasharray="6,3"/>
    <text x="75" y="172" text-anchor="middle" fill="#8D96A8" font-size="11" font-family="Calibri,sans-serif">Image (dark → light)</text>
  </g>
  <!-- Arrow -->
  <polygon points="218,115 210,110 210,120" fill="#E8EDF5"/>
  <line x1="155" y1="115" x2="219" y2="115" stroke="#E8EDF5" stroke-width="1.5"/>
  <!-- Filter matrix -->
  <g transform="translate(224,55)">
    <text x="50" y="-8" text-anchor="middle" fill="#4EC9C0" font-size="12" font-family="Calibri,sans-serif">Horizontal edge filter</text>
    <rect x="0" y="0" width="100" height="120" rx="4" fill="#1A1F2E" stroke="#4EC9C0" stroke-width="1.5"/>
    <!-- Row labels -->
    <text x="50" y="26" text-anchor="middle" fill="#E05C5C" font-size="14" font-family="Calibri,Courier,monospace" font-weight="bold">−1  −1  −1</text>
    <line x1="5" y1="40" x2="95" y2="40" stroke="#3A4255" stroke-width="0.8"/>
    <text x="50" y="66" text-anchor="middle" fill="#8D96A8" font-size="14" font-family="Calibri,Courier,monospace"> 0   0   0</text>
    <line x1="5" y1="80" x2="95" y2="80" stroke="#3A4255" stroke-width="0.8"/>
    <text x="50" y="106" text-anchor="middle" fill="#5CB85C" font-size="14" font-family="Calibri,Courier,monospace">+1  +1  +1</text>
    <text x="50" y="138" text-anchor="middle" fill="#8D96A8" font-size="11" font-family="Calibri,sans-serif">9 weights total</text>
  </g>
  <!-- Arrow -->
  <polygon points="378,115 370,110 370,120" fill="#E8EDF5"/>
  <line x1="324" y1="115" x2="379" y2="115" stroke="#E8EDF5" stroke-width="1.5"/>
  <!-- Feature map output -->
  <g transform="translate(384,40)">
    <text x="60" y="-8" text-anchor="middle" fill="#5CB85C" font-size="12" font-family="Calibri,sans-serif">Feature map output</text>
    <rect x="0" y="0" width="30" height="30" fill="#1A1F2E" stroke="#3A4255" stroke-width="0.5"/>
    <rect x="30" y="0" width="30" height="30" fill="#1A1F2E" stroke="#3A4255" stroke-width="0.5"/>
    <rect x="60" y="0" width="30" height="30" fill="#1A1F2E" stroke="#3A4255" stroke-width="0.5"/>
    <rect x="0" y="30" width="30" height="30" fill="#1A1F2E" stroke="#3A4255" stroke-width="0.5"/>
    <rect x="30" y="30" width="30" height="30" fill="#F0A500" stroke="#3A4255" stroke-width="0.5"/>
    <rect x="60" y="30" width="30" height="30" fill="#F0A500" stroke="#3A4255" stroke-width="0.5"/>
    <rect x="0" y="60" width="30" height="30" fill="#1A1F2E" stroke="#3A4255" stroke-width="0.5"/>
    <rect x="30" y="60" width="30" height="30" fill="#1A1F2E" stroke="#3A4255" stroke-width="0.5"/>
    <rect x="60" y="60" width="30" height="30" fill="#1A1F2E" stroke="#3A4255" stroke-width="0.5"/>
    <!-- Highlight the "fired" cells -->
    <text x="30" y="110" fill="#8D96A8" font-size="10" font-family="Calibri,sans-serif">≈0</text>
    <text x="30" y="125" fill="#F0A500" font-size="10" font-family="Calibri,sans-serif">high → edge detected</text>
    <text x="30" y="140" fill="#8D96A8" font-size="10" font-family="Calibri,sans-serif">≈0</text>
  </g>
  <!-- Annotation -->
  <text x="560" y="90" fill="#4EC9C0" font-size="13" font-family="Calibri,sans-serif">Dark→light transition</text>
  <text x="560" y="110" fill="#4EC9C0" font-size="13" font-family="Calibri,sans-serif">= horizontal edge</text>
  <text x="560" y="130" fill="#4EC9C0" font-size="13" font-family="Calibri,sans-serif">= filter fires ✓</text>
  <text x="560" y="170" fill="#8D96A8" font-size="12" font-family="Calibri,sans-serif">Same filter slides</text>
  <text x="560" y="188" fill="#8D96A8" font-size="12" font-family="Calibri,sans-serif">across whole image</text>
</svg>

---

<!-- _class: technical -->
<div class="header-label">VISUAL RECOGNITION</div>

## 2.4 LeCun and LeNet

- **Yann LeCun**, Bell Labs, late 1980s–early 1990s
- Built **LeNet**: convolutional network for handwritten digit recognition
- Deployed by the **US Postal Service** to read ZIP codes — real-world, at scale
- Trained end-to-end: raw pixels in, digit labels out, backpropagation throughout

**The MNIST dataset:** 70,000 images, 28×28 pixels, digits 0–9. Still a standard benchmark.

<div class="callout">The central idea: stop hand-crafting features. Let the network discover them. Those learned features beat anything humans designed.</div>

---

<!-- _class: technical -->
<div class="header-label">VISUAL RECOGNITION</div>

## 2.5 The Dark Years: Why Deep Networks Failed

Through the 1990s–2000s, neural networks lost ground to other methods. The core problem: **depth**.

- **Vanishing gradients** — the error signal shrinks exponentially as it propagates backward through many layers. Early layers receive almost nothing and don't learn.
- **Poor initialization** — random weights land in bad regions of the loss landscape.

**Geoffrey Hinton's 2006 solution:** layer-wise pretraining using Restricted Boltzmann Machines
- Train one layer at a time; each layer builds on the previous
- By fine-tuning time, the network already has meaningful structure
- Proved deep networks *could* be trained — and learned richer representations

---

<!-- _class: technical -->
<div class="header-label">VISUAL RECOGNITION</div>

## 2.5 The Comeback: AlexNet (2012)

Hinton's pretraining was soon replaced by simpler ingredients:

- **ReLU activations** — a new activation function that resists vanishing gradients
  *(negative input → output zero; positive → pass through unchanged)*
- **Better weight initialization** — smarter starting distributions
- **Dropout** — randomly disable neurons during training to prevent overfitting

Combined with large datasets (ImageNet: 1.2M images) and GPU computing:

**AlexNet** demolished all competitors in the 2012 ImageNet competition.

<div class="callout">Hinton's specific mechanism didn't survive. His <em>conviction</em> — that depth was the right direction — did.</div>

---

<!-- _class: divider progress -->
<div class="divider-content">

# 3

<div class="rule"></div>

## Large Language Models

<span class="reading-label">Session Two</span>
</div>

---

<!-- _class: progress -->
<div class="header-label">LARGE LANGUAGE MODELS</div>

## 3.1 Language Is Hard

Consider the word **"dog"**. It relates to: puppy, hound, mammal, bite, run, pant, pet...

In a sentence:
- Is it subject or object?
- Does "it" later refer to the dog, or something else?
- "May" — the month, a name, or a modal verb?

<br>

A paragraph is a web of interacting words that together construct meaning.

The critical breakthrough: **"Attention Is All You Need"** — Google, 2017. What follows is a description of that architecture.

---

<!-- _class: progress -->
<div class="header-label">LARGE LANGUAGE MODELS</div>

## 3.2 Tokens — What the Model Reads

Not whole words. Not single letters. **Tokens** — a middle ground.

- Common words → one token: *"the"*, *"cat"*
- Rare words → fragments: *"unbelievable"* → `"un"` + `"believ"` + `"able"`
- Vocabulary: ~50,000–100,000 tokens covers virtually any text

**Byte Pair Encoding (BPE):** starts with single characters, iteratively merges the most frequent adjacent pairs until target vocabulary size is reached.

<div class="callout"><strong>Curious limitation:</strong> ask a model to count the letters in <em>strawberry</em> and it may get it wrong — it sees tokens "straw" and "berry", never individual letters.</div>

---

<!-- _class: progress -->
<div class="header-label">LARGE LANGUAGE MODELS</div>

## 3.3 Embeddings

Token IDs are just numbers — #4271 has no meaningful relationship to #4270.

The **embedding layer** converts each token ID into a **vector** of ~4,000 numbers.

- Initially: entirely random
- After training: tokens with similar meanings cluster geometrically
  - *"king"* and *"queen"* are nearby; *"king"* and *"bicycle"* are far apart
- The embedding vectors are **weights** — learned by gradient descent

<br>

These are not "semantic" relationships in the philosophical sense — the model has no knowledge of real-world dogs. They are **distributional**: how does this word co-occur with others across billions of sentences?

---

<!-- _class: progress -->
<div class="header-label">LARGE LANGUAGE MODELS</div>

## 3.4 Positional Encoding

An embedding captures *what* a token means. Not *where* it appears.

*"Not the dog bit the man"* vs *"The dog bit the man"* — position matters.

A **positional encoding vector** is added to each token's embedding:
- Uses sine/cosine functions at different frequencies (original scheme)
- Like a clock: second hand, minute hand, hour hand — together they encode time unambiguously
- Modern LLMs use learned variants (RoPE) that handle longer sequences better

Result: one vector per token, encoding both **identity** and **position**.

---

<!-- _class: progress -->
<div class="header-label">LARGE LANGUAGE MODELS</div>

## 3.5 The Attention Mechanism

<svg viewBox="0 0 780 230" xmlns="http://www.w3.org/2000/svg" style="width:100%;max-height:220px">
  <!-- Sentence tokens -->
  <g font-family="Calibri,sans-serif" font-size="13">
    <rect x="20" y="20" width="80" height="32" rx="4" fill="#2A3247" stroke="#4EC9C0" stroke-width="1.5"/>
    <text x="60" y="41" text-anchor="middle" fill="#E8EDF5">She</text>
    <rect x="112" y="20" width="80" height="32" rx="4" fill="#2A3247" stroke="#4EC9C0" stroke-width="1.5"/>
    <text x="152" y="41" text-anchor="middle" fill="#E8EDF5">went</text>
    <rect x="204" y="20" width="80" height="32" rx="4" fill="#2A3247" stroke="#4EC9C0" stroke-width="1.5"/>
    <text x="244" y="41" text-anchor="middle" fill="#E8EDF5">to</text>
    <rect x="296" y="20" width="80" height="32" rx="4" fill="#2A3247" stroke="#8D96A8" stroke-width="1.5"/>
    <text x="336" y="41" text-anchor="middle" fill="#8D96A8">the</text>
    <rect x="388" y="20" width="80" height="32" rx="4" fill="#2A3247" stroke="#F0A500" stroke-width="2.5"/>
    <text x="428" y="41" text-anchor="middle" fill="#F0A500" font-weight="bold">bank</text>
    <rect x="480" y="20" width="80" height="32" rx="4" fill="#2A3247" stroke="#8D96A8" stroke-width="1.5"/>
    <text x="520" y="41" text-anchor="middle" fill="#8D96A8">by</text>
    <rect x="572" y="20" width="80" height="32" rx="4" fill="#2A3247" stroke="#4EC9C0" stroke-width="2"/>
    <text x="612" y="41" text-anchor="middle" fill="#4EC9C0" font-weight="bold">river</text>
  </g>
  <!-- Attention arc: "bank" attends strongly to "river" -->
  <path d="M428,20 C428,-10 612,-10 612,20" stroke="#4EC9C0" stroke-width="2.5" fill="none" stroke-dasharray="0"/>
  <polygon points="612,20 606,12 618,12" fill="#4EC9C0"/>
  <text x="520" y="-2" text-anchor="middle" fill="#4EC9C0" font-size="11" font-family="Calibri,sans-serif">strong attention (disambiguates "bank")</text>
  <!-- Weak attention arc: "bank" to "went" -->
  <path d="M428,20 C428,5 152,5 152,20" stroke="#8D96A8" stroke-width="1" fill="none" stroke-dasharray="4,3" stroke-opacity="0.5"/>
  <text x="290" y="8" text-anchor="middle" fill="#8D96A8" font-size="10" font-family="Calibri,sans-serif">weak</text>
  <!-- Q K V explanation -->
  <rect x="20" y="100" width="220" height="115" rx="5" fill="#1A1F2E" stroke="#4EC9C0" stroke-width="1"/>
  <text x="130" y="118" text-anchor="middle" fill="#4EC9C0" font-size="12" font-family="Calibri,sans-serif" font-weight="bold">For each token:</text>
  <text x="30" y="138" fill="#E8EDF5" font-size="12" font-family="Calibri,sans-serif"><tspan fill="#F0A500" font-weight="bold">Q</tspan> = what this token is looking for</text>
  <text x="30" y="158" fill="#E8EDF5" font-size="12" font-family="Calibri,sans-serif"><tspan fill="#5CB85C" font-weight="bold">K</tspan> = what this token offers</text>
  <text x="30" y="178" fill="#E8EDF5" font-size="12" font-family="Calibri,sans-serif"><tspan fill="#4EC9C0" font-weight="bold">V</tspan> = what this token contributes</text>
  <text x="30" y="204" fill="#8D96A8" font-size="11" font-family="Calibri,sans-serif">Q·K = attention score → softmax → weight V</text>
  <!-- Causal masking box -->
  <rect x="270" y="100" width="260" height="80" rx="5" fill="#1A1F2E" stroke="#E05C5C" stroke-width="1"/>
  <text x="400" y="120" text-anchor="middle" fill="#E05C5C" font-size="12" font-family="Calibri,sans-serif" font-weight="bold">Causal Masking (generation)</text>
  <text x="280" y="142" fill="#8D96A8" font-size="11" font-family="Calibri,sans-serif">Each token can only attend to</text>
  <text x="280" y="160" fill="#8D96A8" font-size="11" font-family="Calibri,sans-serif">itself and previous tokens —</text>
  <text x="280" y="175" fill="#8D96A8" font-size="11" font-family="Calibri,sans-serif">never future ones.</text>
  <!-- Multi-head box -->
  <rect x="555" y="100" width="210" height="80" rx="5" fill="#1A1F2E" stroke="#7B68EE" stroke-width="1"/>
  <text x="660" y="120" text-anchor="middle" fill="#7B68EE" font-size="12" font-family="Calibri,sans-serif" font-weight="bold">Multi-Head Attention</text>
  <text x="565" y="142" fill="#8D96A8" font-size="11" font-family="Calibri,sans-serif">Run in parallel, many times,</text>
  <text x="565" y="160" fill="#8D96A8" font-size="11" font-family="Calibri,sans-serif">each with different Q,K,V matrices.</text>
  <text x="565" y="178" fill="#8D96A8" font-size="11" font-family="Calibri,sans-serif">Each head learns different relations.</text>
</svg>

---

<!-- _class: progress -->
<div class="header-label">LARGE LANGUAGE MODELS</div>

## 3.5 The Transformer — In Hinton's Terms

Geoffrey Hinton, in recent public talks, offers something like this:

> *The transformer processes all the words simultaneously. Each word looks at all the other words and asks: which of you should I be paying attention to? The answer changes the meaning of each word. After many such rounds, each word knows its full context — and from that, the next word can be predicted.*

The key insight: **meaning is not in individual words, it emerges from their relationships** — and attention is the mechanism that computes those relationships.

---

<!-- _class: progress -->
<div class="header-label">LARGE LANGUAGE MODELS</div>

## 3.6 Feed-Forward Layer & Stacking

After attention: each token has gathered context. Now transform it.

**Feed-forward layer** (per token, independently):
- Expand vector ~4× in size (more room to work)
- Apply nonlinearity (ReLU — negative values → 0)
- Compress back down

**Residual connections:** add the original vector back in at each step — network learns *adjustments*, not reconstructions.

**Stack many layers.** GPT-3: 96 layers. Modern frontier models: ~100–200.

| | Attention | Feed-Forward |
|---|---|---|
| **Does** | Communication between tokens | Computation within each token |

---

<!-- _class: progress -->
<div class="header-label">LARGE LANGUAGE MODELS</div>

## 3.7 Training

**Self-supervised:** no human labels. The text itself is the training signal.
- Show the model text → ask it to predict the next token
- The correct answer is always right there in the data
- Billions of predictions per training run

**Gradient descent** updates all weights to reduce prediction error.

Scale of frontier model training:
- Thousands of GPUs
- Months of compute
- Hundreds of millions of dollars

---

<!-- _class: progress -->
<div class="header-label">LARGE LANGUAGE MODELS</div>

## 3.9 Fine-Tuning: RLHF and LoRA

**Pre-trained model:** can predict next tokens fluently. No particular goal. Will just keep generating text.

**RLHF** (Reinforcement Learning from Human Feedback):
1. Human trainers write ideal responses → supervised fine-tuning
2. Human raters compare outputs → train a **reward model**
3. Main model is trained to maximize reward model scores

Shapes the model toward: completing tasks · being helpful · avoiding harmful outputs

**LoRA** (Low-Rank Adaptation): how to fine-tune *without* overwriting pre-trained knowledge
- Freeze all original weights
- Add small trainable matrices alongside them (much fewer parameters)
- Only the small additions are updated

---

<!-- _class: progress -->
<div class="header-label">LARGE LANGUAGE MODELS</div>

## 3.10 Reasoning

**Chain-of-thought:** instead of jumping to an answer, the model writes out intermediate steps.

- Each generated token becomes context for the next
- Writing steps = giving itself scratch paper
- More tokens → more computation → better answers on hard problems

More sophisticated variants: beam search, tree search, self-consistency (majority vote across multiple independent reasoning chains).

<div class="callout">Before reasoning: most GPU work happened during training. After: everyday inference is GPU-intensive too.</div>

---

<!-- _class: progress -->
<div class="header-label">LARGE LANGUAGE MODELS</div>

## 3.11 The Chinese Strategy

- US restricted export of top-tier GPUs to China (Biden era)
- Trump administration later eased restrictions
- China didn't rush to buy them — two reasons:
  1. Building domestic chip expertise is a strategic priority
  2. They pursued **efficiency** instead of raw compute

**DeepSeek** (2025): results competitive with top American LLMs, at a fraction of the development cost.

<div class="callout">The lesson: more compute is not the only path to capable AI.</div>

---

<!-- _class: divider progress -->
<div class="divider-content">

# 4

<div class="rule"></div>

## A Taxonomy of Neural Networks

<span class="reading-label">Session Two</span>
</div>

---

<!-- _class: progress -->
<div class="header-label">TAXONOMY</div>

## 4. The Neural Network Family

| Architecture | Best suited for |
|---|---|
| **Feedforward / MLP** | General-purpose; building blocks |
| **Autoencoder** | Compression, anomaly detection |
| **Convolutional (CNN)** | Images, spatial data |
| **Recurrent (LSTM/GRU)** | Sequences — pre-transformer era |
| **Transformer** | Language, vision, most tasks today |
| **GAN** | Image generation (largely superseded) |
| **Diffusion model** | Image & audio generation |
| **Graph NN** | Molecules, social networks |
| **Reinforcement learning** | Games, robotics |

Modern systems **combine** several of these. The boundaries are permeable.

---

<!-- _class: divider alignment -->
<div class="divider-content">

# 5

<div class="rule"></div>

## Diffusion Models & Image Generation

<span class="reading-label">Session Two</span>
</div>

---

<!-- _class: alignment -->
<div class="header-label">IMAGE GENERATION</div>

## 5.1 – 5.2 Learning to Denoise

**Training:** start with real images, systematically add noise across ~1,000 steps until pure randomness. At each step, teach the network to estimate what noise was added.

After millions of examples: the network has a rich internal model of what images look like — not by memorizing them, but by learning what separates signal from noise.

**Generation:** run in reverse. Start from pure noise. Iteratively subtract estimated noise. An image coalesces.

<div class="callout">The model never "draws" pixels. It makes a thousand small corrections, each guided by everything it learned about visual structure.</div>

---

<!-- _class: alignment -->
<div class="header-label">IMAGE GENERATION</div>

## 5.3 – 5.4 Text-Guided Generation & the Latent Space

**Text conditioning:** a text encoder (CLIP) converts the prompt into a vector. At every denoising step, this vector steers the corrections toward images consistent with the prompt.

**How can it generate things never in the training data?**

The training images were compressed into a **latent space** — a map of visual concepts. Dragon scales cluster near reptile skin. Neon glow clusters near wet pavement. The prompt "a knight riding a dragon over a cyberpunk city" lands in a region surrounded by all these concept clusters. The denoiser navigates toward it.

*No memorized images. A learned visual grammar.*

---

<!-- _class: alignment -->
<div class="header-label">IMAGE GENERATION</div>

## 5.6 A Video to Explain and Demonstrate Image Generation

It is hard to undertstand how denoising can produce a meaningful image, especially one that is invented using previous patterns.  The following video provides an explanation: [How AI Image Generation Works](https://www.youtube.com/watch?v=iv-5mZ_9CPY)

---

<!-- _class: divider social -->
<div class="divider-content">

# 6

<div class="rule"></div>

## Self-Driving Cars

<span class="reading-label">Session Two</span>
</div>

---

<!-- _class: social -->
<div class="header-label">SELF-DRIVING CARS</div>

## 6.1 Historical Roots: Learning to Stay on the Road

**ALVINN (Carnegie Mellon, late 1980s):** early neural network trained on camera video + human steering — backprop, gradient descent, loss function. Worked well in familiar conditions.

**The core failure:** a model trained only on correct driving has never seen recovery. Once it drifts, it's in territory training never covered — and keeps drifting.

**The fix — DAgger (Dataset Aggregation, ~2011):**
- Deploy the model; let it drive
- A human expert labels each state the model *actually visits* with the correct action — including off-nominal states
- Add those pairs to training; retrain; repeat

<div class="callout">Key insight: you must train on states the model actually reaches, not just states an expert would visit.</div>

---

<!-- _class: social -->
<div class="header-label">SELF-DRIVING CARS</div>

## 6.2 – 6.3 The Full Stack

A self-driving vehicle is a **pipeline**, not a single AI:

1. **Sensors** — cameras, LiDAR, radar, GPS/HD maps. Each has distinct failure modes; redundancy is deliberate.
2. **Beyond the four primaries** — IMUs detect slip and unexpected forces (digital vestibular sense); wheel/suspension sensors infer road surface; microphone research ongoing for sirens and horns.
3. **Sensor fusion** — combine all streams into one scene representation (transformer-based)
4. **Perception** — object detection, semantic segmentation, localization
5. **Prediction** — probability distributions over futures, not single trajectories
6. **Planning** — route, behavior, motion (three nested levels)
7. **Control** — steering, throttle, brake. Classical feedback controllers, not neural networks.

<div class="callout">Humans also use eye contact, hand gestures, and sound. Current AVs replicate only a subset of human sensory integration.</div>

---

<!-- _class: social -->
<div class="header-label">SELF-DRIVING CARS</div>

## 6.5 Modular vs. End-to-End

<div style="display:grid;grid-template-columns:1fr 1fr;gap:24px;margin-top:8px">
<div>

**Modular (Waymo)**
- Human-designed interfaces between stages
- Each stage inspectable and testable
- Failures can be isolated
- Expensive sensor suite (LiDAR)

</div>
<div>

**End-to-End (Tesla)**
- Pixels in → driving commands out
- Intermediate representations learned, not designed
- Camera-only; vast fleet data
- Hard to diagnose failures

</div>
</div>

**The long-tail problem cuts hardest against end-to-end:** neural networks are interpolators — they degrade on inputs far from training data. Rare events may appear too infrequently to learn. The physical world generates novel situations continuously; the tail is inexhaustible.

---

<!-- _class: social -->
<div class="header-label">SELF-DRIVING CARS</div>

## 6.5 A Concrete Failure: Tempe, Arizona 2018

An Uber autonomous vehicle struck and killed Elaine Herzberg, who was walking her bicycle across a road at night.

**What the NTSB found:**
- System cycled between classifying her as an unknown object, a vehicle, and a bicycle — never settling
- Not designed to infer that a bicycle classification implied a human nearby
- Emergency braking had been **disabled** by engineers to reduce false positives
- Safety driver was not watching the road

<div class="callout">A perception failure under an unusual combination of circumstances the training distribution had not adequately covered — a textbook long-tail event.</div>

---

<!-- _class: social -->
<div class="header-label">SELF-DRIVING CARS</div>

## 6.6 Waymo's World Model: Neuro-Symbolic AI

Waymo doesn't just use neural networks — it encodes **explicit physics-based knowledge** alongside them. This is a hybrid of classical AI (GOFAI) and deep learning.

The world model operates in four ways — not as a fallback, but woven in throughout:

- **Constraint:** physically impossible trajectories are ruled out before planning considers them
- **Prior:** when the network is uncertain, physics and context resolve the ambiguity (Bayesian reasoning)
- **Simulation substrate:** possible futures are simulated forward; the network assigns probabilities to them
- **Planning space:** motion planning searches only within physically valid, map-consistent trajectories

<div class="callout">This is <strong>neuro-symbolic AI</strong> — arguably the most sophisticated real-world deployment of that hybrid philosophy.</div>

---

<!-- _class: social -->
<div class="header-label">SELF-DRIVING CARS</div>

## 6.7 The SAE Scale

| Level | Description | Who's responsible |
|---|---|---|
| 0 | No automation | Driver, always |
| 1 | Driver assistance | Driver |
| 2 | Partial (steering + speed) | Driver must supervise |
| **3** | **Conditional** | **Manufacturer during auto operation** |
| 4 | High — driverless in defined domain | Manufacturer |
| 5 | Full — driverless anywhere | Manufacturer |

The legal threshold between 2 and 3 has shaped every company's product strategy.

---

<!-- _class: social -->
<div class="header-label">SELF-DRIVING CARS</div>

## 6.8 – 6.9 Waymo vs Tesla

**Waymo** — true Level 4 robotaxi in SF, LA, Phoenix, Austin
- All decisions made onboard (latency physics demand it)
- Cloud used only for training, updates, monitoring, edge-case assistance
- Expensive sensor suite has constrained scaling

**Tesla** — Level 2 "Full Self-Driving" (officially)
- Camera-only; end-to-end neural networks; massive fleet data
- Level 4 robotaxi launched Austin mid-2025; SF (with safety driver) 2025–26

**Safety:** Waymo has published strong comparative data across millions of driverless miles. Tesla's robotaxi dataset is too new for meaningful comparison.

**Level 5 — fully autonomous everywhere — remains unsolved for both.**

---

<!-- _class: social -->
<div class="header-label">SELF-DRIVING CARS</div>

## 6.10 Beyond Passenger Cars: Autonomous Trucking

**The economic case is compelling:** driver shortage, wages, mandatory rest periods, hours-of-service rules — human drivers are the largest freight operating cost.

**Aurora Innovation** is the clear leader:
- May 2025: first commercial driverless Class 8 trucks on public roads (Dallas–Houston)
- Early 2026: 250,000+ driverless miles, zero attributed collisions, 12 routes across Sun Belt
- Some trucks carry a passive observer at partner request; next-gen hardware (mid-2026) eliminates even that

**Others in earlier development:** Kodiak Robotics, Torc Robotics (Daimler), Gatik (fixed middle-mile routes)

**Common near-term model:** driver-out on the highway, driver-in at terminals — captures most efficiency gains while sidestepping the hardest problems.

**Technical note:** 80,000 lb trucks at highway speed demand exceptional prediction horizons. Consequences of failure are severe.

---

<!-- _class: closing -->
<div class="accent-bar"></div>
<div class="deco-panel"></div>
<div class="closing-content">

# Questions?

## The full document covers each topic in depth — with history, diagrams, and technical detail.

<br>

<span class="muted">Next session picks up at Section 3: Large Language Models</span>

</div>
<div class="closing-footer">UNDERSTANDING ARTIFICIAL INTELLIGENCE</div>
