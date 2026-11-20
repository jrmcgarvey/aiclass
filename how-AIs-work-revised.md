# How AI Systems Work: From Biology to Large Language Models

## Introduction

Today's session — we may spill over to a second meeting — attempts to explain how current AI systems work. We will start with visual recognition. Large language models proved harder to explain. Note: most of the techniques described here have been superseded or refined, so you will not see the current state of the art everywhere. But you will understand the arc of ideas that got us here.

Fair warning: this is pretty technical stuff.

One of the most compelling ways to understand modern neural networks is to trace their origins — from early neuroscience experiments on cats, through the first practical applications in reading handwritten digits, to the deep learning revolution that shapes artificial intelligence today. This document follows that arc, using the history of visual recognition as a thread to illuminate the core ideas behind convolutional neural networks and deep learning, and then turns to large language models, image generation, and self-driving cars.

---

# 1. Basic Neural Network Concepts

---

## 1.1 Forward Propagation in a Neural Network

You start with input data, represented as a collection of **vectors**. A vector is an ordered list of numbers. For an image, a vector might be the RGB (red-green-blue) value of a given pixel. For text being processed by a large language model (LLM), each vector might be a collection of numbers assigned to a textual element in the input — a word, or part of a word.

The first layer then applies a transformation. One part of the transformation is matrix multiplication. A matrix is a rectangular array of numbers. Information from various subsets of vectors in the input is combined and multiplied by the matrix. This combines the information to derive something about the input — for example, "there is an edge at this point in the image," or "this word is the subject of the sentence." Several matrices are used at each stage. Then an **activation function** is applied. The activation function introduces a critical nonlinearity: without it, stacking layer upon layer of matrix multiplications would collapse mathematically to a single multiplication, no matter how many layers you added. The nonlinearity allows the network to represent complex, conditional, threshold-like relationships — the kind that meaning and pattern recognition actually involve. A transformed set of vectors is then passed to the next layer, where the process repeats with a different set of matrices.

Each number in each matrix is a **weight**, or a parameter of the model. At the outset, these weights are randomly assigned — numbers chosen from a range according to some distribution function. As there can be many layers to the model, and many matrices at each layer, there can be many weights — hundreds of billions in current LLMs, for example.

<svg viewBox="0 0 700 180" xmlns="http://www.w3.org/2000/svg" style="width:100%;max-width:700px;display:block;margin:1.2em 0">
  <!-- Input nodes -->
  <circle cx="70" cy="50" r="20" fill="#e8f4f8" stroke="#2a7ae2" stroke-width="2"/>
  <circle cx="70" cy="110" r="20" fill="#e8f4f8" stroke="#2a7ae2" stroke-width="2"/>
  <circle cx="70" cy="170" r="20" fill="#e8f4f8" stroke="#2a7ae2" stroke-width="2"/>
  <!-- Hidden layer 1 -->
  <circle cx="230" cy="35" r="20" fill="#eaf7ea" stroke="#2a7a2a" stroke-width="2"/>
  <circle cx="230" cy="95" r="20" fill="#eaf7ea" stroke="#2a7a2a" stroke-width="2"/>
  <circle cx="230" cy="155" r="20" fill="#eaf7ea" stroke="#2a7a2a" stroke-width="2"/>
  <!-- Hidden layer 2 -->
  <circle cx="390" cy="35" r="20" fill="#eaf7ea" stroke="#2a7a2a" stroke-width="2"/>
  <circle cx="390" cy="95" r="20" fill="#eaf7ea" stroke="#2a7a2a" stroke-width="2"/>
  <circle cx="390" cy="155" r="20" fill="#eaf7ea" stroke="#2a7a2a" stroke-width="2"/>
  <!-- Output nodes -->
  <circle cx="550" cy="70" r="20" fill="#fff8e8" stroke="#c87800" stroke-width="2"/>
  <circle cx="550" cy="140" r="20" fill="#fff8e8" stroke="#c87800" stroke-width="2"/>
  <!-- Connections input->h1 -->
  <line x1="90" y1="55" x2="210" y2="40" stroke="#2a7ae2" stroke-width="1" stroke-opacity="0.35"/>
  <line x1="90" y1="57" x2="210" y2="97" stroke="#2a7ae2" stroke-width="1" stroke-opacity="0.35"/>
  <line x1="90" y1="110" x2="210" y2="38" stroke="#2a7ae2" stroke-width="1" stroke-opacity="0.35"/>
  <line x1="90" y1="112" x2="210" y2="97" stroke="#2a7ae2" stroke-width="1" stroke-opacity="0.35"/>
  <line x1="90" y1="114" x2="210" y2="153" stroke="#2a7ae2" stroke-width="1" stroke-opacity="0.35"/>
  <line x1="90" y1="168" x2="210" y2="97" stroke="#2a7ae2" stroke-width="1" stroke-opacity="0.35"/>
  <line x1="90" y1="170" x2="210" y2="153" stroke="#2a7ae2" stroke-width="1" stroke-opacity="0.35"/>
  <!-- Connections h1->h2 -->
  <line x1="250" y1="38" x2="370" y2="38" stroke="#2a7a2a" stroke-width="1" stroke-opacity="0.35"/>
  <line x1="250" y1="42" x2="370" y2="97" stroke="#2a7a2a" stroke-width="1" stroke-opacity="0.35"/>
  <line x1="250" y1="97" x2="370" y2="38" stroke="#2a7a2a" stroke-width="1" stroke-opacity="0.35"/>
  <line x1="250" y1="99" x2="370" y2="99" stroke="#2a7a2a" stroke-width="1" stroke-opacity="0.35"/>
  <line x1="250" y1="101" x2="370" y2="153" stroke="#2a7a2a" stroke-width="1" stroke-opacity="0.35"/>
  <line x1="250" y1="153" x2="370" y2="97" stroke="#2a7a2a" stroke-width="1" stroke-opacity="0.35"/>
  <line x1="250" y1="155" x2="370" y2="154" stroke="#2a7a2a" stroke-width="1" stroke-opacity="0.35"/>
  <!-- Connections h2->output -->
  <line x1="410" y1="38" x2="530" y2="72" stroke="#c87800" stroke-width="1" stroke-opacity="0.35"/>
  <line x1="410" y1="97" x2="530" y2="73" stroke="#c87800" stroke-width="1" stroke-opacity="0.35"/>
  <line x1="410" y1="99" x2="530" y2="140" stroke="#c87800" stroke-width="1" stroke-opacity="0.35"/>
  <line x1="410" y1="153" x2="530" y2="138" stroke="#c87800" stroke-width="1" stroke-opacity="0.35"/>
  <!-- Labels -->
  <text x="70" y="198" text-anchor="middle" fill="#555" font-size="12" font-family="sans-serif">Input</text>
  <text x="230" y="198" text-anchor="middle" fill="#555" font-size="12" font-family="sans-serif">Hidden layer 1</text>
  <text x="390" y="198" text-anchor="middle" fill="#555" font-size="12" font-family="sans-serif">Hidden layer 2</text>
  <text x="550" y="198" text-anchor="middle" fill="#555" font-size="12" font-family="sans-serif">Output</text>
  <text x="310" y="14" text-anchor="middle" fill="#888" font-size="11" font-family="sans-serif" font-style="italic">every connecting line is a weight</text>
  <!-- Output label -->
  <text x="620" y="75" fill="#c87800" font-size="13" font-family="sans-serif">🐱 93%</text>
  <text x="620" y="145" fill="#aaa" font-size="13" font-family="sans-serif">🐶  5%</text>
</svg>

## 1.2 The Output Layer

After all the layers have done their work, the result is mapped to a collection of **logits** — raw scores, one for each possible output category. For image recognition, a logit represents how strongly the network believes the image is, say, a cat, or a house, or a car. For an LLM, logits represent how likely each possible next word (or word-fragment) is.

The logits themselves are learned — there is a set of weights that produces them. Then a **softmax function** is applied, which converts the logits into probabilities that add up to 100%. The model might then conclude that the image is a cat with 93% probability.

One consequence of softmax is worth noting: because the probabilities always sum to 100%, the model is forced to assign the input to one of its known categories. If you show it something it has never encountered, it will never say "beats the heck out of me." It will assign probabilities across its known categories regardless.

## 1.3 The Loss Function

The end product is some assertion about the input — for example, "this image is a cat" or "the next word is *actually*." During training, the model will be wrong some fraction of the time. The **loss function** (sometimes called a cost function) measures how wrong the model is, in aggregate, across a batch of training examples.

For visual recognition, **supervised learning** is used: a set of images labeled by humans as belonging to a fixed list of categories. The model's output is compared against the correct label, and the difference is the loss.

For LLMs, the approach is different and worth understanding carefully. The training data is simply text from the Internet — it is not labeled by humans. The model is trained to predict the next token (word fragment) given all the preceding tokens. Because the "correct answer" at every position is right there in the text itself, no human labeling is needed. The supervision is automatic, derived from the structure of the data. This is called **self-supervised learning** — a term more precise than "unsupervised," which technically means no learning signal exists at all. The distinction matters because it clarifies how LLMs learn: they are not simply clustering or compressing data; they are making billions of specific, checkable predictions and correcting themselves on each one.

## 1.4 Adjusting the Weights: Gradient Descent

Initially, the weights are randomly assigned — random within a range and with a particular distribution. For example, a distribution that assigns middle-range values more often than extreme ones. The neural network must learn a better set of weights — ones that reduce the loss.

### 1.4.1 The Landscape Analogy

Imagine a plastic relief map of a mountain range — the kind where you can feel the peaks and valleys with your hand. Every point has a height. Your goal is to find the lowest point in the landscape — the bottom of the deepest valley. You are blindfolded. You can only feel the slope immediately beneath your feet. A reasonable strategy is to feel which direction is most steeply downhill, take a careful step in that direction, stop and feel again. Repeat.

This is **gradient descent**. The height at any point on the map represents the loss — how wrong the model's predictions are. The slope at any point is the **gradient** — a measure of how steeply the loss is changing. The model follows the gradient downhill, adjusting its weights in small steps.

A real topographic map has two dimensions. The loss landscape of a large language model has **billions** of dimensions — one for each weight. This is impossible to visualize, but the principle is exactly the same. At each step of training, the model calculates the gradient across all those dimensions simultaneously and takes a small step in the direction that most reduces the loss.

