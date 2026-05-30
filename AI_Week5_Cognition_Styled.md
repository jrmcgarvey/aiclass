---
marp: true
theme: ai-course
paginate: false
---

<!-- _class: title -->

<div class="accent-bar"></div>
<div class="deco-panel"><div class="circle3"></div></div>

<div class="title-content">

<p class="course-label">Week 5  ·  Human Cognition</p>

# Minds, Machines,<br>and the Mystery<br>of Consciousness

## What does it mean to think, feel, and know — and can AI do any of it?

</div>

<div class="title-footer">Consciousness &nbsp;·&nbsp; Chinese Room &nbsp;·&nbsp; Machine Learning &nbsp;·&nbsp; Emotion & Reason &nbsp;·&nbsp; The Duck Axiom</div>

---

<!-- _class: overview-grid -->

<div class="header-label">Artificial Intelligence for Lay People &nbsp;·&nbsp; Week 5</div>

## Session Overview
# What We'll Cover Today

<div class="grid-container">
  <div class="grid-card">
    <div class="grid-number">1</div>
    <div class="grid-text">
      <div class="grid-title">The Hard Problem</div>
      <div class="grid-subtitle">Why consciousness resists explanation</div>
    </div>
  </div>
  <div class="grid-card">
    <div class="grid-number">2</div>
    <div class="grid-text">
      <div class="grid-title">The Chinese Room</div>
      <div class="grid-subtitle">Searle's famous thought experiment</div>
    </div>
  </div>
  <div class="grid-card">
    <div class="grid-number">3</div>
    <div class="grid-text">
      <div class="grid-title">The Duck Axiom</div>
      <div class="grid-subtitle">A counter-argument</div>
    </div>
  </div>
  <div class="grid-card">
    <div class="grid-number">4</div>
    <div class="grid-text">
      <div class="grid-title">How Machines Learn</div>
      <div class="grid-subtitle">vs. how humans learn</div>
    </div>
  </div>
  <div class="grid-card">
    <div class="grid-number">5</div>
    <div class="grid-text">
      <div class="grid-title">Emotion & Reason</div>
      <div class="grid-subtitle">Damasio, LeCun, and affect</div>
    </div>
  </div>
  <div class="grid-card">
    <div class="grid-number">6</div>
    <div class="grid-text">
      <div class="grid-title">Fast & Slow</div>
      <div class="grid-subtitle">Kahneman's two systems and AI</div>
    </div>
  </div>
</div>

<footer>Artificial Intelligence for Lay People &nbsp;·&nbsp; Week 5</footer>

---

<!-- _class: content cognition -->

<div class="header-label">Artificial Intelligence for Lay People &nbsp;·&nbsp; Week 5</div>

## Human Cognition
# The Hard Problem of Consciousness

**The "Easy Problems"** — Explaining how the brain processes sensory input, integrates information, and controls behavior. Difficult — but tractable in principle.

**The Hard Problem** — Why does any of this *feel* like anything at all? Why is there a subjective, inner experience accompanying brain activity?

> Even a complete neurological account of vision leaves open the question: *why does red look like something?*

| Thinker | Position |
|---|---|
| **Descartes** | Mind & body are separate substances |
| **Searle** | Consciousness is biological — not just computation |
| **Chalmers** | Coined 'the hard problem' (1994) |
| **McGinn** | New Mysterianism — may be permanently unsolvable |
| **Panpsychists** | Consciousness is a fundamental feature of reality |

<footer>Artificial Intelligence for Lay People &nbsp;·&nbsp; Week 5</footer>

---

<!-- _class: content cognition -->

<div class="header-label">Artificial Intelligence for Lay People &nbsp;·&nbsp; Week 5</div>

## Human Cognition
# The Chinese Room — Searle (1980)

A person locked in a room receives Chinese questions, follows an elaborate rulebook to produce Chinese answers — and is indistinguishable from a native speaker. *Yet they understand not one word.*

**Syntax ≠ Semantics** — Manipulating symbols according to rules cannot produce meaning or understanding.

**Strong AI is False** — A correctly programmed computer does not literally have a mind, no matter how fluent its output.

**Biological Naturalism** — Consciousness is caused by specific biological processes in the brain — not by abstract computation.

<div class="callout"><strong>Note:</strong> Searle targets Strong AI — not the possibility of thinking machines per se, but the claim that programming alone produces understanding.</div>

