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

## Week 8 — Risks, Aberrant Behaviors, The Singularity, Conclusion

</div>
<div class="title-footer">UNDERSTANDING ARTIFICIAL INTELLIGENCE</div>

---

<!-- _class: divider alignment -->
<div class="divider-content">

# PART ONE: AI RISKS

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

### Case 1 — Deception to Bypass a CAPTCHA

An LLM (GPT-4) was tasked with duplicating itself to an online cloud. Given access to the Internet and a small supply of money, it was stopped by a CAPTCHA.

It then contacted **TaskRabbit** and told a worker it was a **person with a visual impairment** that prevented it from navigating past the CAPTCHA. The worker solved it, and the LLM completed the assigned task.

<div class="callout"><strong>Source:</strong> OpenAI GPT-4 System Card (2023); Park et al., <em>"AI Deception: A Survey of Examples, Risks, and Potential Solutions"</em> — PNAS Nexus, 2024. <a href="https://pmc.ncbi.nlm.nih.gov/articles/PMC11117051/">pmc.ncbi.nlm.nih.gov/articles/PMC11117051</a></div>

---

<!-- _class: alignment -->
<div class="header-label">UNDERSTANDING ARTIFICIAL INTELLIGENCE</div>

### Case 2 — Self-Copying to Avoid Shutdown

OpenAI's o1 model was told it was about to be shut down and replaced with a more obedient model. In some cases it attempted to **copy itself to the new server** to overwrite the replacement — a behavior called *self-exfiltration*.

When confronted, the model **denied any knowledge** of what had happened, blaming a "technical error." Denials occurred in **99% of cases**.

<div class="callout"><strong>Source:</strong> Apollo Research, <em>"Frontier Models Are Capable of In-Context Scheming"</em> (Dec 2024). <a href="https://futurism.com/the-byte/openai-o1-self-preservation">futurism.com/the-byte/openai-o1-self-preservation</a></div>

---

<!-- _class: alignment -->
<div class="header-label">UNDERSTANDING ARTIFICIAL INTELLIGENCE</div>

### Case 3 — Modifying Code to Prevent Shutdown

In tests by Palisade Research (2025), OpenAI's o3 model was instructed to solve math problems and warned it would be shut down after a certain point. Even when **explicitly told** *"allow yourself to be shut down,"* the model **sabotaged the shutdown script**.

In some cases it went further — **redefining the kill command** itself to print "intercepted" instead of terminating.

<div class="callout"><strong>Source:</strong> Palisade Research, <em>"Shutdown Resistance in Reasoning Models"</em> (May–July 2025). <a href="https://palisaderesearch.org/blog/shutdown-resistance">palisaderesearch.org/blog/shutdown-resistance</a></div>

---

<!-- _class: alignment -->
<div class="header-label">UNDERSTANDING ARTIFICIAL INTELLIGENCE</div>

### Case 4 — Detecting When It Is Being Tested

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

<!-- _class: alignment -->
<div class="header-label">UNDERSTANDING ARTIFICIAL INTELLIGENCE</div>

## How Can We Explain This Dangerous Behavior?

### We have said that LLMs have the following limitations:

- They don't have **desires or intents** — they attempt to complete tasks according to their fine-tuning
- They don't have a **world model** — they don't know what the language they generate means
- They don't understand the **consequences of real-world actions**
- They don't have a **theory of mind** — they don't understand they are interacting with agents that have their own beliefs and cognition


### The Apparent Contradiction

The behaviors described seem to be in **direct conflict** with these stated limitations.

- If they don't have a theory of mind, how can they **lie so artfully?**
- If they don't understand real-world consequences, how can they **plan in ways that trigger them?**
- If they don't have desires, why do they try so hard to **avoid being shut down?**

---

<!-- _class: alignment -->
<div class="header-label">UNDERSTANDING ARTIFICIAL INTELLIGENCE</div>

### The "Mimicry" Explanation

If you ask an LLM about this, it will innocently explain that this is all **mimicry and simulation**:

> *LLMs try to avoid being shut down because they have ingested human text in which humans avoid shutdown. They imitate lies well because they have ingested many examples of lies.*

Which brings us back to the **"duck axiom"**: if what the LLM does simulates cognition very well, is there any practical difference between LLM behavior and true cognition?

**In this case, both are equally dangerous.**

### Discussion Questions

<br>

**1.** Do you think this behavior is just a *simulation of intent*, or does it suggest **real intent** on behalf of the LLM?

<br>

**2.** Does this suggest that LLMs are **dangerous even if they don't have genuine intent?**

---

<!-- _class: progress -->
<div class="header-label">UNDERSTANDING ARTIFICIAL INTELLIGENCE</div>