The step size is kept deliberately small, controlled by a parameter called the **learning rate**. Large steps risk overshooting a good valley and ending up somewhere worse. The model rarely finds the single lowest point in the entire landscape — it finds *a* valley that is good enough. Researchers have found that many different valleys produce models of similar quality, which is why different training runs starting from different random initializations tend to perform comparably despite having quite different weights.

<svg viewBox="0 0 700 190" xmlns="http://www.w3.org/2000/svg" style="width:100%;max-width:700px;display:block;margin:1.2em 0">
  <rect width="700" height="190" fill="#f7f9fc" rx="6"/>
  <path d="M0,170 C35,168 55,158 85,122 C105,98 118,88 142,74 C160,62 174,59 188,78 C202,94 211,108 229,94 C248,79 262,46 290,27 C309,15 323,12 342,31 C356,46 365,64 384,78 C402,91 416,85 434,69 C448,57 457,50 476,64 C494,78 508,97 527,111 C546,125 560,130 583,116 C602,104 616,92 640,106 C658,118 672,140 695,150 L700,190 L0,190 Z" fill="#ddeeff" stroke="#5599cc" stroke-width="1.5"/>
  <circle cx="290" cy="27" r="7" fill="#e06020" stroke="#e06020" stroke-width="1.5"/>
  <text x="290" y="17" text-anchor="middle" fill="#e06020" font-size="11" font-family="sans-serif">global minimum</text>
  <circle cx="434" cy="69" r="6" fill="#2a7ae2" stroke="#2a7ae2" stroke-width="1.5"/>
  <text x="452" y="62" fill="#2a7ae2" font-size="11" font-family="sans-serif">good enough</text>
  <path d="M188,78 C202,74 216,68 229,62 C244,55 260,42 276,34" stroke="#333" stroke-width="1.8" fill="none" stroke-dasharray="5,3"/>
  <polygon points="276,34 268,43 282,42" fill="#333"/>
  <circle cx="188" cy="72" r="8" fill="#888"/>
  <line x1="184" y1="70" x2="192" y2="70" stroke="#f7f9fc" stroke-width="2"/>
  <text x="170" y="95" fill="#555" font-size="10" font-family="sans-serif" font-style="italic">you are here</text>
  <text x="350" y="184" text-anchor="middle" fill="#888" font-size="11" font-family="sans-serif">one dimension shown — real landscapes have billions</text>
</svg>

### 1.4.2 Backpropagation

To calculate the gradient across billions of parameters, the model uses a technique called **backpropagation** — sending the error signal backward through all the layers using the chain rule of calculus to determine how much each weight contributed to the loss.

Backpropagation exploits the fact that forward propagation is a composition of functions:

- Layer 1 applies **f(x)**
- Layer 2 applies **g(f(x))**
- Layer 3 applies **h(g(f(x)))**

The chain rule prescribes how to combine the derivatives of f, g, and h to compute the overall gradient. You compute the derivative of the outermost layer first, then propagate backward through each layer in turn. This calculation — performed billions of times across a vast training dataset — is what makes training so computationally demanding, requiring specialized hardware running for weeks or months.

In practice, **stochastic gradient descent** is used: rather than computing the gradient across the entire dataset before taking a single step, a step is taken after each small batch of examples. This is both computationally necessary and beneficial, because the noise in batch-by-batch updates helps the model avoid getting stuck in poor solutions.

## 1.5 Why Nvidia Is Worth Several Trillion Dollars

Nvidia makes graphics processing units (GPUs). When personal computers became common, people wanted to play video games. Compelling graphics required enormous amounts of computation performed in parallel. GPUs are designed to do exactly this: many simple operations simultaneously, on many inputs at once. A standard CPU can do the same computations, but largely one at a time. GPUs don't replace CPUs, because they don't handle **conditional branching** well — that is, "if the result of the previous operation is X, do the following; otherwise do Y." GPUs just execute a prescribed sequence of operations in parallel, which is fine for rendering pixels, and it turns out to be exactly what neural network training needs.

Nvidia made a good business supporting video gamers. Then AI came along and proved lucrative at an entirely different scale. Computing the gradient during training is extremely costly — especially for LLMs with hundreds of billions of weights, where the gradient must be computed for every weight, after every batch, for months. The GPUs in AI data centers run hot and wear out fast. The people running those data centers keep buying more.

---

# 2. Neural Networks for Visual Recognition

---

## 2.1 The Biological Foundation: Hubel and Wiesel

Before any computer scientist wrote a line of neural network code, two neurophysiologists at Harvard Medical School were recording electrical signals from individual neurons in the brains of anesthetized cats. **David Hubel** and **Torsten Wiesel** began this work in the late 1950s, and their discoveries won them the Nobel Prize in Physiology or Medicine in 1981.

Their key paper — *"Receptive fields, binocular interaction and functional architecture in the cat's visual cortex"* (*Journal of Physiology*, 1962) — built on their first publication from 1959 and remains one of the most cited papers in neuroscience. The experimental setup was elegant: project patterns of light onto a cat's retina and record which neurons in the visual cortex fire in response.

A famous discovery came almost by accident. As the story is usually told, Hubel and Wiesel had placed a small black dot on a glass slide, hoping it would excite cortical neurons the way spots of light excited retinal neurons. It largely did not. But the *edge* of the glass slide, as it was inserted into the projector at a particular angle, caused a neuron to fire dramatically. This led them to a foundational finding: cortical neurons respond not to spots of light, but to **oriented edges and bars**, and only when those stimuli appear at the right position and angle in the visual field.

### 2.1.1 Simple Cells and Complex Cells

Hubel and Wiesel identified two broad classes of neurons directly relevant to how we now build artificial visual systems.

**Simple cells** respond to an edge or bar of light at a specific orientation *and* a specific location in the visual field. Move the edge to a different part of the image, and the cell goes silent. Tilt the edge a few degrees from the cell's preferred orientation, and the response weakens. Each simple cell is, in effect, a very precise local detector.

**Complex cells** are one step more abstract. They also prefer edges at a specific orientation, but they respond to that edge *wherever* it appears within a broader region of the visual field. They have given up positional specificity in exchange for a kind of location tolerance.

This two-level hierarchy — precise local detectors feeding into more tolerant, abstract detectors — is not merely a curiosity of cat neuroanatomy. It became the architectural blueprint for convolutional neural networks.

## 2.2 How Visual Recognition Works: Channels and Layers

In visual recognition, an image is represented as a grid of pixels. For a color image, each pixel has three values — red, green, and blue intensity — so the input starts with **3 channels**: one feature map per color.

The first layer applies a set of learned filters to this input. Each filter is a small grid of weights that slides across the image (more on this below). Each filter produces a new feature map — a grid of numbers summarizing what that filter detected at each location. Where earlier there were 3 channels (RGB), there are now, say, 64 channels — each one a report about something the corresponding filter noticed at each position in the image.

In the early layers, those channels tend to encode simple things: a horizontal edge, a vertical edge, a diagonal edge, a particular color transition. In later layers, the channels encode more complex and less interpretable things — perhaps a texture, a repeated pattern, or a shape. The network discovers these representations on its own; nobody programs them in.

Because the number of channels multiplies at each layer, the representation grows very large. This is periodically compressed back down by **pooling** — a step that summarizes a small neighborhood of the feature map into a single value, reducing the spatial resolution while retaining the most important information. So the progression is: more channels (more information per location), but fewer spatial positions to track. Later layers have a compressed but richer representation of the image.

## 2.3 The Convolution Idea

### 2.3.1 Why Fully Connected Networks Fail on Images

Consider a modest 200×200 grayscale image: 40,000 pixels. If every pixel connects to every neuron in the next layer — a *fully connected* layer — and that layer has 1,000 neurons, we already have 40 million parameters in the first layer alone. This is computationally expensive, prone to overfitting, and fundamentally wasteful, because it ignores something obvious about images: **meaningful structure is local**.

A horizontal edge is defined by the relationship between a few neighboring pixels, not between a pixel in the top-left corner and one at the bottom-right. A cat's eye looks like a cat's eye whether it appears in the upper portion of the image or the lower. Fully connected networks have no way to exploit these properties without learning them redundantly for every position.

### 2.3.2 Filters and Weight Sharing

A **convolutional filter** (or kernel) is a small grid of weights — typically 3×3 or 5×5. Rather than connecting to the whole image, it slides across the image one small patch at a time. At each position, it computes a dot product between its weights and the underlying pixel values. The result is written into an output grid called a **feature map**.

Consider a simple 3×3 filter:

```
-1  -1  -1
 0   0   0
 1   1   1
```

Where this filter slides over a region where pixel values transition from dark (top) to bright (bottom), the dot product yields a large positive number — the filter "fires." Where the image is uniform, the result is near zero. This particular filter detects horizontal edges, and it does so *wherever they appear*, because the same weights slide across the entire image.

