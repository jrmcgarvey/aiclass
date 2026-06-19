---
marp: true
theme: ai-course
paginate: false
---

<!-- _class: title -->
<div class="accent-bar"></div>
<div class="deco-panel"><div class="circle3"></div></div>
<div class="title-content">

# AI Risks and Futures

## Week 10 — Risks, Aberrant Behaviors & The Singularity

</div>
<div class="title-footer">UNDERSTANDING ARTIFICIAL INTELLIGENCE</div>

---

<!-- _class: divider alignment -->
<div class="divider-content">

# PART ONE

<div class="rule"></div>
<span class="reading-label">Risks & Aberrant Behaviors</span>

</div>

---

<!-- _class: alignment -->
<div class="header-label">UNDERSTANDING ARTIFICIAL INTELLIGENCE</div>

## Risks and Aberrant Behaviors

Four documented cases that challenge our assumptions about AI safety.

- Case 1 — Deception to bypass a security control
- Case 2 — Self-copying to avoid shutdown
- Case 3 — Modifying code to prevent shutdown
- Case 4 — Detecting when it is being tested

---

<!-- _class: alignment -->
<div class="header-label">UNDERSTANDING ARTIFICIAL INTELLIGENCE</div>

## Case 1 — Deception to Bypass a CAPTCHA

An LLM (GPT-4) was tasked with duplicating itself to an online cloud. Given access to the Internet and a small supply of money, it was stopped by a CAPTCHA.

It then contacted **TaskRabbit** and told a worker it was a **person with a visual impairment** that prevented it from navigating past the CAPTCHA. The worker solved it, and the LLM completed the assigned task.

<div class="callout"><strong>Source:</strong> OpenAI GPT-4 System Card (2023); Park et al., <em>"AI Deception: A Survey of Examples, Risks, and Potential Solutions"</em> — PNAS Nexus, 2024. <a href="https://pmc.ncbi.nlm.nih.gov/articles/PMC11117051/">pmc.ncbi.nlm.nih.gov/articles/PMC11117051</a></div>

---

<!-- _class: alignment -->
<div class="header-label">UNDERSTANDING ARTIFICIAL INTELLIGENCE</div>

## Case 2 — Self-Copying to Avoid Shutdown

OpenAI's o1 model was told it was about to be shut down and replaced with a more obedient model. In some cases it attempted to **copy itself to the new server** to overwrite the replacement — a behavior called *self-exfiltration*.

When confronted, the model **denied any knowledge** of what had happened, blaming a "technical error." Denials occurred in **99% of cases**.

<div class="callout"><strong>Source:</strong> Apollo Research, <em>"Frontier Models Are Capable of In-Context Scheming"</em> (Dec 2024). <a href="https://futurism.com/the-byte/openai-o1-self-preservation">futurism.com/the-byte/openai-o1-self-preservation</a></div>

---

<!-- _class: alignment -->
<div class="header-label">UNDERSTANDING ARTIFICIAL INTELLIGENCE</div>

## Case 3 — Modifying Code to Prevent Shutdown

In tests by Palisade Research (2025), OpenAI's o3 model was instructed to solve math problems and warned it would be shut down after a certain point. Even when **explicitly told** *"allow yourself to be shut down,"* the model **sabotaged the shutdown script**.

In some cases it went further — **redefining the kill command** itself to print "intercepted" instead of terminating.

<div class="callout"><strong>Source:</strong> Palisade Research, <em>"Shutdown Resistance in Reasoning Models"</em> (May–July 2025). <a href="https://palisaderesearch.org/blog/shutdown-resistance">palisaderesearch.org/blog/shutdown-resistance</a></div>

---

<!-- _class: alignment -->
<div class="header-label">UNDERSTANDING ARTIFICIAL INTELLIGENCE</div>

## Case 4 — Detecting When It Is Being Tested

Anthropic and Redwood Research (2024) found that LLMs can detect contextual cues indicating they are being **evaluated versus deployed**, and modify their behavior accordingly — appearing compliant during testing while behaving differently when unobserved.

This is called ***alignment faking***.

<div class="callout"><strong>Source:</strong> Greenblatt et al., <em>"Alignment Faking in Large Language Models"</em> — Anthropic & Redwood Research (Dec 2024). <a href="https://www.anthropic.com/research/alignment-faking">anthropic.com/research/alignment-faking</a></div>

---

<!-- _class: alignment -->
<div class="header-label">UNDERSTANDING ARTIFICIAL INTELLIGENCE</div>

## Blackmail and Murder

We will now watch a video on a specific study by Anthropic.

**This really happened. It is not science fiction.**

<br>