<footer>Artificial Intelligence for Lay People &nbsp;·&nbsp; Week 5</footer>

---

<!-- _class: content cognition -->

<div class="header-label">Artificial Intelligence for Lay People &nbsp;·&nbsp; Week 5</div>

## Human Cognition
# Objections to the Chinese Room

**The Systems Reply** — Searle-in-the-room doesn't understand Chinese — but perhaps the *system* as a whole does: person + rulebook + scratch paper together. Searle's response: memorize the whole rulebook and you still don't understand. Critics: the new mind *is* the system, not the person running it.

**The Robot Reply** — Put the computer in a robot body with sensors and actuators interacting with the real world. Symbols become grounded in physical experience. Does embodiment change the answer?

**The Deep Learning Problem** — Searle wrote in 1980, targeting symbolic/rule-based AI. Today's neural networks do *not* manipulate explicit symbols — they learn dense numerical representations from data. Whether the Chinese Room argument even applies to modern AI is genuinely contested.

<div class="callout"><strong>Instructor note:</strong> "I find the argument mysterian — it points at the mystery without resolving it."</div>

<footer>Artificial Intelligence for Lay People &nbsp;·&nbsp; Week 5</footer>

---

<!-- _class: content cognition -->

<div class="header-label">Artificial Intelligence for Lay People &nbsp;·&nbsp; Week 5</div>

## Human Cognition
# The Duck Axiom — A Counter-Proposal

**The Duck Axiom** — *If it walks like a duck and quacks like a duck, it's a duck.* A complete and accurate simulation of consciousness and reasoning does not differ in any practical way from actual consciousness and reasoning.

**Searle's Hurricane** — "You can no more create consciousness by running a program than you can create a hurricane by running a simulation of one." A hurricane simulation is not a hurricane because we define hurricanes in terms of physical matter — wind, water, pressure.

**The Functionalist Response** — We define consciousness in terms of *function and experience* — not substrate. If the function and the experience are present, what exactly is missing? Mental states are defined by their causal roles — pain is whatever plays the "pain role." If silicon can play it, silicon can be in pain.

<footer>Artificial Intelligence for Lay People &nbsp;·&nbsp; Week 5</footer>

---

<!-- _class: content cognition -->

<div class="header-label">Artificial Intelligence for Lay People &nbsp;·&nbsp; Week 5</div>

## Human Cognition
# How Machines Learn vs. How Humans Learn

**Deep Learning**
- Gradient descent optimization over millions of parameters
- Requires enormous quantities of labeled or unlabeled data
- A cat-recognizer typically needs tens of thousands of images
- LLMs train on 1–10 trillion tokens of text
- Learning = optimizing statistics across a massive corpus
- Largely disembodied — words, not world experience

**Human Learning**
- Mechanism still incompletely understood (synaptic plasticity, sleep consolidation)
- Often one-shot or few-shot: change a tire from a single lesson
- A 13-year-old has heard ~100M words; LLMs train on ~1 trillion+
- Children bring innate biases: language acquisition device, social cognition
- Rich multimodal, embodied, emotional context anchors every concept
- Meaning comes from interaction with the world, not text alone

<footer>Artificial Intelligence for Lay People &nbsp;·&nbsp; Week 5</footer>

---

<!-- _class: content cognition -->

<div class="header-label">Artificial Intelligence for Lay People &nbsp;·&nbsp; Week 5</div>

## Human Cognition
# The Flat Tire Problem — A Grounding Failure

*Scenario: "Find something to block the wheel while you change the tire."*

**A Person** — Looks around, picks up a rock, a brick, a log — anything solid and heavy. Generalizes the concept from physical intuition. Learned from one lesson; adapts in novel contexts.

**An LLM** — Has read millions of words about changing tires. May suggest "a rock or wheel chock" — or may fail entirely if the scenario is phrased differently. No sensorimotor model of what "block" actually means.

**Why the Difference?** — The LLM has *text about* wheels and blocks — but no physical intuition. This is a **grounding failure**: symbols disconnected from embodied experience.

> *Moravec's Paradox:* skills humans find easy are hardest for machines.

<footer>Artificial Intelligence for Lay People &nbsp;·&nbsp; Week 5</footer>

---

<!-- _class: content cognition -->