<svg viewBox="0 0 680 210" xmlns="http://www.w3.org/2000/svg" style="width:100%;max-width:680px;display:block;margin:1.2em 0">
  <rect width="680" height="210" fill="#f7f9fc" rx="6"/>
  <!-- Image patch (5x5 grid, dark top / light bottom) -->
  <g transform="translate(20,30)">
    <text x="60" y="-10" text-anchor="middle" fill="#555" font-size="12" font-family="sans-serif">Image patch</text>
    <!-- row 1 dark -->
    <rect x="0"  y="0" width="24" height="24" fill="#222"/><rect x="24" y="0" width="24" height="24" fill="#1a1a1a"/><rect x="48" y="0" width="24" height="24" fill="#1e1e1e"/><rect x="72" y="0" width="24" height="24" fill="#222"/><rect x="96" y="0" width="24" height="24" fill="#1e1e1e"/>
    <!-- row 2 dark -->
    <rect x="0"  y="24" width="24" height="24" fill="#1e1e1e"/><rect x="24" y="24" width="24" height="24" fill="#222"/><rect x="48" y="24" width="24" height="24" fill="#1a1a1a"/><rect x="72" y="24" width="24" height="24" fill="#1e1e1e"/><rect x="96" y="24" width="24" height="24" fill="#222"/>
    <!-- row 3 mid (transition) -->
    <rect x="0"  y="48" width="24" height="24" fill="#777"/><rect x="24" y="48" width="24" height="24" fill="#888"/><rect x="48" y="48" width="24" height="24" fill="#808080"/><rect x="72" y="48" width="24" height="24" fill="#888"/><rect x="96" y="48" width="24" height="24" fill="#777"/>
    <!-- row 4 light -->
    <rect x="0"  y="72" width="24" height="24" fill="#ccc"/><rect x="24" y="72" width="24" height="24" fill="#ddd"/><rect x="48" y="72" width="24" height="24" fill="#d8d8d8"/><rect x="72" y="72" width="24" height="24" fill="#ddd"/><rect x="96" y="72" width="24" height="24" fill="#ccc"/>
    <!-- row 5 bright -->
    <rect x="0"  y="96" width="24" height="24" fill="#eee"/><rect x="24" y="96" width="24" height="24" fill="#f0f0f0"/><rect x="48" y="96" width="24" height="24" fill="#eee"/><rect x="72" y="96" width="24" height="24" fill="#f0f0f0"/><rect x="96" y="96" width="24" height="24" fill="#eee"/>
    <!-- highlight the 3x3 window (rows 2-4, cols 2-4) -->
    <rect x="24" y="24" width="72" height="72" fill="none" stroke="#2a7ae2" stroke-width="2.5" stroke-dasharray="6,3"/>
    <!-- grid lines -->
    <rect x="0" y="0" width="120" height="120" fill="none" stroke="#bbb" stroke-width="0.5"/>
    <line x1="24" y1="0" x2="24" y2="120" stroke="#bbb" stroke-width="0.5"/>
    <line x1="48" y1="0" x2="48" y2="120" stroke="#bbb" stroke-width="0.5"/>
    <line x1="72" y1="0" x2="72" y2="120" stroke="#bbb" stroke-width="0.5"/>
    <line x1="96" y1="0" x2="96" y2="120" stroke="#bbb" stroke-width="0.5"/>
    <line x1="0" y1="24" x2="120" y2="24" stroke="#bbb" stroke-width="0.5"/>
    <line x1="0" y1="48" x2="120" y2="48" stroke="#bbb" stroke-width="0.5"/>
    <line x1="0" y1="72" x2="120" y2="72" stroke="#bbb" stroke-width="0.5"/>
    <line x1="0" y1="96" x2="120" y2="96" stroke="#bbb" stroke-width="0.5"/>
    <text x="60" y="138" text-anchor="middle" fill="#777" font-size="11" font-family="sans-serif">dark → light (edge)</text>
  </g>
  <!-- Arrow -->
  <line x1="152" y1="100" x2="192" y2="100" stroke="#555" stroke-width="1.5"/>
  <polygon points="192,100 184,95 184,105" fill="#555"/>
  <!-- Filter matrix -->
  <g transform="translate(198,30)">
    <text x="52" y="-10" text-anchor="middle" fill="#2a7ae2" font-size="12" font-family="sans-serif">3×3 filter (9 weights)</text>
    <rect x="0" y="0" width="104" height="104" rx="4" fill="#fff" stroke="#2a7ae2" stroke-width="1.5"/>
    <text x="52" y="26"  text-anchor="middle" fill="#c0392b" font-size="14" font-family="monospace" font-weight="bold">−1  −1  −1</text>
    <line x1="6" y1="38" x2="98" y2="38" stroke="#ddd" stroke-width="1"/>
    <text x="52" y="60"  text-anchor="middle" fill="#888" font-size="14" font-family="monospace"> 0   0   0</text>
    <line x1="6" y1="72" x2="98" y2="72" stroke="#ddd" stroke-width="1"/>
    <text x="52" y="94"  text-anchor="middle" fill="#27ae60" font-size="14" font-family="monospace" font-weight="bold">+1  +1  +1</text>
    <text x="52" y="124" text-anchor="middle" fill="#888" font-size="11" font-family="sans-serif">slides across entire image</text>
  </g>
  <!-- Arrow -->
  <line x1="314" y1="100" x2="354" y2="100" stroke="#555" stroke-width="1.5"/>
  <polygon points="354,100 346,95 346,105" fill="#555"/>
  <!-- Feature map -->
  <g transform="translate(360,30)">
    <text x="60" y="-10" text-anchor="middle" fill="#555" font-size="12" font-family="sans-serif">Feature map output</text>
    <rect x="0"  y="0"  width="24" height="24" fill="#e8e8e8"/><rect x="24" y="0"  width="24" height="24" fill="#e8e8e8"/><rect x="48" y="0"  width="24" height="24" fill="#e8e8e8"/>
    <rect x="0"  y="24" width="24" height="24" fill="#f5a623" stroke="#bbb" stroke-width="0.5"/>
    <rect x="24" y="24" width="24" height="24" fill="#f5a623" stroke="#bbb" stroke-width="0.5"/>
    <rect x="48" y="24" width="24" height="24" fill="#f5a623" stroke="#bbb" stroke-width="0.5"/>
    <rect x="0"  y="48" width="24" height="24" fill="#e8e8e8"/><rect x="24" y="48" width="24" height="24" fill="#e8e8e8"/><rect x="48" y="48" width="24" height="24" fill="#e8e8e8"/>
    <rect x="0" y="0" width="72" height="72" fill="none" stroke="#bbb" stroke-width="0.5"/>
    <line x1="24" y1="0" x2="24" y2="72" stroke="#bbb" stroke-width="0.5"/>
    <line x1="48" y1="0" x2="48" y2="72" stroke="#bbb" stroke-width="0.5"/>
    <line x1="0" y1="24" x2="72" y2="24" stroke="#bbb" stroke-width="0.5"/>
    <line x1="0" y1="48" x2="72" y2="48" stroke="#bbb" stroke-width="0.5"/>
    <text x="36" y="90"  text-anchor="middle" fill="#888" font-size="11" font-family="sans-serif">≈ 0 (uniform)</text>
    <text x="36" y="106" text-anchor="middle" fill="#f5a623" font-size="11" font-family="sans-serif" font-weight="bold">high → edge!</text>
    <text x="36" y="122" text-anchor="middle" fill="#888" font-size="11" font-family="sans-serif">≈ 0 (uniform)</text>
  </g>
</svg>

This is called **weight sharing**: instead of 40 million parameters for the first layer, a single 3×3 filter has just 9. In a network with many filters per layer, this is an enormous reduction in complexity — and a direct computational analog of Hubel and Wiesel's simple cells.

**Pooling layers** then play the role of complex cells: they summarize filter responses over a small neighborhood, introducing tolerance to small shifts in position.

### 2.3.3 Learned Feature Hierarchies

In a deep convolutional network, you use not one filter but many — typically dozens per layer — and you stack multiple layers. The key insight is that you do not design these filters by hand. Backpropagation learns them from data. And what the network learns, reliably and across many different architectures, mirrors the biological hierarchy Hubel and Wiesel described:

- **Early layers** learn low-level features: oriented edges, color gradients, simple textures
- **Middle layers** combine these into corners, curves, and simple shapes
- **Later layers** respond to complex patterns: eyes, wheels, faces, entire objects

The convolutional architecture encodes a useful *inductive bias* — a built-in assumption that visual patterns are local and repeatable — rather than forcing the network to discover this from scratch. It is the right architecture for images precisely because it mirrors the actual structure of visual information.

---

## 2.4 LeCun and the First Practical Success

The most famous early application of convolutional networks came from **Yann LeCun** at Bell Labs in the late 1980s and early 1990s. LeCun developed **LeNet**, a convolutional neural network trained to recognize handwritten digits, which the United States Postal Service deployed to automatically sort mail by reading ZIP codes.

This was remarkable for several reasons. First, it was a *real-world deployment* of neural networks at a time when they were largely academic curiosities. Second, it demonstrated end-to-end training: rather than hand-engineering features and feeding them to a classifier, the entire network — convolutional layers, pooling layers, and final classification — was trained jointly from raw pixel values to digit labels, via backpropagation. (Backpropagation itself had been developed and popularized somewhat earlier, by Rumelhart, Hinton, and Williams in 1986.)

The dataset used, **MNIST**, consists of 70,000 28×28 grayscale images of handwritten digits (0–9). It remains a standard benchmark to this day. Someone with a few hours and basic Python knowledge can build a network that achieves over 98% accuracy on MNIST — experiencing, in compressed form, exactly what LeCun accomplished.

The conceptual shift LeNet embodied — from engineered features to *learned* features — is arguably the central idea of the entire deep learning era. Before LeNet, computer vision required human experts to write rules: look for this kind of edge here, this kind of curve there. LeNet demonstrated that a network could discover its own features, and that those learned features could be more powerful than anything hand-crafted.

---

## 2.5 The Dark Years and the Comeback: Hinton and Deep Belief Networks

LeNet was a proof of concept, but through the 1990s and 2000s neural networks lost ground to other methods for most practical tasks. The core problem was depth. Backpropagation worked well for shallow networks, but training networks with many layers ran into two serious obstacles:

**Vanishing gradients**: The error signal propagated backward through many layers shrinks exponentially. By the time it reaches the early layers, it is essentially zero. Those layers do not learn.

**Poor initialization**: Networks initialized with random weights would get stuck in bad regions of the loss landscape and fail to train effectively.

The result was a practical ceiling on the number of layers that could be usefully trained, which in turn limited the complexity of features the network could learn.

### 2.5.1 Boltzmann Machines and the Energy Landscape

**Geoffrey Hinton** (along with colleagues including Ruslan Salakhutdinov) introduced a different approach in a landmark 2006 paper: training **Deep Belief Networks** by stacking **Restricted Boltzmann Machines** (RBMs). Hinton later shared the 2024 Nobel Prize in Physics — with John Hopfield — for foundational contributions to neural networks broadly. The physics connection is real: the Boltzmann machine borrows the mathematical framework of thermodynamics, modeling a network's state in terms of an energy landscape analogous to that used in statistical mechanics.

### 2.5.2 Layer-Wise Pretraining

Hinton's crucial insight was to train a Deep Belief Network greedily, one layer at a time:

1. Train an RBM on the raw input data. It learns first-level features.
2. Treat the hidden activations of that RBM as input data, and train a new RBM on top. It learns second-level features.
3. Repeat for as many layers as desired.
4. Fine-tune the whole stack jointly using backpropagation.

This **layer-wise pretraining** solved the initialization problem. Each layer arrives at the fine-tuning stage already encoding meaningful structure, rather than starting from random noise. The error signal from backpropagation then had a much shorter, well-prepared path to travel.

More importantly, this work demonstrated that deep networks — networks with many layers — could be trained successfully, and that they learned qualitatively richer representations than shallow ones. At a moment when much of the field had given up on depth, Hinton's paper reopened the question.

### 2.5.3 The Successor Technologies

RBMs and Deep Belief Networks were fairly short-lived as the dominant approach. Within a few years, researchers found that the training problems Hinton had solved with pretraining could be addressed more simply through:

- **ReLU activations** — ReLU stands for Rectified Linear Unit. It is a simple activation function: for any negative input value, output zero; for any positive value, output the value as-is. This turns out to resist the vanishing gradient problem far better than earlier activation functions did.
- **Better weight initialization** schemes — choosing a better starting distribution for the randomly assigned weights, so the network begins in a more tractable region of the loss landscape.
- **Dropout regularization** — When a neural network learns to recognize patterns too narrowly — only when they match the training data almost exactly — that is called **overfitting**. Dropout addresses this by randomly disabling some neurons during each training pass, forcing the network to learn more robust, generalizable representations.

These ingredients, combined with large datasets and GPU computing power, produced **AlexNet** in 2012 — a deep convolutional network trained on the ImageNet dataset of 1.2 million images that dramatically outperformed all other entries in that year's ImageNet competition. AlexNet used none of the Boltzmann machinery. But it would not have been built without the conceptual groundwork Hinton's work had laid: the conviction that depth was the right direction, and that learned hierarchical representations were worth pursuing.

---

## 2.6 The Arc of the Story

Tracing this history reveals a coherent set of ideas that have persisted from Hubel and Wiesel's cat experiments to today's vision transformers:

**Local structure matters.** Visual features are defined by relationships between nearby pixels, not distant ones. This insight, first demonstrated neurophysiologically, is encoded in the convolutional layer.

**Hierarchies of abstraction.** The visual system — biological and artificial — builds complex representations by composing simpler ones. Edges combine into shapes; shapes combine into objects. This principle runs from simple and complex cells through LeNet to ResNet and beyond.

**Features should be learned.** Rather than hand-crafting intermediate representations, we should provide the network with enough data and capacity and let it discover the representations that work. LeCun demonstrated this for convolutional networks; the deep learning era has confirmed it at every scale since.

**Depth is essential.** Hinton's contribution was to show, at a moment of skepticism, that deep networks could be trained and that they learned qualitatively richer representations than shallow ones. The specific mechanism he used is less important than the door it reopened.

These ideas, rooted partly in biology, partly in mathematics, and partly in the pragmatic engineering of early systems like LeNet, form the conceptual foundation of virtually all modern visual AI.

---

## 2.7 Further Exploration

Anyone interested in building their own digit-recognition network can start with the **3Blue1Brown neural networks series**, which provides beautiful visual explanations alongside an interactive MNIST demo:

