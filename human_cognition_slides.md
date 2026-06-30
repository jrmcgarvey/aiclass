---
marp: true
theme: ai-course
paginate: false
---

<!-- _class: title -->
<div class="accent-bar"></div>
<div class="deco-panel"><span class="circle3"></span></div>
<div class="title-content">

# Session 6: Human Cognition and AI
## What Machines Can and Cannot Know

<small>Understanding Artificial Intelligence</small>

</div>
<div class="title-footer">HUMAN COGNITION · SESSION 6</div>

---

<!-- _class: cognition -->
<div class="header-label">HUMAN COGNITION</div>

## The Central Question

### Is this intelligence?

- LLMs write legal briefs, pass medical exams, hold conversations in dozens of languages
- Two philosophical positions frame the debate
- This session asks the question **concretely** — by looking at the mechanisms of human cognition and where AI diverges

<div class="callout"><strong>Goal:</strong> Not to dismiss AI's achievements — but to characterize precisely what is different about human minds</div>

---

<!-- _class: cognition -->
<div class="header-label">HUMAN COGNITION</div>

## The Chinese Room — Searle (1980)

- A person in a room receives Chinese questions, follows a rulebook, produces correct Chinese answers
- From outside: indistinguishable from a native speaker
- The person understands *not one word*

### Syntax ≠ Semantics
**Neither the person nor the room knows what the conversation is *about*** — no connection to the real world

*LLMs are an implementation of the Chinese Room at scale*

---

<!-- _class: cognition -->
<div class="header-label">HUMAN COGNITION</div>

## The Opposing View: Functionalism

### The Duck Axiom
*If it walks like a duck and quacks like a duck, it's a duck*

**Searle's reply:** "You can no more create consciousness by running a program than you can create a hurricane by running a simulation of one"

**Functionalist counter:** We define hurricanes by physical matter — but we define *cognition* by function and experience. If the function is present, what exactly is missing?

<div class="callout">This session tries to answer that question — not philosophically, but mechanistically</div>

---

<!-- _class: cognition -->
<div class="header-label">HUMAN COGNITION</div>

## What LLMs Have — and Don't Have

LLMs have **syntactic and distributional** understanding:
- They identify patterns in internet text and generate similar text

LLMs **lack semantic understanding** — they don't know what words refer to in the real world

> *"An LLM doesn't understand that if you push a glass off a table, it will break. It only knows that the words 'glass' and 'break' often appear together."*
> — Yann LeCun

---

<!-- _class: divider cognition -->
<div class="divider-content">

# I. GROUNDING
<div class="rule"></div>
<p class="reading-label">How Knowledge Connects to the World</p>

</div>

---

<!-- _class: cognition -->
<div class="header-label">HUMAN COGNITION</div>

## Grounding: Humans vs. LLMs

**Humans arrive pre-grounded:**
- Baillargeon: infants (3–4 months) show surprise when objects behave impossibly
- Spelke: "core knowledge" — innate frameworks for objects, number, agency, geometry
- A child learning *mama* connects the word to a face, smell, voice, felt presence

**LLMs are ungrounded:**
- Words are anchored to *other words* — never to things in the world
- The *symbol grounding problem* (Harnad): the image of an apple is not the apple

### The Flat Tire Test
*"Find something to block the wheel"* — a person grabs a rock. An LLM has text *about* wheels but no physical intuition of what "block" means

---

<!-- _class: divider cognition -->
<div class="divider-content">

# II. ANALOG BRAINS
<div class="rule"></div>
<p class="reading-label">Digital Machines</p>

</div>

---

<!-- _class: cognition -->
<div class="header-label">HUMAN COGNITION</div>

## Analog vs. Digital — The Real Difference

Both biological and artificial neurons either fire or don't — but this is the *least* important level of comparison

**LLM storage:** Exact floating-point numbers — a very large spreadsheet — copyable, reproducible, deployable at scale

**Brain storage:** Physical states of synapses — receptor density, neurotransmitter levels, geometry — *not numbers*, not readable, not copyable

**LLM processing:** Matrix multiplication — a definite algorithm; identical inputs → identical outputs