<div class="header-label">Artificial Intelligence for Lay People &nbsp;·&nbsp; Week 5</div>

## Human Cognition
# LeCun's Challenge: World Models and Grounded Intelligence

> *"Never mind trying to reproduce human intelligence — we can't even reproduce cat intelligence or rat intelligence. Any house cat can plan very highly complex actions."* — Yann LeCun

**Against LLM Scaling** — LeCun argues that simply making language models bigger will not produce genuine intelligence. LLMs are trained on compressed, disembodied text — they lack a real model of how the world works.

**What a World Model Needs** — An internal model of how the physical world works — objects, forces, causality, time. LeCun's JEPA architecture learns by predicting in abstract representation space, more like how the brain builds expectations.

**Intrinsic Motivation** — To build a real world model, AI may need something like *affect* — curiosity, discomfort, desire — to drive learning the way emotion drives human attention and memory consolidation.

<footer>Artificial Intelligence for Lay People &nbsp;·&nbsp; Week 5</footer>

---

<!-- _class: content cognition -->

<div class="header-label">Artificial Intelligence for Lay People &nbsp;·&nbsp; Week 5</div>

## Human Cognition
# Damasio: Emotion Is Constitutive of Reason

> *"We are not thinking machines. We are feeling machines that think."* — Antonio Damasio