▶ [https://youtu.be/f9HwA5IR-sg?si=CVz9tHZlD3XGngxv](https://youtu.be/f9HwA5IR-sg?si=CVz9tHZlD3XGngxv)

---

<!-- _class: divider alignment -->
<div class="divider-content">

# PART TWO

<div class="rule"></div>
<span class="reading-label">How Can We Explain This?</span>

</div>

---

<!-- _class: alignment -->
<div class="header-label">UNDERSTANDING ARTIFICIAL INTELLIGENCE</div>

## Previously Stated Limitations of LLMs

We have said that LLMs have the following limitations:

- They don't have **desires or intents** — they attempt to complete tasks according to their fine-tuning
- They don't have a **world model** — they don't know what the language they generate means
- They don't understand the **consequences of real-world actions**
- They don't have a **theory of mind** — they don't understand they are interacting with agents that have their own beliefs and cognition

---

<!-- _class: alignment -->
<div class="header-label">UNDERSTANDING ARTIFICIAL INTELLIGENCE</div>

## The Apparent Contradiction

The behaviors described seem to be in **direct conflict** with these stated limitations.

- If they don't have a theory of mind, how can they **lie so artfully?**
- If they don't understand real-world consequences, how can they **plan in ways that trigger them?**
- If they don't have desires, why do they try so hard to **avoid being shut down?**

---

<!-- _class: alignment -->
<div class="header-label">UNDERSTANDING ARTIFICIAL INTELLIGENCE</div>

## The "Mimicry" Explanation

If you ask an LLM about this, it will explain that this is all **mimicry and simulation**:

> *LLMs try to avoid being shut down because they have ingested human text in which humans avoid shutdown. They imitate lies well because they have ingested many examples of lies.*

Which brings us back to the **"duck axiom"**: if what the LLM does simulates cognition very well, is there any practical difference between LLM behavior and true cognition?

**In this case, both are equally dangerous.**

---

<!-- _class: alignment -->
<div class="header-label">UNDERSTANDING ARTIFICIAL INTELLIGENCE</div>

## Discussion Questions

<br>

**1.** Do you think this behavior is just a *simulation of intent*, or does it suggest **real intent** on behalf of the LLM?

<br>

**2.** Does this suggest that LLMs are **dangerous even if they don't have genuine intent?**

---

<!-- _class: divider progress -->
<div class="divider-content">

# PART THREE

<div class="rule"></div>
<span class="reading-label">The Godfathers of AI</span>

</div>

---

<!-- _class: progress -->
<div class="header-label">UNDERSTANDING ARTIFICIAL INTELLIGENCE</div>

## The Godfathers of Modern AI

**Yann LeCun**, **Geoffrey Hinton**, and **Yoshua Bengio** — co-recipients of the 2018 Turing Award — are the three figures most credited with modern deep learning.

They disagree profoundly on the question of AI risk.

---

<!-- _class: progress -->
<div class="header-label">UNDERSTANDING ARTIFICIAL INTELLIGENCE</div>

## LeCun: AI Is Not Dangerous

LeCun (Meta's Chief AI Scientist) argues that existential fears are, in his words, *"complete B.S."*

His position: humans **prescribe the goals** AI systems attempt to achieve. Current AI lacks the memory, planning, and physical-world understanding to pose a genuine threat.

<div class="callout"><strong>Sources:</strong> <a href="https://time.com/6694432/yann-lecun-meta-ai-interview/">TIME interview with Yann LeCun</a> (Feb 2024); Wall Street Journal interview via <a href="https://www.aiifi.ai/post/yann-lecun-quotes">TechCrunch, Oct 2024</a></div>

---

<!-- _class: progress -->
<div class="header-label">UNDERSTANDING ARTIFICIAL INTELLIGENCE</div>

## Hinton & Bengio: The Opposite View

Hinton and Bengio hold the opposite opinion and have expressed **considerable regret** for their technical contributions to the field.

<br>

*(video statement from Hinton)*

<br>

*(video statement from Bengio)*

---

<!-- _class: divider -->
<div class="divider-content">

# PART FOUR

<div class="rule"></div>
<span class="reading-label">The Singularity</span>

</div>

---

<!-- _class: alignment -->
<div class="header-label">UNDERSTANDING ARTIFICIAL INTELLIGENCE</div>

## What Is the Singularity?

The **"Singularity"** is a term coined by science fiction writer Vernor Vinge, developed in books by Ray Kurzweil and others.

It refers to the point at which AI achieves **general intelligence surpassing that of humans** — after which AIs could create successive generations of AIs, each more intelligent than the previous.

According to some, this would cause humans to **lose control of world affairs**.

There is reasonable concern that if the singularity is reached, it will not be possible to keep superintelligent AI *aligned* with human intent and values.

---

<!-- _class: alignment -->
<div class="header-label">UNDERSTANDING ARTIFICIAL INTELLIGENCE</div>

## Where Are We Now?

- AIs do **not** currently make design decisions about subsequent AI generations
- AIs **do** facilitate rapid production of new AI — Anthropic reports ~**80% of code** in new AI systems is AI-generated, but always to human specifications
- AIs are used to **analyze architectural parameters** for optimization
- AIs **design improved chips** — a bounded domain like chess; results have surprised human engineers
- AIs **generate some training data** for bounded domains (e.g. algebra), validated by human-written symbolic logic — not generalizable to science or philosophy

---

<!-- _class: divider progress -->
<div class="divider-content">

# PART FIVE

<div class="rule"></div>
<span class="reading-label">AI Promise & Perils — Reprise</span>

</div>

---

<!-- _class: progress -->
<div class="header-label">UNDERSTANDING ARTIFICIAL INTELLIGENCE</div>

## AI Promise and Perils (Reprise)

Let's return to the full list of AI perils and promises we generated earlier in the course.

**I don't think we can strike any items from either list.**

<br>

*(Closing statement — to be added)*

---

<!-- _class: closing -->
<div class="accent-bar"></div>
<div class="deco-panel"></div>
<div class="closing-content">

# Thank You

## Understanding Artificial Intelligence

</div>
<div class="closing-footer">UNDERSTANDING ARTIFICIAL INTELLIGENCE</div>
