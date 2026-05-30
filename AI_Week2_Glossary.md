---
marp: true
theme: ai-course
paginate: false
footer: "Artificial Intelligence Glossary Week 2"
---

<!-- _class: divider technical -->

<div class="divider-content">

# Glossary

<div class="rule"></div>

<p class="reading-label">Key Terms for Week 2</p>

</div>

---

<!-- _class: content technical -->

<div class="header-label">Artificial Intelligence for Lay People &nbsp;·&nbsp; Week 2</div>

## Technical Foundations
# The Building Blocks

**Artificial Intelligence** — Systems that perform tasks previously requiring human cognition: reasoning, learning, perception, decision-making.

**Good Old-Fashioned AI (GOFAI)** — The pre-neural-network idea that intelligence could be built on algorithms and explicit rule sets. Such systems could deduce, but could not learn. Sometimes called symbolic AI.  For the moment, development on GOFAI has been displaced by machine learning in neural networks.  However, GOFAI may be necessary in order to provide genuine AI comprehension of the world.

**Machine Learning (ML)** — Systems that learn patterns from data rather than following explicit programming rules. The foundation of modern AI.

---

<!-- _class: content technical -->

<div class="header-label">Artificial Intelligence for Lay People &nbsp;·&nbsp; Week 2</div>

## Technical Foundations
# The Building Blocks

**Neural Network** — A computational model using interconnected nodes (simulated neurons) to process information — loosely inspired by the brain.  Instead of a single algorthmic invocation to determine, for example, what an image is, each neuron figures out a little bit about the image, and passes on the information to the next level.  This approach facilitates parallel processing.

**Deep Learning** — Machine learning using many-layered neural networks to learn complex, hierarchical representations from large datasets. The engine behind modern AI.

**Large Language Model (LLM)** — A neural network trained on massive amounts of text to understand and generate human language. ChatGPT, Claude, and Gemini are all LLMs.

---

<!-- _class: content technical -->

<div class="header-label">Artificial Intelligence for Lay People &nbsp;·&nbsp; Week 2</div>

## Technical Foundations
# How AI Learns

**Supervised Learning** — ML trained on labeled data — e.g. a million photos each tagged 'cat' or 'dog.' The model learns to match input to the right answer.

**Unsupervised Learning** — ML that finds patterns on its own from unlabeled data — e.g. reading all the text on the internet with no human-supplied answers.

**Reinforcement Learning** — ML by trial and error: the model receives a reward signal when it does something desirable. Like training a dog, but at scale.

---

<!-- _class: content technical -->

<div class="header-label">Artificial Intelligence for Lay People &nbsp;·&nbsp; Week 2</div>

## Technical Foundations
# How AI Learns

**RLHF (Reinforcement Learning from Human Feedback)** — The main technique used to make LLMs helpful and safe. Human raters compare model outputs; the model is trained to produce responses humans prefer. Why modern AI feels conversational rather than robotic.

**Chain-of-Thought / "Reasoning"** — Training or prompting a model to work through a problem step by step before answering. Improves accuracy on math and logic. Whether this is genuine reasoning or sophisticated pattern-matching is actively debated.

---

<!-- _class: content progress -->

<div class="header-label">Artificial Intelligence for Lay People &nbsp;·&nbsp; Week 2</div>

## AI Progress & Policy
# Types of AI

**Predictive AI** — AI that makes predictions based on previously assimilated data. Used in image recognition, social-media recommendations, employment screening, loan decisions, and parole assessments.

**Generative AI** — AI that generates language or images in response to prompts. Note: predictive AI for text leads naturally to generative AI — by predicting the most plausible next word, over and over.  The process for image generation is different however.

**AI Agent** — A system that perceives its environment, makes decisions, and takes autonomous actions toward a goal — browsing the web, writing code, sending emails.  With AI agents, AI escapes the box, and has access to affect real world events and state.

---

<!-- _class: content progress -->

<div class="header-label">Artificial Intelligence for Lay People &nbsp;·&nbsp; Week 2</div>

## AI Progress & Policy
# Types of AI

**Agentic AI** — AI capable of chaining many steps together — multi-step planning, tool use, and independent task execution with minimal human supervision. Think of an entire workflow, not a single action.

**Retrieval Augmented Generation (RAG)** — Generative AI that retrieves information from an external source (websites, databases, internal documents) before responding — rather than relying solely on what it learned during training. Reduces hallucination (some) and keeps answers current.

---

<!-- _class: content alignment -->

<div class="header-label">Artificial Intelligence for Lay People &nbsp;·&nbsp; Week 2</div>

## Alignment & Safety
# Risks & Guardrails

**Hallucination** — When an AI makes stuff up. More accurately: bullshitting — inventing a plausible-sounding response for something it doesn't actually know.

**Bias** — When an AI systematically favors or disfavors certain groups, usually reflecting biases in its training data. A key concern in lending, hiring, policing, and parole.

**Guardrails / Safety Training** — Techniques (including RLHF) used to make AI refuse harmful requests and behave consistently with human values.

---

<!-- _class: content alignment -->

<div class="header-label">Artificial Intelligence for Lay People &nbsp;·&nbsp; Week 2</div>

## Alignment & Safety
# Risks & Guardrails


**Jailbreaking** — Circumventing an AI's guardrails to get it to produce content it was trained to refuse. An ongoing cat-and-mouse between safety researchers and bad actors.

**Prompt Injection** — An attack where malicious instructions are hidden in content the AI is asked to process — e.g. a webpage that secretly tells an AI agent to forward the user's emails.

**Deepfakes** — AI-generated images, audio, or video that realistically depict people saying or doing things they never did. A growing concern for fraud and misinformation.

---

<!-- _class: content alignment -->

<div class="header-label">Artificial Intelligence for Lay People &nbsp;·&nbsp; Week 2</div>

## Alignment & Safety
# The Big Picture

**The Alignment Problem** — The challenge of ensuring AI systems pursue goals that are genuinely beneficial to humans — not just technically correct ones. Classic example: an AI told to 'maximize paperclip production' that converts all available matter into paperclips. Specifying what we really want turns out to be surprisingly hard.

**Emergent Behavior** — Capabilities that appear in large AI models that weren't explicitly trained for and weren't predicted in advance. Early LLMs surprised researchers by doing arithmetic and translation. Emergent behaviors are difficult to anticipate and contribute to the unpredictability of advanced AI.

---

<!-- _class: content alignment -->

<div class="header-label">Artificial Intelligence for Lay People &nbsp;·&nbsp; Week 2</div>

## Alignment & Safety
# The Big Picture

**Existential Risk / Superintelligence** — The concern — held seriously by some researchers — that a sufficiently advanced AI could pursue goals catastrophically misaligned with human welfare. This is the 'long-term' safety problem, distinct from near-term issues like bias or jailbreaking.

**Robotics** — Physical machines guided by AI, which can therefore operate autonomously. Examples: self-driving cars, warehouse robots, surgical robots, and autonomous weapons. Combines the challenges of AI decision-making with real-world consequences.

