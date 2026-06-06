---
marp: true
theme: ai-course
paginate: false
---

<!-- _class: title -->
<div class="accent-bar"></div>
<div class="deco-panel"></div>
<div class="title-content">
  <div class="course-label">Understanding Artificial Intelligence</div>
  <h1>Do LLMs Understand?</h1>
  <div class="subtitle">Language, Meaning, and the Limits of Pattern</div>
  <div class="muted">Discussion Session · Read the companion document before class</div>
</div>

---

<!-- _class: divider cognition -->
<div class="header-label">Understanding Artificial Intelligence</div>
<div class="divider-content">
  <div class="divider-title">The Central Question</div>
  <div class="divider-sub">What does it mean for an LLM to "understand" anything?</div>
</div>

---

<!-- _class: cognition -->
<div class="header-label">Understanding Artificial Intelligence</div>

## The Starting Position

**LLMs have *distributional* understanding of language**

- They learn, with extraordinary sophistication, which words and phrases tend to appear near which other words and phrases
- What they may lack: any genuine connection to the physical world those words are *supposed to refer to*
- This is a live philosophical debate — smart people disagree sharply

> **The question matters** because LLMs are now producing results that in some domains exceed what individual humans can do — including solving 80-year-old mathematical problems

---

<!-- _class: divider progress -->
<div class="header-label">Understanding Artificial Intelligence</div>
<div class="divider-content">
  <div class="divider-title">Two Camps</div>
  <div class="divider-sub">Believers and Skeptics</div>
</div>

---

<!-- _class: progress -->
<div class="header-label">Understanding Artificial Intelligence</div>

## Camp 1 — They Do Understand

**Geoffrey Hinton** *(Turing Award, "Godfather of Deep Learning")*
> *"ChatGPT seems to me to be like an idiot savant whose understanding is different from mine but not entirely absent."*

- Understanding should not be treated as binary — all or nothing
- LLMs create high-dimensional representations capturing genuine semantic relationships

**Dario Amodei** *(CEO, Anthropic)*
> *"We don't know if the models are conscious… But we're open to the idea that it could be."*

- Internal interpretability work finds activations associated with states like anxiety
- Leaves the door open; does not make a strong positive claim

---

<!-- _class: cognition -->
<div class="header-label">Understanding Artificial Intelligence</div>

## Camp 2 — They Don't Understand (1/3)

**Yann LeCun** *(Turing Award, founder AMI — formerly Meta)*
> *"LLMs perform well at the language level, but they don't understand the world. They lack common sense and causal relationships and are just a stack of statistical correlations."*

> *"An LLM doesn't understand that if you push a glass off a table, it will break. It only knows that the words 'glass' and 'break' often appear together."*

**Four capabilities LeCun says LLMs lack:**
- Understanding of the physical world
- Persistent memory
- Genuine reasoning
- Planning

---

<!-- _class: cognition -->
<div class="header-label">Understanding Artificial Intelligence</div>

## Camp 2 — They Don't Understand (2/3)

**John Searle** *(philosopher, UC Berkeley — the Chinese Room, 1980)*

A person in a room follows rules to manipulate Chinese symbols perfectly — passes the Turing Test — but understands nothing.

> *"If the man in the room does not understand Chinese on the basis of implementing the appropriate program… then neither does any other digital computer solely on that basis."*

**The key distinction:** computers have *syntax* but not *semantics*
- Symbols are manipulated by formal rules
- No intrinsic *intentionality* — no genuine "aboutness"
- Meaning requires biological, embodied processes — not symbol shuffling

---

<!-- _class: cognition -->
<div class="header-label">Understanding Artificial Intelligence</div>

## Camp 2 — They Don't Understand (3/3)

**Bender, Gebru, McMillan-Major & Mitchell** *("Stochastic Parrots," 2021)*

> *"Contrary to how it may seem when we observe its output, an LM is a system for haphazardly stitching together sequences of linguistic forms it has observed in its vast training data, according to probabilistic information about how they combine, but without any reference to meaning: a **stochastic parrot**."*

**Gary Marcus** *(cognitive scientist, NYU)*

> *"I do believe that LLMs do not really understand what they are saying."*

> *"Humans rarely make things up wholesale. LLMs do."*

- Hallucination is not a fixable bug — it is a symptom of a deeper absence: no grounded model of reality
- Has been in direct public debate with both Hinton and LeCun

---

<!-- _class: divider technical -->
<div class="header-label">Understanding Artificial Intelligence</div>
<div class="divider-content">
  <div class="divider-title">Philosophical Roots</div>
  <div class="divider-sub">This debate is not new</div>
</div>

---

<!-- _class: technical -->
<div class="header-label">Understanding Artificial Intelligence</div>

## A Long Argument

**Lady Lovelace (1843)** on Babbage's Analytical Engine:
> *"The Analytical Engine has no pretensions whatever to originate anything. It can do whatever we know how to order it to perform… but it has no power of anticipating any analytical relations or truths."*