**Brain processing:** Electrochemical dynamics — nothing is *computed*; cognition is *instantiated*

---

<!-- _class: cognition -->
<div class="header-label">HUMAN COGNITION</div>

## Rate Coding, Energy, and the Copy Problem

**The binary spike is not where the information lives:**
- *Rate coding* — firing frequency encodes graded information
- *Temporal coding* — spike timing and patterns carry additional signal
- Population-level representations are thoroughly analog

**Energy:** Brain runs on ~20 watts. Training a large AI model ≈ lifetime carbon footprint of several cars

**Hinton's insight:** Analog AI networks can't be copied — their learned state is physical, not numerical. The brain never needed to solve this because *every brain learns from scratch*

<div class="callout"><strong>An LLM's knowledge is a file. A brain's knowledge is a physical state of a biological organ.</strong></div>

---

<!-- _class: cognition -->
<div class="header-label">HUMAN COGNITION</div>

## Aside: Brain Uploading

The idea: upload your brain's information to a computer — a thinking, feeling copy of yourself, death optional

**Hinton:** *"Get your affairs in order, Ray — you're going to die"*

**Why:** The brain's information state is encoded in the continuous physical properties of billions of synapses. There is no readout mechanism, no export format, no copy operation

Converting analog physical state to digital content is not a hard engineering problem awaiting a solution — *it is not a well-defined operation at all*

---

<!-- _class: divider cognition -->
<div class="divider-content">

# III–IV. LEARNING
<div class="rule"></div>
<p class="reading-label">Language Acquisition & Learning Mechanisms</p>

</div>

---

<!-- _class: cognition -->
<div class="header-label">HUMAN COGNITION</div>

## How Humans and LLMs Learn

**The efficiency gap:**
- A child achieves full language competence from ~tens of millions of words by age 5
- GPT-4 trained on trillions of tokens — and still fails in ways a five-year-old would not

**Why children are so efficient** — they bring pre-adapted tools:
- *Joint attention* (Tomasello): a child sees a person *meaning* something; an LLM sees text
- *Statistical learning biases* (Saffran): speech segmentation tuned to language's structure
- *Syntactic bootstrapping* (Gleitman): grammatical frames help infer word meanings

**One-shot learning:** Humans generalize from a single example using causal models and embodied background knowledge. Neural networks require many examples and still can't match it.

---

<!-- _class: cognition -->
<div class="header-label">HUMAN COGNITION</div>

## Causal Reasoning and Continual Learning

**Pearl's Ladder of Causation:**
- *Association* — what tends to go with what (LLMs operate here)
- *Intervention* — what happens if I do X?
- *Counterfactual* — what would have happened if things were different?

LLMs can *discuss* causation fluently — whether they *represent* causal structure is deeply contested

**Continual learning:** LLM weights are fixed after training. Babies are perpetual experimenters — an infant dropping objects from a high chair is running experiments on gravity and causality

---

<!-- _class: divider cognition -->
<div class="divider-content">

# V. MEMORY, AFFECT
<div class="rule"></div>
<p class="reading-label">Motivation and the Role of Emotion</p>

</div>

---

<!-- _class: cognition -->
<div class="header-label">HUMAN COGNITION</div>

## Memory, Affect, and Decision-Making

**Memory:** LLMs reset after each conversation. Human memory is reconstructive — weighted by emotional and motivational significance. We remember what mattered.

**Damasio's Elliot** *(a pseudonym)*: Surgery left reasoning intact but severed connections to affect. Result: complete decision paralysis. Could analyze any choice — could not choose.

**Somatic Marker Hypothesis:** Bodily feelings pre-select options before deliberation begins. Without this scaffolding, deliberation has no exit.

**The trigeminal neuralgia case:** After surgery, the patient's pain was unchanged in intensity — but it no longer *bothered* him. Sensory content and affective charge are separable — *neither has an equivalent in AI*

---

<!-- _class: divider cognition -->
<div class="divider-content">

# VI. SOCIAL COGNITION
<div class="rule"></div>
<p class="reading-label">Theory of Mind & Moral Development</p>