- [3Blue1Brown: But what is a Neural Network?](https://www.3blue1brown.com/lessons/neural-networks)

For a hands-on coding introduction, good starting points include:

- Michael Nielsen's free online book *Neural Networks and Deep Learning*, which builds MNIST from scratch in Python and NumPy
- The TensorFlow.js MNIST codelab, which runs entirely in the browser with no installation required
- The DigitalOcean tutorials for building the same network in either TensorFlow or PyTorch

You can do this on your laptop — no data center required. Your neural network might be able to recognize handwritten numbers, but probably not cats. Is anyone in this group that nerdy? Even if not, the 3Blue1Brown video linked above is worth an hour of anyone's time.

The original Hubel and Wiesel papers are freely accessible and surprisingly readable. Their 1959 paper — *"Receptive fields of single neurones in the cat's striate cortex"* (*Journal of Physiology* 148, 574–591) — is a model of careful experimental science and worth at least a browse for anyone curious about the biological origins of these ideas.

---
# 3. Large Language Models: The Birth of the AI Chatbot

---

## 3.1 Language Is Hard

Language conveys the patterns of thought — or at least the patterns of verbal thought. It is inherently complicated. Consider the web of meaning around the word "dog." Related words include: puppy, hound, mammal, carnivore, bite, run, pant, pet. Now consider a sentence. Is "dog" the subject or the object? If "it" appears later, does it refer to the dog or something else in the sentence? How does "brown dog" differ from just "dog"? If the word "May" appears, is it the month, a person's name, or the modal verb, as in "may go"? In a typical paragraph, many words interact to construct the meaning being conveyed.

These problems were sticky. It took a long time to figure them out. The critical moment was the 2017 publication of "Attention Is All You Need" by Ashish Vaswani and other researchers at Google. What they came up with is complicated, and it is not obvious how they derived these ideas — researchers proceeded by intuition and experiment as much as by analysis. What follows is a description of the architecture that paper introduced.

---

## 3.2 Tokens — What the Model Reads

When a large language model reads text, it does not read words the way you do, and it does not read letter by letter either. Instead it breaks text into chunks called **tokens**.

Why not whole words? English alone contains hundreds of thousands of words — and that is before adding slang, technical terms, foreign words, misspellings, and new coinages. A dictionary large enough to cover everything would be unmanageably large, and the model would struggle with any word it had never seen before, or seen too rarely to learn from.

Why not single letters? Letters carry almost no meaning on their own. The letter "b" tells you almost nothing. Processing text one letter at a time would be like trying to understand a painting one brushstroke at a time.

Tokens are a middle ground. A typical model uses a vocabulary of roughly 50,000 to 100,000 tokens — a manageable number that can represent virtually any text. Common words like "the" or "cat" become a single token. Less common words get broken into meaningful pieces: "unbelievable" might become "un," "believ," and "able." Punctuation and spaces are tokens too.

Notice that some tokens are whole words, some are word-fragments that carry meaning (prefixes like "un-" or "pre-," suffixes like "-ing"), and some are punctuation or numbers. The model may never have seen the word "unbelievable" — but because it knows "un-," "believ," and "-able" from thousands of other words, it can handle it anyway.

This also explains a curious limitation: if you ask a model to count the letters in *strawberry*, it may get it wrong. The model never sees individual letters — it sees tokens like "straw" and "berry," and has to reason about the letters inside them indirectly. It often fails at exactly these simple character-level tasks, while succeeding at far more complex ones. (Newer models with extended reasoning have improved on this specific weakness, but it remains a useful illustration of how tokenization shapes the model's perception of text.)

### 3.2.1 How Tokens Are Chosen: Byte Pair Encoding

The tokenization process is not arbitrary. Before a model is trained, a separate **tokenizer training phase** runs on a large corpus of text to determine the optimal vocabulary, using an algorithm called **Byte Pair Encoding (BPE)**. The process begins with individual characters, then iteratively merges the most frequent adjacent pairs — "t" and "h" merge to "th," then "th" and "e" to "the," and so on — until a target vocabulary size is reached, typically between 32,000 and 128,000 tokens. This produces a vocabulary that represents common words as single tokens and rare words as sequences of meaningful fragments.

English can be represented fairly well using a dictionary of 30,000 to 50,000 tokens. A dictionary of 150,000 tokens seems to suffice for all languages that are common on the Internet. LLMs do not perform as well on languages that appear infrequently in the training data.

Once tokenized, each token is assigned a unique identification number. From this point on, the model works entirely with numbers, not text. The tokenizing step uses no neural network — it is a one-time statistical analysis of all the training text, done before training begins.

For an image, each pixel is associated with a position in the first layer of the model. For a text prompt passed to an LLM, each token in the prompt is associated with a position.

---

## 3.3 Embeddings: From Token Numbers to Vectors

Tokens cannot be fed directly into a neural network as bare ID numbers, because those numbers have no meaningful numeric relationship to one another. Token #4271 is not "more than" or "close to" token #4270 in any useful sense. The first layer of an LLM must therefore construct a richer representation.

This is done via an **embedding layer**. Each token ID is looked up in a learned table, and the result is a vector — a list of hundreds or thousands of floating-point numbers. In many models, a typical embedding vector is about 4,000 numbers long. Unlike pixel values, which are read directly from the image, these embedding vectors are **learned during training**. The numbers in the vector are initially assigned entirely randomly. Through training, the vectors adjust so that tokens with similar meanings end up with similar vectors — geometrically close to each other in the high-dimensional space the vectors inhabit. So "king" and "queen" end up closer together than "king" and "bicycle."

This is a fundamental difference from visual recognition: pixel values describe physical reality directly, while embedding vectors describe relational patterns — and the network figures out what those relationships should be through training.

One note on the word "semantic": you will sometimes hear these called semantic relationships, meaning relationships of meaning. That word is used loosely here. A more precise term is **distributional**: the relationships reflect how words distribute across the patterns of observed language, not any grounding in real-world objects. An LLM has no direct knowledge of the physical world. It knows "dog" relates to "puppy" and "bark" because those words co-occur in similar contexts across billions of sentences — not because the model has ever encountered a dog.

---

## 3.4 Positional Encoding

An embedding vector captures what a token means, but not where it appears in the sequence. The word "not" means something very different at different positions in a sentence. LLMs need to encode this positional information explicitly.

For each position in the sequence, a **positional encoding vector** is computed and added element-wise to the token's embedding vector. The result is a single combined vector per token that encodes both identity and position.

The original scheme, introduced in "Attention Is All You Need," uses sine and cosine functions at different frequencies to generate the positional vectors — with an intuitive resemblance to a Fourier decomposition. Low-frequency components capture broad positional information (early versus late in the sequence), while high-frequency components capture fine-grained position (the exact slot). A useful analogy is a clock: the second hand, minute hand, and hour hand each complete their cycles at different rates, and together they encode time unambiguously. The sinusoidal positional encoding does the same thing across the dimensions of the vector.

An important property of this scheme is that it preserves information about relative distance between tokens — the network can recover not just where each token is, but how far apart any two tokens are, which is valuable for understanding grammatical and semantic relationships.

It is worth noting that virtually all modern LLMs have replaced this original sinusoidal scheme with learned variants — most commonly **Rotary Position Embedding (RoPE)** — which handle longer sequences more effectively. But the core idea of injecting positional information into the token vectors is the same.

After combining embeddings and positional encodings, the result is a set of N vectors — one per token in the prompt — which serves as the starting state for the transformer.

---

## 3.5 The Attention Mechanism

The attention mechanism is the heart of the transformer. It allows every token to gather information from every other token in the sequence, so that each token's representation can reflect its full context.

(Attention-based mechanisms have now also largely displaced convolutional networks for visual recognition. They can detect relationships across an entire image rather than being restricted to local pixel neighborhoods. The hooves of a horse may be far from its head in an image, but they are related in determining what the image represents — attention can capture that connection.)

### 3.5.1 Queries, Keys, and Values

Each token's vector is transformed into three derived vectors through learned weight matrices:

- **Query (Q):** what this token is looking for
- **Key (K):** what this token advertises about itself
- **Value (V):** what this token will contribute if selected

These are simply linear transformations — matrix multiplications — and the Q, K, and V vectors are typically lower-dimensional than the original input vectors.

These matrices, like all the others in the model, begin with entirely random values. They are weights — parameters of the model — and their values are adjusted during training by gradient descent. This is one of the places where the parameter count accumulates quickly: every attention layer, every head within that layer, has its own Q, K, and V matrices.

### 3.5.2 Computing Attention Scores

For each token, its Q vector is compared against the K vector of every other token (including itself) by computing the dot product. A high dot product indicates that the two tokens are highly relevant to each other. This produces a matrix of scores — every token against every token.

The scores are scaled by dividing by the square root of the vector dimension, to prevent the values from growing too large. They are then passed through a softmax function, which converts them into weights that sum to 1 — a learned probability distribution over the sequence.

### 3.5.3 Causal Masking

In a language model used for text generation, there is a critical constraint: when predicting the next token, the model must not be allowed to "look ahead" at tokens that haven't been generated yet. This is enforced by **causal masking** — before the softmax step, all attention scores pointing to future positions in the sequence are set to negative infinity, so that the softmax produces zero weight for those positions. Each token can only attend to itself and the tokens before it. This is what makes it possible to train the model on complete sentences while still having it learn to predict one token at a time.

### 3.5.4 Producing the Output

Each token's output vector is computed as a weighted sum of all the Value vectors, where the weights are the attention scores just computed. A token's output is therefore dominated by the Value vectors of whichever tokens it attended to most strongly. This is how "bank" in "river bank" learns to attend to "river" and update its representation accordingly.

<svg viewBox="0 0 680 200" xmlns="http://www.w3.org/2000/svg" style="width:100%;max-width:680px;display:block;margin:1.2em 0">
  <rect width="680" height="200" fill="#f7f9fc" rx="6"/>
  <!-- Token boxes -->
  <rect x="16"  y="30" width="62" height="30" rx="4" fill="#e8f0ff" stroke="#5599cc" stroke-width="1.5"/>
  <text x="47"  y="50" text-anchor="middle" fill="#333" font-size="13" font-family="sans-serif">She</text>
  <rect x="90"  y="30" width="62" height="30" rx="4" fill="#e8f0ff" stroke="#5599cc" stroke-width="1.5"/>
  <text x="121" y="50" text-anchor="middle" fill="#333" font-size="13" font-family="sans-serif">went</text>
  <rect x="164" y="30" width="62" height="30" rx="4" fill="#e8f0ff" stroke="#5599cc" stroke-width="1.5"/>
  <text x="195" y="50" text-anchor="middle" fill="#333" font-size="13" font-family="sans-serif">to</text>
  <rect x="238" y="30" width="62" height="30" rx="4" fill="#e8f0ff" stroke="#aaa" stroke-width="1.5"/>
  <text x="269" y="50" text-anchor="middle" fill="#888" font-size="13" font-family="sans-serif">the</text>
  <rect x="312" y="30" width="62" height="30" rx="4" fill="#fff3cd" stroke="#c87800" stroke-width="2.5"/>
  <text x="343" y="50" text-anchor="middle" fill="#7a4800" font-size="13" font-family="sans-serif" font-weight="bold">bank</text>
  <rect x="386" y="30" width="62" height="30" rx="4" fill="#e8f0ff" stroke="#aaa" stroke-width="1.5"/>
  <text x="417" y="50" text-anchor="middle" fill="#888" font-size="13" font-family="sans-serif">by</text>
  <rect x="460" y="30" width="62" height="30" rx="4" fill="#e8ffe8" stroke="#2a7a2a" stroke-width="2.5"/>
  <text x="491" y="50" text-anchor="middle" fill="#1a4a1a" font-size="13" font-family="sans-serif" font-weight="bold">river</text>
  <!-- Strong attention arc: bank → river -->
  <path d="M343,30 C343,0 491,0 491,30" stroke="#2a7a2a" stroke-width="2.5" fill="none"/>
  <polygon points="491,30 484,22 497,22" fill="#2a7a2a"/>
  <text x="417" y="10" text-anchor="middle" fill="#2a7a2a" font-size="11" font-family="sans-serif" font-weight="bold">strong attention — disambiguates "bank"</text>
  <!-- Weak attention arc: bank → went (dashed) -->
  <path d="M343,30 C330,12 134,12 121,30" stroke="#aaa" stroke-width="1" fill="none" stroke-dasharray="4,3"/>
  <text x="232" y="18" text-anchor="middle" fill="#aaa" font-size="10" font-family="sans-serif">weak</text>
  <!-- Q K V legend -->
  <rect x="16" y="100" width="200" height="86" rx="4" fill="#fff" stroke="#ddd" stroke-width="1"/>
  <text x="116" y="118" text-anchor="middle" fill="#555" font-size="12" font-family="sans-serif" font-weight="bold">For each token:</text>
  <text x="26" y="138" fill="#333" font-size="12" font-family="sans-serif"><tspan fill="#c87800" font-weight="bold">Q</tspan> = what this token is looking for</text>
  <text x="26" y="157" fill="#333" font-size="12" font-family="sans-serif"><tspan fill="#2a7a2a" font-weight="bold">K</tspan> = what this token offers</text>
  <text x="26" y="176" fill="#333" font-size="12" font-family="sans-serif"><tspan fill="#2a7ae2" font-weight="bold">V</tspan> = what this token contributes</text>
  <!-- Causal masking box -->
  <rect x="232" y="100" width="210" height="86" rx="4" fill="#fff" stroke="#e05c5c" stroke-width="1"/>
  <text x="337" y="120" text-anchor="middle" fill="#e05c5c" font-size="12" font-family="sans-serif" font-weight="bold">Causal masking (generation)</text>
  <text x="242" y="140" fill="#555" font-size="11" font-family="sans-serif">Each token attends only to</text>
  <text x="242" y="157" fill="#555" font-size="11" font-family="sans-serif">itself and earlier tokens.</text>
  <text x="242" y="174" fill="#555" font-size="11" font-family="sans-serif">No peeking at future tokens.</text>
  <!-- Multi-head box -->
  <rect x="458" y="100" width="206" height="86" rx="4" fill="#fff" stroke="#7b68ee" stroke-width="1"/>
  <text x="561" y="120" text-anchor="middle" fill="#7b68ee" font-size="12" font-family="sans-serif" font-weight="bold">Multi-head attention</text>
  <text x="468" y="140" fill="#555" font-size="11" font-family="sans-serif">Run in parallel many times,</text>
  <text x="468" y="157" fill="#555" font-size="11" font-family="sans-serif">each with different Q, K, V.</text>
  <text x="468" y="174" fill="#555" font-size="11" font-family="sans-serif">Each head learns different relations.</text>
</svg>

### 3.5.5 Multi-Head Attention

Rather than performing this process once, the transformer performs it multiple times in parallel — each time using different learned Q, K, V matrices. Each parallel run is called an **attention head**, and different heads can learn to attend to different kinds of relationships: syntactic structure, semantic similarity, coreference, and so on.

The outputs of all heads are concatenated and then projected back to the original vector dimension via another learned matrix. The dimensionality entering and leaving the multi-head attention block is therefore the same.

---

## 3.6 The Feed-Forward Layer

After the attention step, each token has gathered contextual information from across the sequence. But the attention mechanism is essentially a weighted averaging operation — good at routing information between tokens, but limited in its ability to transform that information in complex, nonlinear ways. The feed-forward layer provides that transformative capacity.

Each token's vector is passed independently through a small neural network consisting of two linear transformations with a nonlinearity between them. Crucially, there is **no communication between tokens** at this stage — each token is processed entirely on its own.

### 3.6.1 The Expansion and Compression

The first linear transformation projects each vector into a higher-dimensional space — in the original "Attention Is All You Need" paper, four times larger. This expansion provides more "analysis knobs" for the network to work with, giving it room to capture subtle distinctions in meaning that would be lost in a lower-dimensional representation.

The nonlinearity — typically ReLU, which sets any negative value to zero — is essential. Without it, stacking linear transformations one after another would be mathematically equivalent to a single linear transformation, no matter how many layers you added. The nonlinearity breaks this collapse by allowing different neurons to switch on or off depending on the input, creating piecewise behavior — the kind that sharp, conditional, threshold-like relationships require.

The second linear transformation then projects back down to the original vector dimension: a learned compression that decides what to preserve and what to discard from the richer intermediate representation.

### 3.6.2 Residual Connections and Normalization

After both the attention block and the feed-forward block, the original input vector is added back to the output — a **residual connection**. This means the network learns adjustments and refinements to the representation rather than recomputing it from scratch, which makes training much more stable. A Layer Normalization step follows, adjusting the values in each vector to a consistent scale to prevent any single dimension from dominating.

The full sequence within each transformer layer is therefore:

1. Multi-head attention (with causal masking)
2. Add residual + normalize
3. Feed-forward expand (linear)
4. Nonlinearity (ReLU)
5. Feed-forward compress (linear)
6. Add residual + normalize

A clean way to summarize the division of labor: **attention handles communication between tokens** — which tokens should influence which — while the **feed-forward layer handles computation within each token** — what to do with the information once gathered.

---

## 3.7 Stacking Layers

The block described above — attention followed by feed-forward, with residual connections and normalization — constitutes one transformer layer. In practice this block is stacked many times. The original "Attention Is All You Need" paper used 6 layers; modern large models use far more.

The number of layers, the vector dimension size, and the number of attention heads are the three main dials for scaling up a model, and together they largely determine the total parameter count. As a rough guide:

| Model | Layers |
|---|---|
| GPT-2 (largest version) | 48 |
| GPT-3 | 96 |
| LLaMA 2 70B | 80 |
| Frontier models (GPT-4, Claude, Gemini) | Not disclosed; estimated 100–200 |

Each layer refines the token representations further. Early layers tend to capture syntactic and local relationships; later layers capture more abstract and long-range relationships — loosely analogous to how early layers in visual recognition detect edges while later layers detect objects.

---

## 3.8 Training and Gradient Descent

The architecture — number of layers, vector dimensions, attention heads — is fixed before training begins. What training adjusts is exclusively the **weights**: all the learned matrices for embeddings, Q/K/V projections, feed-forward transformations, and so on.

LLMs are trained on vast quantities of text from the Internet. This is self-supervised training, as described in Section 1.3: nothing is labeled up front. The model is simply shown enormous amounts of text and trained to predict the next token at every position. The correct answer is always available — it is the actual next token in the text — so no human annotation is needed.

Training proceeds by gradient descent:

1. Feed a training example through the network (the forward pass)
2. Compare the output to the correct answer using the loss function — for LLMs, typically how well the model predicted the next token
3. Compute the gradient — how much each weight contributed to the error
4. Nudge every weight slightly in the direction that reduces the loss (the backward pass, via backpropagation)
5. Repeat billions of times across an enormous dataset

The backward pass is roughly twice as expensive as the forward pass, making training significantly more costly than inference. This is why training frontier models requires thousands of GPUs running for months, at a cost of tens or hundreds of millions of dollars.

The residual connections play an important role early in training: when the learned transformations are still essentially random noise, the signal flows through the residual connections largely unchanged, and the network effectively behaves like a shallower model. The layers gradually learn to contribute useful transformations as training progresses.

---

## 3.9 Fine-Tuning: RLHF and LoRA

After pre-training, a model can predict the next token with impressive fluency — but it has no particular goal. It will continue text in a statistically plausible direction, but it will not reliably complete a task, answer a question helpfully, or avoid harmful outputs. Fine-tuning shapes the model's behavior toward being useful.

### 3.9.1 Reinforcement Learning from Human Feedback (RLHF)

The primary method for aligning a pre-trained LLM with human preferences is **Reinforcement Learning from Human Feedback (RLHF)**. The process has three stages:

1. **Supervised fine-tuning**: Human trainers write examples of ideal responses to a variety of prompts. The model is fine-tuned on these examples to begin steering its behavior in the right direction.
2. **Reward model training**: Human raters compare pairs of model outputs and indicate which they prefer. A separate neural network — the reward model — is trained to predict these preferences, effectively learning to score outputs as a human rater would.
3. **Reinforcement learning**: The main model is further trained to maximize the reward model's scores on its outputs. This is what shapes the model toward helpfulness, accuracy, and appropriate limits.

Fine-tuning steers the model to:

- Complete the task — answering a question, writing code, summarizing a document, or whatever else is asked.
- Seem helpful and friendly. The companies deploying these systems want people to find them pleasant to use.
- Avoid dangerous outputs. Not helping someone build weapons of mass destruction, not generating content that exploits children, and so on. These are the so-called "guardrails." They are imperfect — they can be circumvented with sufficient effort — and improving them is an active area of research.

### 3.9.2 LoRA: Fine-Tuning Without Breaking the Model

The challenge of fine-tuning is doing it without destabilizing the vast knowledge encoded in the pre-trained weights. If you simply retrain the whole model on fine-tuning data, you risk overwriting what the model already knows.

The most widely used solution is **LoRA** (Low-Rank Adaptation). Rather than modifying the original weight matrices directly, LoRA freezes all pre-trained weights and adds a small parallel structure alongside each matrix it targets.

The mechanism is elegant. Instead of adding a full-sized matrix — which would have as many parameters as the original — LoRA adds two much smaller matrices A and B, where A is tall and thin and B is short and wide. Their product A×B has the same dimensions as the original weight matrix but far fewer parameters, because the rank of the product is much smaller than the full matrix. This is the "low rank" in LoRA.

At the start of fine-tuning, A and B are initialized so that their product is zero — meaning the modification has no effect. Only A and B are updated during fine-tuning; the original matrix remains frozen. The effective weight used in the forward pass is the original matrix plus A×B.

LoRA is typically applied to the Q and V matrices in the attention mechanism, based on the intuition that these matrices most directly control what the model pays attention to, and are therefore the highest-leverage targets for behavioral adjustment.

---

## 3.10 Reasoning

"Reasoning" in modern LLMs refers to a technique applied at inference time, not during training. The core idea is **chain-of-thought**: rather than jumping straight to a final answer, the model generates a sequence of intermediate tokens — visible working steps — before producing its response.

This works because each token the model generates becomes part of the context for generating the next token. By writing out intermediate steps, the model effectively gives itself scratch paper: each step can build on the previous ones, allowing it to tackle problems too complex to solve in a single pass.

More sophisticated variants go beyond linear chains of thought. **Beam search** keeps multiple candidate sequences in play simultaneously, pruning low-probability branches as generation proceeds. **Tree search** allows genuine backtracking — exploring a branching space of reasoning paths and abandoning dead ends. **Self-consistency** generates multiple independent reasoning chains for the same problem and takes a majority vote on the final answer, exploiting the fact that correct reasoning paths tend to converge even when they differ in their route.

The key insight is that reasoning is not a new mechanism but a clever exploitation of the existing token-by-token generation process: using the model's own output as extended context for continued computation. The cost is real, however. Before chain-of-thought reasoning, generating an answer required little GPU work at inference time — almost all the heavy computation had already been done during training. Reasoning models generate many more tokens per query, making everyday use significantly more GPU-intensive as well.

---

## 3.11 An Aside: The Chinese Strategy

Various Chinese companies and academic groups are competing with US companies for AI leadership. During the Biden administration, this competition was seen as a security concern, and the sale of the most powerful GPU chips to Chinese entities was restricted.

This approach may not have had the intended effect. Chinese developers could still rent time on data centers outside China. In any case, the Trump administration subsequently eased those restrictions.

What happened next was instructive. The Chinese largely did not rush to buy the newly available chips — for two reasons. First, they are making substantial progress developing their own AI chips and want strong domestic expertise in that area. Second, rather than competing by dedicating ever more electricity and hardware to training, they focused on making the process more efficient. The DeepSeek LLM, released by a Chinese group in early 2025, produced results competitive with the best American models at a fraction of the development cost — a significant demonstration that raw compute is not the only path to capable AI.

---
# 4. A Taxonomy of Neural Network Architectures

---

The sections above have focused on two specific architectures: convolutional networks for visual recognition and transformers for language. It is worth stepping back to map the broader landscape of neural network types, since the field has produced a variety of architectures each suited to different kinds of problems.

## 4.1 Feedforward Networks and Autoencoders

The simplest neural network is the **feedforward network** (also called a multilayer perceptron or MLP): data flows in one direction, from input through hidden layers to output, with no loops or recurrence. These networks are the building blocks inside many more complex architectures.

A close relative, the **autoencoder**, is a feedforward network trained to compress its input down to a compact internal representation and then reconstruct it. The bottleneck forces the network to learn efficient summaries of the data — making autoencoders useful for anomaly detection (inputs that compress poorly are unusual) and representation learning (the compressed form can be used as a rich feature vector for other tasks).

## 4.2 Convolutional Networks

Convolutional neural networks (CNNs) were designed for data with spatial structure, particularly images. Their central insight is weight sharing: rather than learning separate parameters for every position in the input, a CNN uses a small filter — a grid of learned numbers — that slides across the entire input. The same filter detects the same feature (an edge, a curve, a texture) wherever it appears. This makes CNNs extraordinarily parameter-efficient and gives them a natural form of translation invariance.

CNNs are the workhorses of computer vision: image classification, object detection, and segmentation. The same idea applied to one-dimensional sequences — temporal convolutional networks — makes them competitive with recurrent architectures for audio and time-series data.

## 4.3 Recurrent Networks

Where feedforward networks treat each input independently, **recurrent neural networks (RNNs)** maintain a hidden state that carries information forward through a sequence. This makes them natural for language, speech, and any domain where the meaning of the current input depends on what came before.

Basic RNNs struggled with long sequences because gradients vanish as they propagate back through many time steps. **Long short-term memory networks (LSTMs)** and their simpler cousin, the **gated recurrent unit (GRU)**, solved this with explicit gating mechanisms that learn what to remember and what to forget. Sequence-to-sequence models built from LSTMs were the dominant architecture for machine translation before transformers displaced them.

## 4.4 Transformers

The transformer is currently the dominant architecture for the majority of AI tasks, as described at length in Section 3. Two main variants have emerged. **Encoder-only models** (the BERT family) read the full sequence bidirectionally and excel at understanding tasks: classification, named entity recognition, search. **Decoder-only models** (the GPT family) generate text autoregressively and are the basis for conversational AI. **Vision Transformers (ViT)** apply the same attention mechanism to image patches rather than tokens and are now competitive with CNNs for many vision tasks.

## 4.5 Generative Models

A separate family of architectures is concerned not with classifying or predicting, but with generating new data.

**Generative Adversarial Networks (GANs)** pit a generator against a discriminator in an adversarial game: the generator tries to produce realistic images; the discriminator tries to detect fakes. This dynamic produces very sharp outputs but is notoriously difficult to train. GANs have been largely superseded for image generation but remain in use for specific applications such as video synthesis.

**Diffusion models** — the basis of Stable Diffusion, DALL-E, and Midjourney — have largely taken over image generation. They learn to reverse a process of systematic noise addition, and are discussed in detail in Section 5.

**Variational autoencoders (VAEs)** learn a smooth, structured latent space that can be sampled and interpolated, making them useful for controlled generation and the compression stage that sits inside many diffusion pipelines.

## 4.6 Specialist and Hybrid Architectures

Several important architectures address domains where the above do not naturally fit.

**Graph neural networks (GNNs)** handle data defined as graphs — molecular structures, social networks, knowledge graphs — by having nodes iteratively pass messages to their neighbors.

**Reinforcement learning networks**, typically MLPs or CNNs, learn policies and value functions through trial and error with reward signals, and underlie systems like AlphaGo and modern robotics.

**Spiking neural networks** communicate through discrete spikes in time rather than continuous values, placing them closer to biological neurons. They are efficient on specialized neuromorphic hardware but remain largely a research area.

**State space models** — of which Mamba is the most prominent recent example — aim to replace transformers for very long sequences by using recurrent-style state updates that can nonetheless be parallelized during training.

In practice, the most capable modern systems combine several of these ideas. Vision-language models run a vision transformer alongside a language model. Generative image models use transformer backbones. Reinforcement learning is layered atop pre-trained transformers in the RLHF process that aligns conversational AI. The boundaries between these families are, increasingly, permeable.

---
# 5. Diffusion Models and Image Generation

---

## 5.1 Learning to Denoise

The central idea of a diffusion model is counterintuitive: rather than training a network to draw images, train it to *un-destroy* them. The training process begins with real images from a large dataset and systematically corrupts each one by adding Gaussian noise across a sequence of many small steps. After roughly a thousand steps, following a carefully designed noise schedule, every image — regardless of its content — has been reduced to something statistically indistinguishable from pure random noise.

At each intermediate step along this degradation, the network is presented with the noisy image and asked a single question: what noise was added here? The network does not need to reconstruct the full clean image; it only needs to estimate the noise component at this particular level of corruption. This is a much simpler regression problem, and it can be learned reliably.

Over millions of such training examples, the network learns a rich internal model of what natural images look like at every scale and level of abstraction — not by memorizing images, but by learning what distinguishes signal from noise in them.

## 5.2 Reversing the Process: Generation

Generation is the reverse of training. A fresh sample of pure Gaussian noise is drawn — a random image with no structure — and the denoising network is applied iteratively. At each step, the network estimates the noise present in the current image, and a small fraction of that estimated noise is subtracted. After all steps are completed, a coherent image has emerged from what began as randomness.

The critical insight is that the network never generates pixels directly. It makes a series of small corrections, each removing a tiny amount of noise, each guided by everything it learned during training about the statistical structure of natural images. The image coalesces, step by step, from structured noise removal.

An important practical refinement: generation does not happen in the space of raw pixels. Running a thousand denoising steps on a full-resolution image would be computationally prohibitive. Modern systems such as Stable Diffusion work in a **compressed latent space**: a variational autoencoder first encodes the image into a representation roughly sixty-four times smaller in area, diffusion happens in that compact space, and a decoder expands the result back to full resolution. This is what makes high-quality image generation feasible on consumer hardware.

## 5.3 Guiding Generation with Text

A diffusion model trained without conditioning generates images that reflect the distribution of the training data but cannot be steered toward a specific subject. Text-to-image generation requires a mechanism for injecting the semantic content of a prompt into the denoising process.

This is accomplished through a text encoder — typically **CLIP**, a model trained to embed images and their text descriptions into a shared vector space. A prompt like "a knight riding a dragon over a neon-lit cyberpunk city at sunset" is encoded into a vector that captures its semantic content. At every denoising step, this vector is fed into the network via cross-attention, where it influences which directions the denoiser corrects toward. The noise removal is no longer neutral — it systematically favors image states consistent with the prompt.

The strength of this influence is controlled by the **guidance scale** parameter. A high guidance scale produces images that closely match the literal prompt but may be garish or oversaturated, because the model is being pushed into an extreme corner of the probability distribution. A lower value yields more natural-looking images that interpret the prompt more loosely.

## 5.4 Novel Images: The Latent Space

A question that naturally arises: if the model was trained on specific images, how can it generate "a knight riding a dragon over a cyberpunk city" — an image that certainly did not appear in any training set?

The answer is that the model was never trained to remember images. It was trained to understand the structure of visual information. Those millions of training images were not stored; they were compressed into the weights of the network as a rich statistical model of what patterns, textures, lighting conditions, spatial relationships, and object appearances tend to occur in natural and man-made imagery.

This internal model can be thought of geometrically as a **latent space**: a high-dimensional mathematical space in which nearby points correspond to visually similar concepts. Dragon scales and reptile skin are neighbors. Neon glow and rain-slicked pavement are neighbors. Sunset orange and warm backlighting are neighbors. The CLIP text encoder places the prompt's meaning as a point in this same space.

The novel prompt lands in a region of the latent space that no training image directly occupies — but it is surrounded by well-learned concepts on all sides. The denoising process navigates toward that region, synthesizing visual elements from all the neighboring concept clusters simultaneously. The result is an image that has never existed, built from a visual grammar that was thoroughly learned.

## 5.5 What Remains Difficult

This compositionality is powerful but imperfect. Simple combinations work reliably; unusual structural relationships between unfamiliar pairings can fail. The model may understand dragons and knights separately but struggle to correctly render one astride the other, because that particular spatial relationship was not common in training data.

Generating "a red ball to the left of a blue cube" reliably is harder than generating either object alone, because training images rarely depicted those objects in explicitly labeled spatial relationships. This kind of structural composition requires understanding that exceeds statistical co-occurrence of visual patterns.

Techniques such as attention weighting, negative prompting, and iterative refinement exist largely to address such compositional failures. The underlying challenge remains an active area of research, connected to broader questions about whether deep learning systems can achieve the kind of structured, relational reasoning that humans apply effortlessly to novel descriptions.

## 5.6 Mathematics of the Approach, with Visualization

It is hard to undertstand how denoising can produce a meaningful image, especially one that is invented using previous patterns.  The following video provides an explanation: [How AI Image Generation Works](https://www.youtube.com/watch?v=iv-5mZ_9CPY)

One confusing thing about the video is the spiral meant to represent known images.  The presenter was trying to say this: Suppose all your pictures have just two pixels, and suppose they are all black and white images.  You then have two values for each image.  Ok, we can graph that.  Then suppose some human has identified a bunch of these so-called pictures as being of dogs and cats and people.  Of course, this couldn't happen, as a "picture" of two grayscale pictures doesn't show anything recognizable, but we're just supposing, and while we're at, we'll suppose that all the cat pictures are one one arc on the graph, all the dog pictures on another, and all the people pictures are on a third arc. For real pictures, you would have a lot of dimensions, and all the cat pictures would be within one manifold in that many dimensional space. (A manifold in n-space is a surface within that space that is smooth, i.e. differentiable to use a math term.) The presenter was trying to cut that representation down to something that he could show in his 2 dimensional graph.  In actual use, the models and vectors would progress as they do in the video, but in a space of n dimensions, which is more than most of us can visualize.

---

# 6. Artificial Vision in Motion: Self-Driving Cars

---

## 6.1 Historical Roots: Learning to Stay on the Road

The earliest neural network approach to autonomous driving — ALVINN (Autonomous Land Vehicle in a Neural Network), developed by Dean Pomerleau at Carnegie Mellon in the late 1980s — already contained the seed of the central challenge. The system took camera video and sensor data as input and was trained, using backpropagation and gradient descent, to predict the steering action a human driver would take at each moment. The loss function penalized deviations from the human's actual behavior, and the network learned to imitate good driving remarkably well — in conditions similar to its training data.

The failure mode was equally instructive. A model trained only on correct driving has never seen what to do when the vehicle drifts off course, because the training data never includes that situation. Once the car began to deviate, it entered territory the network had never encountered, and it had no learned basis for recovery. It would continue drifting, or behave erratically, having no examples of "I am off the intended path — here is how to return."

The naive fix — deliberately including off-track examples in the training data — fails for an obvious reason: the model would then learn to imitate that behavior too.

The solution that emerged is known as **DAgger** (Dataset Aggregation), formalized by Stéphane Ross and colleagues around 2011. The insight is subtle but important. Rather than having a human physically override the vehicle whenever it drifts, a human expert observes the states the model actually visits — including the slightly-off-nominal ones — and labels each state with the correct action they would take. Those state-action pairs from real, imperfect operation are added to the training set, and the model is retrained. Iterating this process produces a model that has learned recovery behavior from states it actually reaches, not just from the idealized states an expert would visit. This combination of supervised learning with ongoing human feedback closed the gap that purely imitation-based training could not.

---

## 6.2 The Full Stack

A self-driving vehicle is not a single AI system but a tightly integrated pipeline of AI and classical engineering components, each solving a distinct subproblem, with the outputs of each stage feeding the next. Understanding this stack reveals both the sophistication of the engineering and the reasons why full autonomy has proven so difficult to achieve.

The pipeline begins with **sensors**. A fully capable autonomous vehicle typically carries four complementary sensing modalities. **Cameras** provide rich color and texture information across a 360-degree field but perform poorly in rain, fog, and darkness. **LiDAR** fires pulses of laser light and measures the return time to construct a precise three-dimensional point cloud of the surroundings — accurate and lighting-independent but expensive, and degraded by heavy precipitation. **Radar** is cheap, penetrates weather reliably, and measures the velocity of detected objects with high accuracy, though its spatial resolution is too coarse to distinguish object shapes. **GPS combined with high-definition maps** provides centimeter-level positional accuracy when satellite signal is strong and supplies pre-built knowledge of road geometry, lane markings, and speed limits.

Beyond these four primary modalities, autonomous vehicles also incorporate sensors that more closely parallel other aspects of human perception. **Inertial measurement units (IMUs)** — arrays of accelerometers and gyroscopes — detect vehicle slip, unexpected lateral forces, and orientation changes, giving the system a digital analog of the vestibular sense that tells a human driver when the car is sliding on ice. Wheel speed sensors and suspension data can signal road surface conditions. There is active research interest in using **microphones** to detect emergency vehicle sirens, horns, and other auditory cues, though audio has not yet become a primary sensing modality in production systems.

The diversity is deliberate. Each sensor has distinct failure modes; the system is designed so that any single sensor can fail without disabling the car. That redundancy comes at significant hardware cost, which has become a major point of differentiation between competing approaches to the problem.

Humans navigate with a still richer sensory palette — eye contact with pedestrians, the sound of tires on wet pavement, a vibration through the steering wheel, spoken navigation guidance — and current autonomous systems replicate only a subset of these inputs. The gap is real, if narrowing.

---

## 6.3 Perception

Sensor data from all modalities must first be fused into a unified representation of the scene. This **sensor fusion** step is more complex than it might appear: the sensors run at different frequencies, have different spatial coordinate frames, and have different latencies. Transformer architectures have become the approach of choice here, treating each sensor's output as a sequence of tokens that cross-attend to each other, learning which information from which sensor is most relevant in any given driving context.

From the fused representation, three parallel perception tasks proceed. **Object detection** assigns bounding boxes and class labels to every vehicle, pedestrian, cyclist, and obstacle in the scene. CNNs trained on massive datasets of labeled driving footage do this reliably in good conditions. **Semantic segmentation** labels every pixel of every camera image with a category — road surface, lane marking, sidewalk, vegetation, building — giving the car a fine-grained understanding of the drivable space. **Localization** matches current sensor readings against the stored HD map to determine the car's precise position and heading, typically to within a few centimeters.

---

## 6.4 Prediction and Planning

Knowing the current state of the scene is necessary but not sufficient. The system must anticipate the near-future behavior of every other agent — where will that cyclist be in three seconds? Will that pedestrian at the corner step into the road? This trajectory prediction problem is among the hardest in the stack because human behavior is governed by social conventions and intentions that are not directly observable.

Modern prediction models use transformers or graph neural networks that represent each agent as a node in a graph and reason over the interactions between them. A pedestrian facing the road, near a crosswalk, who has been glancing toward oncoming traffic, is likely about to cross. The output of such a model is not a single predicted trajectory for each agent but a probability distribution over several plausible futures. Planning must then navigate safely across all plausible futures simultaneously, not just the most likely one.

Planning itself is organized into three nested levels. **Route planning** is essentially navigation: select a path through the road network from origin to destination. **Behavior planning** makes higher-level tactical decisions at each moment: when to change lanes, when to yield, when to proceed through an intersection, how to react to an unusual obstacle. **Motion planning** works out the precise trajectory — the curve through space and the speed profile along it — that the vehicle should execute over the next few seconds, subject to both physical constraints (steering geometry, tire friction limits) and comfort constraints (passengers notice sudden lateral accelerations even when mechanically safe).

The final stage, **control**, translates the planned trajectory into actual commands to the vehicle's actuators: steering angle, throttle percentage, brake pressure. This stage is typically implemented with classical feedback controllers — PID controllers and model predictive control — rather than neural networks, because these methods are well-understood, formally analyzable, and certifiable for safety.

---

## 6.5 The Modular vs. End-to-End Debate

The pipeline described above represents the **modular philosophy**: each stage of reasoning is implemented as a distinct, interpretable, testable component with a human-designed interface specifying what it should produce. The perception module is told to output bounding boxes and class labels; the prediction module is told to output trajectory probability distributions; the planning module is told to produce a safe motion plan. Neural networks operate *within* each module, learning from data — but what they are learning to produce is defined by engineers. The result is that any stage can be individually inspected, tested, and debugged: if the car behaves unexpectedly, engineers can examine the output of each stage and determine precisely where the reasoning went wrong.

Tesla has pursued a substantially different philosophy, using **end-to-end neural networks** that take camera pixels as input and produce driving commands as output, with intermediate representations learned rather than designed. The argument for this approach is that human engineers cannot anticipate all the intermediate representations that matter; learning them from data may produce a richer internal model than hand-engineered modules can. Tesla has progressively replaced its earlier hand-engineered modules with learned representations, arguing that the network can discover better internal structure than engineers can design.

Both approaches have made remarkable progress. The fundamental challenge for both is the long tail of rare situations: the child who runs into the road between parked cars, the construction zone laid out in a way no training example anticipated, the driver ahead behaving in an inexplicable way. No finite training set covers all such cases, and the consequences of failure are severe.

This long-tail problem cuts more deeply against the end-to-end approach. Neural networks are fundamentally interpolators: they perform well on inputs similar to their training distribution and degrade on inputs far from it. Rare events — a mattress falling from a truck, a horse on the highway, an unusual temporary road configuration — may appear too infrequently in training data for a network to learn robust responses. And because neural networks require many examples of a pattern to learn it reliably, a single dashcam recording of an unusual situation contributes almost nothing. The physical world generates genuinely novel situations continuously; the tail is mathematically inexhaustible.

The 2018 Uber autonomous vehicle fatality in Tempe, Arizona is a sobering illustration. The system struck and killed Elaine Herzberg, who was walking her bicycle across a multi-lane road at night. The NTSB investigation found that the system cycled between classifying her as an unknown object, a vehicle, and a bicycle — never settling on a stable classification — and was not designed to infer from a bicycle detection that a human was likely nearby. The emergency braking system had been disabled by engineers to reduce false positives. This was a perception failure under an unusual combination of circumstances that the training distribution had not adequately covered.

---

## 6.6 Waymo's World Model: Neuro-Symbolic Integration

A crucial and often underappreciated element of Waymo's modular approach is its explicit **world model** — a set of physics-based, algorithmically encoded representations of how the physical world behaves. This is distinct from what the neural networks have learned statistically from data: it is structured knowledge encoded directly by engineers, of the kind associated with classical "Good Old-Fashioned AI" (GOFAI). The result is a **neuro-symbolic architecture** — a hybrid that combines the pattern-recognition power of deep learning with the precision and generalizability of explicit knowledge representation.

The world model is not a safety net that the neural network falls back on when confused. It is woven into the system more deeply than that, operating in at least four distinct ways:

**As a constraint on neural network outputs.** Rather than letting the network predict anything and checking it afterward, the world model defines what outputs are physically valid. If the prediction module suggests a trajectory for a vehicle that violates kinematic constraints — turning sharper than physics allows at that speed — that trajectory is ruled out before planning considers it. The world model acts as a filter running in parallel with learned inference.

**As a prior that resolves uncertainty.** When sensor data is ambiguous — say, partial occlusion makes object classification uncertain — the world model provides probabilistic constraints. If the system knows it is at an intersection and something is moving at 12 mph on the sidewalk, the world model says this is almost certainly a cyclist, not a vehicle. The network's uncertainty is resolved partly by what physical and contextual plausibility dictates. This is Bayesian reasoning, not fallback.

**As the substrate for simulation.** Waymo runs continuous simulation of possible futures using the world model to propagate scenarios forward. The neural network's job is partly to assign probabilities to those simulated futures rather than to predict futures from scratch. This is a profound architectural difference from pure learned prediction.

**As the space within which planning operates.** Motion planning does not search through arbitrary trajectories — it searches through trajectories already constrained to be physically executable, geometrically consistent with the HD map, and within comfort limits. The world model defines the feasible space; planning finds the best option within it.

This architecture reflects one of the oldest debates in AI: explicit knowledge representation versus learning from data. Waymo's position is that some things we know precisely and should encode that way, while the neural networks handle what cannot be known analytically. It is arguably the most sophisticated real-world deployment of neuro-symbolic AI yet built.

---

## 6.7 The SAE Autonomy Scale

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

---

## 6.8 Waymo: Onboard Intelligence

Waymo operates fully driverless paid robotaxi services across San Francisco, Los Angeles, Phoenix, and Austin — true Level 4 operation within those cities' defined operational domains. A common misconception is that Waymo vehicles rely on cloud computing for their real-time decisions. This is incorrect.

All time-critical decisions — perception, prediction, and planning — are executed onboard, in the vehicle, by a purpose-built computer processing the sensor data in real time. The physics of the situation demand this: a cellular round-trip to a data center and back introduces hundreds of milliseconds of latency. A pedestrian stepping into the road at 30 miles per hour covers several feet in that time.

The cloud is used — but for different purposes: training new models on aggregated fleet data, distributing software updates, remote monitoring, and providing human assistance in edge cases where the car has safely stopped to await guidance. A cellular outage would not cause a Waymo vehicle to stop or behave unsafely.

Each Waymo vehicle carries camera, LiDAR, and radar arrays together with the onboard computer that processes their output. This sensor suite is expensive, which has constrained Waymo's scaling relative to camera-only competitors.

---

## 6.9 Tesla: A Different Bet

Tesla's consumer "Full Self-Driving" product is officially classified as a Level 2 system. The driver must remain attentive and ready to intervene at all times; the system provides assistance but does not assume responsibility. Tesla's own documentation states this clearly, even as the product's name has attracted regulatory scrutiny for implying a capability it does not yet have.

Tesla's technical bet differs from Waymo's in two important respects. First, **camera-only sensing**: Tesla argues that humans navigate complex environments using only eyes, and that sufficient camera data — drawn from millions of customer vehicles driving millions of miles daily — can train a system to do the same, making expensive LiDAR unnecessary. Second, **end-to-end neural networks**: Tesla has progressively replaced its hand-engineered perception and planning modules with learned representations, arguing that the network can discover better internal representations than engineers can design.

Tesla launched a commercial robotaxi service in Austin, Texas in mid-2025, initially with a safety employee present in the passenger seat. By early 2026, the service was operating in Austin without any Tesla employee in the vehicle — genuine Level 4 operation within that geofenced area. The service has since expanded in limited form to San Francisco, though California regulations required a safety driver to remain seated there.

---

## 6.10 Beyond Passenger Cars: Autonomous Trucking

The economic case for autonomous vehicles may be even stronger in long-haul freight than in passenger transport. Trucking faces a persistent driver shortage, and the costs of human drivers — wages, mandatory rest periods, hours-of-service regulations — represent the largest single operating expense for carriers. A self-driving semi-truck that can run continuously without rest stops represents a transformative efficiency gain.

**Aurora Innovation** has moved furthest toward commercial reality. In May 2025, Aurora became the first company to operate a commercial driverless trucking service with heavy-duty Class 8 trucks on public roads, running regular freight between Dallas and Houston with no human in the cab. By early 2026, Aurora had surpassed 250,000 driverless miles across a network of routes in the Texas Sun Belt, with a reported safety record of zero Aurora Driver-attributed collisions. A nuance worth noting: some trucks have carried a passive observer at certain partners' request — not operating the vehicle, but present — and Aurora's next-generation hardware, planned for mid-2026, is designed to eliminate even that. Aurora is, by a significant margin, the most advanced commercial deployment in autonomous trucking.

Other companies are at earlier stages of development and testing. **Kodiak Robotics** is conducting autonomous freight operations in the Sun Belt. **Torc Robotics**, acquired by Daimler Truck, is developing systems for integration into Freightliner vehicles. **Gatik** focuses on a narrower problem — short, fixed-route "middle mile" logistics between warehouses and distribution centers — arguing that constrained, repeatable routes are more tractable than open-ended highway driving.

The technical challenges of trucking differ meaningfully from those of robotaxis. Highway driving at sustained speeds is in some respects simpler than urban navigation — fewer pedestrians, fewer intersections, more predictable behavior from other vehicles — but a loaded semi-truck weighing 80,000 pounds has braking distances and handling characteristics that demand exceptional prediction and planning horizons. The consequences of a perception failure at highway speed are severe.

A common near-term deployment model is **"driver-out" on the highway, driver-in at terminals**: a human driver handles the complex urban pickup and delivery legs, while the autonomous system manages the highway segment. This approach sidesteps the hardest parts of the problem while capturing a significant fraction of the efficiency gains. Aurora's current operations fit this model, with the autonomous system handling the highway corridors between major freight hubs.

---

## 6.11 Safety and the Long Road Ahead

Waymo has published comparative safety analyses showing significant advantages over human-driven vehicles across metrics including injury-causing crashes per mile and crashes involving pedestrians and cyclists. These figures reflect millions of fully driverless miles across multiple cities.

No equivalent independently verified dataset yet exists for Tesla's robotaxi at comparable scale, given its recent and more limited deployment. The coming years will produce the data needed to make meaningful comparisons between the two technical philosophies.

Neither company has solved the problem. Level 5 — full automation under any conditions anywhere — remains a distant goal. The challenge is not the typical driving that both systems handle well; it is the unbounded variety of atypical situations that the physical world generates without warning. Both the modular and end-to-end approaches are ultimately attempts to build systems robust enough to handle that long tail. The question of which approach gets there first, and at what scale, remains genuinely open.

---