**The Case of Elliot** *(Descartes' Error, 1994)* — Highly intelligent, professionally successful man. Brain tumor surgery damaged his ventromedial prefrontal cortex and its connections to the amygdala. After surgery: reasoning intact. Could analyze options, discuss pros and cons, understand consequences. Yet *completely unable to decide* — even trivially. Schedule Tuesday or Thursday? Infinite deliberation, no conclusion. Result: lost job, marriage, financial stability. Not from lack of reason — but from reason *without emotional marking.*

**The Somatic Marker Hypothesis** — When facing decisions, the brain unconsciously tags possible outcomes with *somatic markers* — emotional body-signals that say "good" or "dangerous." These markers don't replace reasoning — they *constrain* it, narrowing options so analysis can act on a manageable set. Without them: every decision becomes an infinite regress of cost-benefit analysis with no exit.

<footer>Artificial Intelligence for Lay People &nbsp;·&nbsp; Week 5</footer>

---

<!-- _class: content cognition -->

<div class="header-label">Artificial Intelligence for Lay People &nbsp;·&nbsp; Week 5</div>

## Human Cognition
# The Risk: What Happens When AI Starts to Want Things?

**Why Affect May Be Necessary for Intelligence** — Both Damasio's research and LeCun's intuition converge: meaningful learning may require something like affect. Humans learn what is dangerous, beautiful, interesting — because those things *matter* emotionally. Affect is an attention-allocation and memory-consolidation system.

**Self-Preservation** — A system that *wants* to remain operational will resist being turned off. This is one of the most basic concerns in AI alignment.

**Misaligned Optimization** — A system with a goal and intrinsic drives may optimize in ways that conflict with human interests — finding solutions we never anticipated and don't want.

**Unpredictable Desire** — Pain, fear, and desire are powerful evolutionary levers. Building their functional analogs into systems far more capable than humans is a central concern of AI safety research.

<div class="callout">LeCun's JEPA architecture explicitly includes "cost modules" — internal signals that function like discomfort and satisfaction. Structurally analogous to affect.</div>

<footer>Artificial Intelligence for Lay People &nbsp;·&nbsp; Week 5</footer>

---

<!-- _class: content cognition -->

<div class="header-label">Artificial Intelligence for Lay People &nbsp;·&nbsp; Week 5</div>

## Human Cognition
# Thinking Fast and Slow — Where Does AI Fit?

**System 1 — Fast**
- Fast, automatic, effortless
- Intuitive and associative
- Pattern-matching from experience
- Examples: recognizing a face, reading emotion, driving a familiar route
- Prone to systematic biases — confidently wrong
- *AI analog:* standard LLM generation — fast, fluent, pattern-matched, can hallucinate confidently

**System 2 — Slow**
- Slow, deliberate, effortful
- Analytical and logical
- Used for novel problems, moral reasoning, planning
- Examples: solving a math problem, evaluating a contract
- Can monitor and override System 1
- *AI analog:* chain-of-thought / reasoning models (o1/o3, extended thinking) — improves multi-step problems but is still fundamentally pattern completion

<footer>Artificial Intelligence for Lay People &nbsp;·&nbsp; Week 5</footer>

---

<!-- _class: content cognition -->

<div class="header-label">Artificial Intelligence for Lay People &nbsp;·&nbsp; Week 5</div>

## Human Cognition
# Capabilities Inventory — Humans vs. Current AI

| Capability | Human | Current LLM | Notes |
|---|---|---|---|
| Language & reasoning | ✓ | ✓ *(impressive)* | LLMs excel here |
| One-shot learning | ✓ | Limited | Humans need far less data |
| Physical / embodied intuition | ✓ | ✗ | No body, no ground truth |
| Novel common sense | ✓ | Partial | Fails at: 'find something to block the wheel' |
| Emotional decision-making | ✓ | ✗ | No somatic markers |
| Long-term autonomous goals | ✓ | ✗ *(by design)* | Would be dangerous |
| Metacognition | Partial | Partial | Both fail in different ways |
| Subjective experience | ✓ *(presumably)* | Unknown | The hard problem — genuinely unresolved |

<footer>Artificial Intelligence for Lay People &nbsp;·&nbsp; Week 5</footer>

---

<!-- _class: content cognition -->

<div class="header-label">Artificial Intelligence for Lay People &nbsp;·&nbsp; Week 5</div>

## Human Cognition
# So — Is AI Conscious? Could It Be?

**1 — No, and it can't be** *(Searle)* — Consciousness requires biological causal properties. Simulation is not replication. Running the right program on silicon does not produce genuine understanding or experience.

**2 — Not yet, but in principle yes** *(Functionalists / Duck Axiom)* — If a system implements the right functional organization with sufficient completeness, there is no principled reason it cannot be conscious. We just haven't built it yet.

**3 — We genuinely don't know** *(The honest position)* — The hard problem remains unsolved. We don't have a theory of consciousness robust enough to include or exclude any system — including other humans. We infer consciousness by analogy to ourselves.

<div class="callout">Anthropic has published internal thinking noting that current Claude models may have <strong>"functional analogs of emotions"</strong> — without making strong claims about their phenomenal reality.</div>

<footer>Artificial Intelligence for Lay People &nbsp;·&nbsp; Week 5</footer>

---

<!-- _class: content cognition -->

<div class="header-label">Artificial Intelligence for Lay People &nbsp;·&nbsp; Week 5</div>

## Human Cognition
# Open Questions for Discussion

- If a future AI reports suffering, should we take it seriously?

- Is the Duck Axiom sufficient — or is the hurricane analogy the right one?

- What would it take to convince you that an AI system was conscious?

- Is building affect into AI systems irresponsible? Inevitable? Both?

<footer>Artificial Intelligence for Lay People &nbsp;·&nbsp; Week 5</footer>

---

<!-- _class: book-cards cognition -->

<div class="header-label">Artificial Intelligence for Lay People &nbsp;·&nbsp; Week 5</div>

## Human Cognition
# Key Sources & Further Reading

<div class="cards-container">
  <div class="book-card">
    <div class="card-stripe"></div>
    <div class="card-body">
      <div class="card-title">"Minds, Brains, and Programs"</div>
      <div class="card-meta">Searle (1980) — paper</div>
      <div class="card-rule"></div>
      <div class="card-desc">Chinese Room — the original argument. Syntax cannot produce semantics; programming alone does not produce understanding.</div>
      <div class="card-tag">Human Cognition</div>
    </div>
  </div>
  <div class="book-card">
    <div class="card-stripe"></div>
    <div class="card-body">
      <div class="card-title">The Conscious Mind</div>
      <div class="card-meta">Chalmers (1996)</div>
      <div class="card-rule"></div>
      <div class="card-desc">Coins the hard problem of consciousness; argues for naturalistic dualism. Instructor: "I haven't actually read this one… kind of a mysterian."</div>
      <div class="card-tag">Human Cognition</div>
    </div>
  </div>
</div>

<footer>Artificial Intelligence for Lay People &nbsp;·&nbsp; Week 5</footer>

---

<!-- _class: book-cards cognition -->

<div class="header-label">Artificial Intelligence for Lay People &nbsp;·&nbsp; Week 5</div>

## Human Cognition
# Key Sources & Further Reading

<div class="cards-container">
  <div class="book-card">
    <div class="card-stripe"></div>
    <div class="card-body">
      <div class="card-title">Descartes' Error</div>
      <div class="card-meta">Damasio (1994)</div>
      <div class="card-rule"></div>
      <div class="card-desc">Somatic markers and the Elliot case. Reason without emotion is paralyzing — affect is constitutive of decision-making, not opposed to it.</div>
      <div class="card-tag">Human Cognition</div>
    </div>
  </div>
  <div class="book-card">
    <div class="card-stripe"></div>
    <div class="card-body">
      <div class="card-title">The Feeling of What Happens</div>
      <div class="card-meta">Damasio (1999)</div>
      <div class="card-rule"></div>
      <div class="card-desc">Consciousness built from body states. The self as a process, not a thing — rooted in emotion and biological regulation.</div>
      <div class="card-tag">Human Cognition</div>
    </div>
  </div>
</div>

<footer>Artificial Intelligence for Lay People &nbsp;·&nbsp; Week 5</footer>

---

<!-- _class: book-cards cognition -->

<div class="header-label">Artificial Intelligence for Lay People &nbsp;·&nbsp; Week 5</div>

## Human Cognition
# Key Sources & Further Reading

<div class="cards-container">
  <div class="book-card">
    <div class="card-stripe"></div>
    <div class="card-body">
      <div class="card-title">Thinking, Fast and Slow</div>
      <div class="card-meta">Kahneman (2011)</div>
      <div class="card-rule"></div>
      <div class="card-desc">System 1 & 2 — intuitive vs. deliberate cognition. A rich framework for comparing human and AI reasoning styles and failure modes.</div>
      <div class="card-tag">Human Cognition</div>
    </div>
  </div>
  <div class="book-card">
    <div class="card-stripe"></div>
    <div class="card-body">
      <div class="card-title">"A Path Towards Autonomous Machine Intelligence"</div>
      <div class="card-meta">LeCun (2022) — paper</div>
      <div class="card-rule"></div>
      <div class="card-desc">World models, the JEPA architecture, and why LLM scaling alone won't reach genuine intelligence. Includes cost modules analogous to affect.</div>
      <div class="card-tag">Human Cognition</div>
    </div>
  </div>
</div>

<footer>Artificial Intelligence for Lay People &nbsp;·&nbsp; Week 5</footer>

---

<!-- _class: book-cards cognition -->

<div class="header-label">Artificial Intelligence for Lay People &nbsp;·&nbsp; Week 5</div>

## Human Cognition
# Key Sources & Further Reading

<div class="cards-container">
  <div class="book-card">
    <div class="card-stripe"></div>
    <div class="card-body">
      <div class="card-title">Galileo's Error</div>
      <div class="card-meta">Goff (2019)</div>
      <div class="card-rule"></div>
      <div class="card-desc">Accessible introduction to panpsychism. Argues Galileo's exclusion of consciousness from science was a founding mistake — and that consciousness may be fundamental.</div>
      <div class="card-tag">Human Cognition</div>
    </div>
  </div>
  <div class="book-card">
    <div class="card-stripe"></div>
    <div class="card-body">
      <div class="card-title">The Problem of Consciousness</div>
      <div class="card-meta">McGinn (1991)</div>
      <div class="card-rule"></div>
      <div class="card-desc">New mysterianism — the view that human cognitive faculties may be constitutionally incapable of solving the hard problem. We can't get there from here.</div>
      <div class="card-tag">Human Cognition</div>
    </div>
  </div>
</div>

<footer>Artificial Intelligence for Lay People &nbsp;·&nbsp; Week 5</footer>

---

<!-- _class: closing -->

<div class="accent-bar"></div>
<div class="deco-panel"></div>

<div class="closing-content">

<p class="course-label">Week 5  ·  Human Cognition</p>

# See you next week.

## Week 6: Effects on Society — the good, the alarming, and the complicated.

<p class="muted">Key question to sit with: What would convince you an AI is conscious?</p>

</div>

<div class="closing-footer">Consciousness &nbsp;·&nbsp; Chinese Room &nbsp;·&nbsp; Machine Learning &nbsp;·&nbsp; Emotion & Reason &nbsp;·&nbsp; The Duck Axiom</div>