**Alan Turing (1950)** named this "Lady Lovelace's Objection" — and disputed it, arguing a machine can be programmed to surprise us

**Hubert Dreyfus (1972)** *What Computers Can't Do*
- Human intelligence is rooted in **embodied experience** and tacit **background knowledge** that cannot be captured symbolically
- Called AI research of his era: *"tree climbing with one's eyes on the moon"*

<div class="callout"><strong>The stochastic parrot argument is the latest chapter in a very long story.</strong></div>

---

<!-- _class: divider progress -->
<div class="header-label">Understanding Artificial Intelligence</div>
<div class="divider-content">
  <div class="divider-title">The Puzzle</div>
  <div class="divider-sub">If they don't understand — why are they so good?</div>
</div>

---

<!-- _class: progress -->
<div class="header-label">Understanding Artificial Intelligence</div>

## Recent Mathematics Results

**May 2026 — OpenAI disproves Erdős' planar unit distance conjecture**
- An 80-year-old geometry problem, unsolved by human mathematicians
- Mathematicians called the AI's approach *"clever," "elegant"* — a *"Proof from The Book"*

**The "First Proof" project**
- LLMs resolved **9 of 353** open Erdős problems autonomously
- Also proved **44 of 492** open conjectures from the Online Encyclopedia of Integer Sequences
- Cost: a few hundred dollars per problem

**The architecture:** LLMs generate candidate proofs → **Lean** (a symbolic formal verification language) checks them

<div class="callout">Lean was <strong>not</strong> built with AI — it uses classical symbolic logic. The intelligence is <em>distributed</em>: LLMs for generation, symbolic systems for verification.</div>

---

<!-- _class: divider technical -->
<div class="header-label">Understanding Artificial Intelligence</div>
<div class="divider-content">
  <div class="divider-title">The Proposal</div>
  <div class="divider-sub">Mathematics is language</div>
</div>

---

<!-- _class: technical -->
<div class="header-label">Understanding Artificial Intelligence</div>

## Mathematics Is a Form of Language

- Mathematics has unusually strict rules of inference and an unusually tight relationship to physical reality — Wigner's *"unreasonable effectiveness of mathematics"*
- But at bottom, it is a **formal symbolic system**: proofs are valid transformations from premises to conclusions
- The symbols ∃ ∀ → ∈ have no more intrinsic connection to the physical world than "glass" or "break"

**Therefore LLMs can emulate mathematical reasoning for the same reason they emulate any linguistic production:**
they have learned the patterns of valid mathematical inference from an enormous corpus of mathematical text

**This explains:**
- Why LLMs produce impressive math results
- Why they still hallucinate proofs — and why Lean is needed
- Why fine-tuning on proofs and chain-of-thought "reasoning" improve results

---

<!-- _class: technical -->
<div class="header-label">Understanding Artificial Intelligence</div>

## The Broader Claim

**Much of what we call human intelligence is, at bottom, linguistic production**

Scientific papers · Legal briefs · Philosophical arguments · Medical reports · Software code · Business strategy · Literature

An entity that has mastered the **deep patterns** of human language — not just grammar, but valid reasoning, evidence marshaling, narrative structure — can produce outputs indistinguishable from, and sometimes superior to, individual human experts.

**But LLMs remain genuinely limited where language is not enough:**

- Statements about the physical world still go wrong
- Hallucination persists — confirming Marcus's point about no grounded reality model
- Novel physical situations, robotics, causal reasoning: distributional semantics is insufficient

<div class="callout">The line between "what is linguistic" and "what requires physical grounding" may be the most important boundary in AI capability.</div>

---

<!-- _class: divider alignment -->
<div class="header-label">Understanding Artificial Intelligence</div>
<div class="divider-content">
  <div class="divider-title">For Discussion</div>
  <div class="divider-sub">Questions to consider</div>
</div>

---

<!-- _class: alignment -->
<div class="header-label">Understanding Artificial Intelligence</div>

## Discussion Questions

1. Is *"mathematics is language"* convincing? Does it matter that mathematicians report a felt sense of **insight** when they grasp a proof?

2. Hinton: the line between "mere pattern matching" and "real understanding" may not be as clear as critics assume — human understanding may itself be sophisticated pattern recognition. How do we respond?

3. If LLMs produce valid proofs (verified by Lean), does it matter whether they *understand* them in a philosophically robust sense?

4. What tasks are **not** reducible to linguistic pattern? Where do you expect LLMs to remain permanently limited?

5. Searle: *intrinsic* intentionality (meaning that originates in a mind) vs. *derived* intentionality (meaning we project onto artifacts). Is this distinction defensible?

6. Marcus argues hallucination is a symptom, not a bug. Does the Lean workaround solve the problem — or confirm his point?

---

<!-- _class: closing -->
<div class="accent-bar"></div>
<div class="deco-panel"></div>
<div class="closing-content">
  <h1>Read Before Next Session</h1>
  <h2>See the companion document for full argument, quotes, and references</h2>
</div>
<div class="closing-footer">Understanding Artificial Intelligence</div>