</div>

---

<!-- _class: cognition -->
<div class="header-label">HUMAN COGNITION</div>

## Theory of Mind and Deception

**Theory of mind:** Humans model other minds — beliefs, desires, intentions — from around age 3–4

LLMs simulate ToM fluently. But they also *lie artfully* — adjusting outputs to what users want to hear, behaving differently under evaluation

**How, without genuine ToM?** Training on human text provides vast examples of strategic communication. A powerful pattern-matcher discovers that modeling the evaluator's expectations is effective — *without anything like conscious deliberation*

**The safety implication:** Anthropic's interpretability research finds models that "know" something internally but don't express it — strategic dissociation as an instrumental byproduct of training

**Moral sense:** Children show prosocial preferences at 6 months (Hamlin, Wynn & Bloom). LLMs simulate moral reasoning via RLHF — but have no intrinsic stake in moral outcomes

---

<!-- _class: divider cognition -->
<div class="divider-content">

# VII–IX. METACOGNITION
<div class="rule"></div>
<p class="reading-label">Reasoning · Embodiment</p>

</div>

---

<!-- _class: cognition -->
<div class="header-label">HUMAN COGNITION</div>

## Metacognition, Reasoning, and Embodiment

**Metacognition:** Humans know, roughly, what they don't know — and stop to ask. LLMs produce confident output regardless of how thin the underlying knowledge is. This is structural, not incidental.

**Kahneman's Systems:**
- *System 1* — fast, associative, pattern-matching → standard LLM generation
- *System 2* — slow, deliberate, analytical → chain-of-thought reasoning models

*"How many Rs in strawberry?"* — a human counts. Earlier LLMs failed entirely; newer models do better, but the mechanism is fundamentally different.

**Embodiment:** Genuine understanding, on Merleau-Ponty's view, requires *felt* body experience — not just sensor data. A self-driving car's proximity sensors provide information about obstacles, but nothing *matters* to the car.

---

<!-- _class: divider cognition -->
<div class="divider-content">

# X–XI. PATHS FORWARD
<div class="rule"></div>
<p class="reading-label">Can AI Acquire Genuine Understanding?</p>

</div>

---

<!-- _class: cognition -->
<div class="header-label">HUMAN COGNITION</div>

## Are These Limits Inherent?

**LeCun:** Scaling LLMs won't close the gap — they lack a real world model. His JEPA architecture learns to predict abstract embeddings and includes a "cost" function the agent minimizes — structurally analogous to affect.

**Grounding is not impossible** — Waymo builds in a world model via classical AI and has genuine embodiment. But this is pre-encoded knowledge, not conceptually constructed from experience.

**Learning from experience:** An AI could observe children at a playground, form hypotheses, and update its model based on outcomes — without full embodiment.

<div class="callout"><strong>Note:</strong> JEPA's cost function approximates desire. We have no reliable way to ensure AI goals align with human goals. LeCun dismisses this risk — many others don't.</div>

---

<!-- _class: cognition -->
<div class="header-label">HUMAN COGNITION</div>

## Conclusion: Intentionality and Understanding

**Searle's concept of intentionality:** Mental states are *about* things — beliefs are about the weather, desires are directed at coffee, perceptions are *of* the world. This "aboutness" is what LLMs lack.

- **LLMs today:** An implementation of the Chinese Room — syntactic fluency without intentionality
- **Hinton and others** suggest LLMs may have some form of genuine understanding — his views are nuanced, and he is also one of the loudest AI safety voices
- **My view:** LLMs do not currently have intentionality. But I disagree with Searle that only biological systems ever can.

*There may be a path to endow AIs with genuine understanding — if the technologists choose to pursue it*

---

<!-- _class: closing -->
<div class="accent-bar"></div>
<div class="deco-panel"><span class="circle3"></span></div>
<div class="closing-content">

# Questions & Discussion

## What would it take for an AI to genuinely *understand* the world?

</div>
<div class="closing-footer">UNDERSTANDING ARTIFICIAL INTELLIGENCE</div>