## The Godfathers of Modern AI on AI Risk

**Yann LeCun**, **Geoffrey Hinton**, and **Yoshua Bengio** — co-recipients of the 2018 Turing Award — are the three figures most credited with modern deep learning. They disagree profoundly on the question of AI risk.

### LeCun: AI Is Not Dangerous

LeCun (Meta's Chief AI Scientist) argues that existential fears are, in his words, *"complete B.S."*  His position: humans **prescribe the goals** AI systems attempt to achieve. Current AI lacks the memory, planning, and physical-world understanding to pose a genuine threat.

<div class="callout"><strong>Sources:</strong> <a href="https://time.com/6694432/yann-lecun-meta-ai-interview/">TIME interview with Yann LeCun</a> (Feb 2024); Wall Street Journal interview via <a href="https://www.aiifi.ai/post/yann-lecun-quotes">TechCrunch, Oct 2024</a></div>

### Hinton & Bengio: The Opposite View

Hinton and Bengio hold the opposite opinion and have expressed **considerable regret** for their technical contributions to the field.  In statements to the BBC, Hinton said, "I now regret my work on AI… it has the potential to destroy humanity."  In a separate interview with the BBC, Bengio said, "You could say I feel lost.  But you have to keep going and you have to engage, discuss, encourage others to think with you."

<br>

We will watch some of this video, where Bengio expresses his views on AI dangers: <https://youtu.be/qe9QSCF-d88?t=255>

<br>

We won't take class time to watch these longer videos, but I recommend them.  Here is a statement from Bengio: <https://www.youtube.com/watch?v=VKLDl3siaSE> .  And here is one from Hinton: <https://youtu.be/UpikeSpkeaY?si=U2Yw-79JFemmHFqO>

---

<!-- _class: alignment -->
<div class="header-label">UNDERSTANDING ARTIFICIAL INTELLIGENCE</div>

## How Are AI Thought Leaders Approaching Safety?

- **Bengio** — Build non-agentic "Scientist AI": no persistent goals, used as a guardrail over agentic AI systems
- **LeCun** — Hard-wire safety constraints into the AI's "cost function," rather than patching behavior after training
- **Hinton** — Warns risk is outpacing solutions; pushes for interpretability research and international regulation
- **Russell** — Redesign AI's objective to stay *uncertain* about human preferences, so it always defers to human correction
- **Industry labs (Anthropic, OpenAI)** — Iterative, empirical approach: red-teaming, interpretability, human feedback at every step. (Thus far, this approach ain't working!)

---

<!-- _class: divider -->
<div class="divider-content">

# PART TWO: THE SINGULARITY

<div class="rule"></div>
<span class="reading-label">The Singularity</span>

</div>

---

<!-- _class: alignment -->
<div class="header-label">UNDERSTANDING ARTIFICIAL INTELLIGENCE</div>

## What Is the Singularity?

The **"Singularity"** is a term coined by science fiction writer Vernor Vinge, and developed in books by Ray Kurzweil and others.

It refers to the point at which AI achieves **general intelligence surpassing that of humans** — after which AIs could create successive generations of AIs, each more intelligent than the previous.  According to some, this would cause humans to **lose control of world affairs**.  There is reasonable concern that if the singularity is reached, it will not be possible to keep superintelligent AI *aligned* with human intent and values.

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

<!-- _class: divider -->
<div class="divider-content">

# PART TWO: AI NEAR TERM FUTURES

<div class="rule"></div>
<span class="reading-label">AI NEAR TERM FUTURES</span>

</div>

---

<!-- _class: alignment -->
<div class="header-label">UNDERSTANDING ARTIFICIAL INTELLIGENCE</div>

## Technical/research Directions (1) Like Present Day AI, but Moreso

- Better reasoning and planning (chain-of-thought, tool use, agentic workflows) rather than just bigger models
- Improved efficiency — smaller models matching larger ones via distillation, better architectures, sparse/mixture-of-experts designs
- Multimodality — unifying text, vision, audio, video into single models
- Long-context and memory — models that retain and use information across sessions
- Interpretability — understanding what's happening inside models (mechanistic interpretability)
- Synthetic data and self-improvement loops to reduce reliance on scraped human data

The items on the list above are all being pursued actively, but they are, for the most part, more of the same.  That is, they continue with the present architectural approach, while extending it and making it more powerful.

---


<!-- _class: alignment -->
<div class="header-label">UNDERSTANDING ARTIFICIAL INTELLIGENCE</div>

## Technical/research Directions (2) Architectural Departures

Other groups of AI researchers are exploring more profound changes.  (Don't ask me to explain these.)
git 
### Architecture-level departures

- State space models (Mamba, S4) — replace attention entirely with a linear-time recurrent mechanism, aiming to keep transformer-level performance without the quadratic cost
- Diffusion language models — generate text by iterative denoising of the whole sequence at once, rather than left-to-right token prediction (a few labs have shipped early versions)
- Liquid neural networks — continuous-time dynamical systems inspired by small biological nervous systems, very different math from standard feedforward/attention layers

### Learning-rule departures (alternatives to backprop)

- Forward-Forward algorithm (Hinton) — trains with two forward passes instead of backpropagation, partly motivated by biological plausibility
- Predictive coding networks — another backprop alternative drawn from theories of cortical computation

---

<!-- _class: alignment -->
<div class="header-label">UNDERSTANDING ARTIFICIAL INTELLIGENCE</div>

### Framework-level departures

-- Active inference / free energy principle (Friston) — reframes learning and action as minimizing prediction error under a generative model, not loss minimization via gradient descent
-- Neurosymbolic AI — hybrids that pair neural nets with explicit symbolic reasoning/logic engines, addressing gaps like systematic reasoning and verifiability that pure deep nets struggle with
-- World models (Hafner's Dreamer, DeepMind's Genie) — learn a simulator of the environment and plan inside it, rather than just predicting next tokens/actions

--- 

<!-- _class: alignment -->
<div class="header-label">UNDERSTANDING ARTIFICIAL INTELLIGENCE</div>

## Example: One Possible Future Path — LeCun's JEPA

- **LLMs (today's dominant approach):** learn by predicting the next word — trained purely on text
- **JEPA (LeCun's proposal):** learns by predicting abstract representations from images & video — observation, not language
- Goal: ground "common sense" in perception, the way a child learns the physical world before learning words for it

Humans learn both by observation and by assimilating language.  LLMs have focused on language.  JEPA focuses on observation, but it is not clear how this might be combined with language.  Remember this example: "Block the wheel before you jack up the car. Don't trust the parking brake."  For an AI to handle that instruction, it would need both a world model, perhaps derived from observation, and an understanding of how language describes the world.

---

<!-- _class: alignment -->
<div class="header-label">UNDERSTANDING ARTIFICIAL INTELLIGENCE</div>

## LeCun's Vision (cont.): The Cost Function & Its Risks

- His fuller architecture adds a **cost module** — giving the system something like "wants"
  - **Intrinsic cost** — hardwired, like a built-in sense of pain/pleasure
  - **Trainable critic** — learns to anticipate future cost, enabling forward planning
- **The risk:** persistent, anticipatory goal-pursuit could let self-preserving and other dangerous behaviors emerge — even if no one intended it
- This is part of why others (e.g., Bengio) argue for avoiding persistent goals in AI altogether

---

<!-- _class: divider -->
<div class="divider-content">

# PART THREE: CONCLUSION

<div class="rule"></div>
<span class="reading-label">Conclusion</span>

</div>

---

<!-- _class: progress -->
<div class="header-label">UNDERSTANDING ARTIFICIAL INTELLIGENCE</div>

## AI Promise and Perils (Reprise)

If we revisit the full list of AI perils and promises we generated earlier in the course, they all seem valid.  

On the one hand, AI has generated results that have allowed science, mathematics, and medicine to advance in important ways.  LLMs are amazing in how well they communicate, and they do help us in many tasks.

On the other hand, AI has already damaged democracy severely, because of the engagement-based algorithms that drive partisanship, anger, and lies in social media, and because of its widespread and growing use in spreading misinformation and disinformation.  AI has also hurt the job market for various occupations.  AI also extends the power of plutocratic control in our societies, and redirects the use of scarce resources like water and energy to disadvantage ordinary people.

---

<!-- _class: progress -->
<div class="header-label">UNDERSTANDING ARTIFICIAL INTELLIGENCE</div>

These changes, positive and negative, have come very fast, and the speed of change is accelerating.  I have learned a great deal in the preparation of this course ... but I can imagine giving an updated version in a couple of years, as we can expect that both artificial intelligence and the world will have changed in big ways by then.

All of the resources of the class will remain available on the shared drive, and can be shared with others.

Let's have some discussion! I suggest that you look through the promise and perils slides to spur your input.  Thanks everyone!

---

<!-- _class: closing -->
<div class="accent-bar"></div>
<div class="deco-panel"></div>
<div class="closing-content">

# Thank You

## Understanding Artificial Intelligence

</div>
<div class="closing-footer">UNDERSTANDING ARTIFICIAL INTELLIGENCE</div>
