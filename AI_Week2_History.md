---
marp: true
theme: ai-course
paginate: false
html: true
---

<!-- _class: title -->

<div class="accent-bar"></div>
<div class="deco-panel"><div class="circle3"></div></div>

<div class="title-content">

<p class="course-label">Week 2</p>

# Introduction to the Concepts, Terminology, and People in<br>Artificial Intelligence

</div>

<div class="title-footer">Babbage &nbsp;·&nbsp; Turing &nbsp;·&nbsp; Von Neumann &nbsp;·&nbsp; Minsky &nbsp;·&nbsp; LeCun &nbsp;·&nbsp; Hinton &nbsp;·&nbsp; Bengio</div>

---

<p>This week, we will start with the video "What is AI?" from the Great Courses offering.  Then, we'll mention some of the folks below, and focus on key concepts in the glossary, which is a separate slide deck.</p>

---

<!-- _class: content technical -->

![bg right:30%](https://upload.wikimedia.org/wikipedia/commons/thumb/6/6b/Charles_Babbage_-_1860.jpg/500px-Charles_Babbage_-_1860.jpg)

## 19th Century Foundations &nbsp;·&nbsp; The Luminaries
# Charles Babbage &nbsp;<small>1791–1871</small>

*Inventor of the first mechanical computer*

Babbage was a British mathematician who conceived the Difference Engine (1822) and the Analytical Engine (1837) — a mechanical device with an arithmetic logic unit, conditional branching, and loops. It was never built in his lifetime, but the design contained every key element of a modern computer. He was obsessed, underfunded, and largely unappreciated. Sound familiar?

<div class="callout"><strong>★</strong> Babbage reportedly hated street musicians so intensely he campaigned for a law against them.</div>

---

<!-- _class: content technical -->

![bg right:30%](https://upload.wikimedia.org/wikipedia/commons/thumb/4/4c/Ada_Lovelace_daguerreotype_by_Antoine_Claudet_1843_-_cropped.png/500px-Ada_Lovelace_daguerreotype_by_Antoine_Claudet_1843_-_cropped.png)

<div class="header-label">Artificial Intelligence for Lay People &nbsp;·&nbsp; Week 2</div>

## 19th Century Foundations &nbsp;·&nbsp; The Luminaries
# Ada Lovelace &nbsp;<small>1815–1852</small>

*World's first computer programmer*

Daughter of the poet Lord Byron, Ada Lovelace translated an Italian article on Babbage's Analytical Engine — and added notes three times longer than the original. Those notes contained what is widely regarded as the first algorithm intended to be executed by a machine: a method to compute Bernoulli numbers. She also speculated whether a machine could ever originate anything, or only do what we know how to order it to do — a question we are still arguing about today.

<div class="callout"><strong>★</strong> She called herself an "Analyst and Metaphysician" — a title that would be equally apt for most AI researchers today.</div>


---

<!-- _class: content technical -->

![bg right:30%](https://upload.wikimedia.org/wikipedia/commons/thumb/c/ce/Alan_turing_header.jpg/500px-Alan_turing_header.jpg)

<div class="header-label">Artificial Intelligence for Lay People &nbsp;·&nbsp; Week 2</div>

## Mid-20th Century &nbsp;·&nbsp; The Luminaries
# Alan Turing &nbsp;<small>1912–1954</small>

*Father of theoretical computer science and AI*

Turing formalized the concept of computation with the Turing Machine (1936), broke German Enigma codes in WWII, and in 1950 published "Computing Machinery and Intelligence" — proposing what became the Turing Test as a measure of machine intelligence. He asked the question that still haunts AI: *"Can machines think?"* His tragic death at 41 from cyanide poisoning (likely suicide, after state-mandated chemical castration for homosexuality) cut short what might have been another 30 years of foundational work.

<div class="callout"><strong>★</strong> The programming language Ada — named after Lovelace — was commissioned by the U.S. Department of Defense and is still used in aircraft and air traffic control today.</div>


---

<!-- _class: content technical -->

![bg right:30%](https://upload.wikimedia.org/wikipedia/commons/5/5e/JohnvonNeumann-LosAlamos.gif)

<div class="header-label">Artificial Intelligence for Lay People &nbsp;·&nbsp; Week 2</div>

## Mid-20th Century &nbsp;·&nbsp; The Luminaries
# John von Neumann &nbsp;<small>1903–1957</small>

*Architect of the modern computer*

Von Neumann was arguably the greatest mathematician of the 20th century — contributing to quantum mechanics, game theory, nuclear physics, and economics. His 1945 draft report describing the EDVAC computer gave us the "von Neumann architecture": a stored-program computer where instructions and data share the same memory. Every laptop, phone, and server in the world still uses this basic design. He was reportedly so fast at mental arithmetic that colleagues suspected he was pretending to be human.

<div class="callout"><strong>★</strong> When asked why a computer needed a memory, he is said to have replied: "So it can remember what it's doing."</div>


---

<!-- _class: content technical -->

![bg right:30%](https://upload.wikimedia.org/wikipedia/commons/thumb/a/a0/1954_Walter_Pitts_and_a_blackboard.jpg/500px-1954_Walter_Pitts_and_a_blackboard.jpg)

<div class="header-label">Artificial Intelligence for Lay People &nbsp;·&nbsp; Week 2</div>

## Mid-20th Century &nbsp;·&nbsp; The Luminaries
# Warren McCulloch & Walter Pitts &nbsp;<small>1898–1969 &nbsp;·&nbsp; 1923–1969</small>

*Inventors of the first mathematical model of a neuron*

In 1943, neurophysiologist McCulloch and teenage prodigy Pitts (who had run away from home at 12 to study logic) published "A Logical Calculus of the Ideas Immanent in Nervous Activity." Their McCulloch-Pitts neuron showed that networks of simple binary units could, in principle, compute any logical function. This was the theoretical seed of every neural network that followed — including the one that wrote your email autocomplete. Pitts was discovered by Norbert Wiener living in the University of Chicago library.

<div class="callout"><strong>★</strong> Walter Pitts taught himself Greek and Latin at age 12 by reading the Principia Mathematica in a library where he was hiding from bullies.</div>

*Photo: Walter Pitts*


---

<!-- _class: content technical -->

![bg right:30%](https://upload.wikimedia.org/wikipedia/commons/3/3b/Frank_Rosenblatt.jpg)

<div class="header-label">Artificial Intelligence for Lay People &nbsp;·&nbsp; Week 2</div>

## Early AI (1950s–60s) &nbsp;·&nbsp; The Luminaries
# Frank Rosenblatt &nbsp;<small>1928–1971</small>

*Inventor of the Perceptron — the first trainable neural network*

Rosenblatt's Perceptron (1958) was the first algorithm that could actually learn from data — not just execute fixed logic. The U.S. Navy built a room-sized version and the New York Times predicted it would "be able to walk, talk, see, write, reproduce itself, and be conscious of its existence." Eleven years later, Minsky and Papert proved the Perceptron couldn't solve basic problems like XOR — deflating the hype and ushering in the first AI winter. Rosenblatt drowned in a boating accident in 1971 at 43, before seeing the vindication of his ideas.

<div class="callout"><strong>★</strong> The Navy's Mark 1 Perceptron used 400 photocells connected to motors by a random tangle of wires that was literally adjusted by hand.</div>


---

<!-- _class: content technical -->

![bg right:30%](https://upload.wikimedia.org/wikipedia/commons/thumb/f/f9/Marvin_Minsky_at_OLPCb_%283x4_cropped%29.jpg/500px-Marvin_Minsky_at_OLPCb_%283x4_cropped%29.jpg)

<div class="header-label">Artificial Intelligence for Lay People &nbsp;·&nbsp; Week 2</div>

## Early AI (1950s–60s) &nbsp;·&nbsp; The Luminaries
# Marvin Minsky &nbsp;<small>1927–2016</small>

*AI pioneer — and inadvertent author of the first AI winter*

Minsky was one of the founders of the MIT AI Lab and a brilliant, provocative thinker. His 1969 book *Perceptrons* (with Seymour Papert) rigorously proved the limitations of single-layer neural networks — killing funding for the field for a decade, as was his intent.  He wanted to keep the dollars going only to GOFAI. The critique was technically correct, but Minsky and Papert failed to anticipate multi-layer networks, so more fundamentally, it was wrong. The consequence was the "AI winter", when all funding and progress on AI dried up for years.  It is a classic case of a valid proof of limitation being over-generalized into a dismissal of an entire approach. History did not vindicate the dismissal.

<div class="callout"><strong>★</strong> Minsky was convinced AI was 5–10 years away for most of his career. He said it in 1967. He was still saying it before his death in 2016.</div>

---

<!-- _class: content technical -->

![bg right:30%](https://upload.wikimedia.org/wikipedia/commons/thumb/8/8e/Laura_Chaubard_%26_Yann_Le_Cun_-_2024_%2853814052697%29_%28cropped%29.jpg/500px-Laura_Chaubard_%26_Yann_Le_Cun_-_2024_%2853814052697%29_%28cropped%29.jpg)

<div class="header-label">Artificial Intelligence for Lay People &nbsp;·&nbsp; Week 2</div>

## Deep Learning Revolution &nbsp;·&nbsp; The Luminaries
# Yann LeCun &nbsp;<small>1960–present</small>

*Pioneer of convolutional neural networks; Chief AI Scientist at Meta*

LeCun's 1989 backpropagation work and 1998 LeNet architecture applied convolutional neural networks to handwritten digit recognition — and the USPS used it to read zip codes on billions of envelopes. His work sat largely dormant during the third AI winter until the 2012 ImageNet revolution confirmed what he had been insisting for two decades. One of the three winners of the 2018 Turing Award (with Hinton and Bengio), LeCun is now the most vocal critic of large language models, arguing that they are fundamentally limited architectures.

<div class="callout"><strong>★</strong> LeCun argues on social media with his co-Turing laureate Hinton about whether LLMs can ever achieve real intelligence. Both are probably right about some things.</div>


---

<!-- _class: content technical -->

![bg right:30%](https://upload.wikimedia.org/wikipedia/commons/thumb/3/30/Geoffrey_E._Hinton%2C_2024_Nobel_Prize_Laureate_in_Physics_%28cropped1%29.jpg/500px-Geoffrey_E._Hinton%2C_2024_Nobel_Prize_Laureate_in_Physics_%28cropped1%29.jpg)

<div class="header-label">Artificial Intelligence for Lay People &nbsp;·&nbsp; Week 2</div>

## Deep Learning Revolution &nbsp;·&nbsp; The Luminaries
# Geoffrey Hinton &nbsp;<small>1947–present</small>

*"Godfather of Deep Learning" — 2024 Nobel Prize in Physics*

Hinton co-developed backpropagation (1986), Boltzmann machines, and dropout regularization — then co-authored the 2012 AlexNet paper with his students Sutskever and Krizhevsky, which won the ImageNet competition by an astonishing margin and ignited the modern deep learning era. He worked at Google for a decade. In 2023, at age 75, he resigned from Google specifically so he could speak freely about AI risks — which he now considers very serious. He was awarded the 2024 Nobel Prize in Physics, shared with John Hopfield.

<div class="callout"><strong>★</strong> Hinton refused to fly for decades due to a bad back — he conducted research meetings via video link from Canada while at Google's Toronto office.</div>


---

<!-- _class: content technical -->

![bg right:30%](https://upload.wikimedia.org/wikipedia/commons/thumb/1/11/ICLR_2025_-_Yoshua_Bengio_02.jpg/500px-ICLR_2025_-_Yoshua_Bengio_02.jpg)

<div class="header-label">Artificial Intelligence for Lay People &nbsp;·&nbsp; Week 2</div>

## Deep Learning Revolution &nbsp;·&nbsp; The Luminaries
# Yoshua Bengio &nbsp;<small>1964–present</small>

*Pioneer of deep learning and neural language models*

Bengio's 2003 paper "A Neural Probabilistic Language Model" introduced the idea of learning word embeddings — distributed representations of words as vectors in high-dimensional space. This was the conceptual ancestor of every transformer embedding that followed. He has been one of the most prolific researchers in deep learning and is the third Turing Award laureate alongside Hinton and LeCun. More recently, Bengio has become one of the most prominent voices in AI safety and existential risk.

<div class="callout"><strong>★</strong> Bengio's paper is very technical.  I don't really understand it.</div>


---

<!-- _class: content technical -->

![bg right:30%](https://upload.wikimedia.org/wikipedia/commons/thumb/c/c7/Fei-Fei_Li_at_AI_for_Good_2017.jpg/500px-Fei-Fei_Li_at_AI_for_Good_2017.jpg)

<div class="header-label">Artificial Intelligence for Lay People &nbsp;·&nbsp; Week 2</div>

## Deep Learning Revolution &nbsp;·&nbsp; The Luminaries
# Fei-Fei Li &nbsp;<small>1976–present</small>

*Creator of ImageNet; catalyst of the deep learning revolution*

In 2007, Li launched the ImageNet project: 14 million hand-labeled images across 22,000 categories, crowdsourced via Amazon Mechanical Turk. It was an enormous, unglamorous data-curation project — not a theoretical breakthrough. But without it, there would have been nothing to benchmark deep learning against. The 2012 ImageNet competition, won by Hinton's AlexNet team, dropped the error rate by nearly 11 percentage points in a single year. That competition result was the "big bang" of modern AI. Li has since become a leading voice on human-centered AI and AI ethics.

<div class="callout"><strong>★</strong> Li immigrated from China at 16, worked as a babysitter and waitress to help support her family through college — then built the dataset that changed the world.</div>


---

<!-- _class: content technical -->

![bg right:30%](https://upload.wikimedia.org/wikipedia/commons/d/d4/Ilya_Sutskever_and_Sam_Altman_in_TAU_%28cropped%29.jpg)

<div class="header-label">Artificial Intelligence for Lay People &nbsp;·&nbsp; Week 2</div>

## The LLM Era &nbsp;·&nbsp; The Luminaries
# Ilya Sutskever &nbsp;<small>1986–present</small>

*Co-founder of OpenAI; co-author of AlexNet and GPT*

Sutskever studied under Hinton at Toronto, co-authored the AlexNet paper, and co-founded OpenAI in 2015 where he served as Chief Scientist. He drove much of the research behind the GPT series. In 2023, he was briefly part of the board that voted to remove Sam Altman — then reversed course. In 2024 he left to found Safe Superintelligence (SSI), a company focused exclusively on building safe AGI with no products or revenue pressure. His trajectory — from deep learning pioneer to safety maximalist — mirrors a broader shift in the field.

<div class="callout"><strong>★</strong> Sutskever has said he believes superintelligent AI is the most important and most dangerous technology ever developed. He is building it anyway -- with appropriate care, he claims.</div>


---

<!-- _class: content technical -->

![bg right:30%](https://upload.wikimedia.org/wikipedia/commons/c/c0/Andrej_Karpathy%2C_OpenAI.png)

<div class="header-label">Artificial Intelligence for Lay People &nbsp;·&nbsp; Week 2</div>

## The LLM Era &nbsp;·&nbsp; The Luminaries
# Andrej Karpathy &nbsp;<small>1985–present</small>

*Educator, researcher, and democratizer of deep learning*

Karpathy's contribution is unusual in this list: he did not make a single landmark theoretical breakthrough, but he may have done more than anyone to spread deep learning understanding. His Stanford CS231n course, his blog posts, and his YouTube lectures (including a 3-hour walkthrough of GPT-2 from scratch) have trained a generation of practitioners. He directed AI at Tesla for autonomous driving and was a founding member of OpenAI. His nanoGPT project — a minimal GPT implementation in ~100 lines of Python — is a gold standard teaching tool.

<div class="callout"><strong>★</strong> Karpathy's YouTube lecture "Let's build GPT from scratch" has over 4 million views. It is genuinely one of the best explanations of how LLMs work.</div>


---

<!-- _class: content technical -->

<div class="header-label">Artificial Intelligence for Lay People &nbsp;·&nbsp; Week 2</div>

## The LLM Era &nbsp;·&nbsp; The Luminaries
# Ashish Vaswani et al. &nbsp;<small>Paper published 2017</small>

*Authors of "Attention Is All You Need" — the transformer paper*

In 2017, a team of eight researchers at Google Brain and Google Research published "Attention Is All You Need," introducing the Transformer architecture. The key innovation was the self-attention mechanism, which allows every token in a sequence to attend to every other token simultaneously — replacing the sequential processing of RNNs and LSTMs. Every major AI system today — GPT, Claude, Gemini, BERT, DALL-E, Stable Diffusion — is built on this architecture. It may be the most consequential computer science paper of the 21st century so far.

<div class="callout"><strong>★</strong> The paper's title is itself a manifesto. Attention mechanisms existed before — the claim was that attention was sufficient on its own, without recurrence. They were right. I can't really understand this, but it is very important.</div>

