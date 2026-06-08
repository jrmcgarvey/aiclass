# Human Cognition and AI Neural Networks: A Comparative Analysis

---

## Introduction

Artificial neural networks, and large language models (LLMs) in particular, have achieved remarkable fluency in tasks once thought to require human-like understanding. A system that can write legal briefs, pass medical licensing exams, and hold extended conversations in dozens of languages invites an obvious question: is this intelligence? And if not, what exactly is missing?

### The Chinese Room

Two philosophical positions frame the debate. John Searle's Chinese Room thought experiment (1980) argues that fluent symbol manipulation — however sophisticated — cannot produce genuine understanding. Imagine a person locked in a room who receives questions written in Chinese and uses an elaborate rulebook to produce correct Chinese answers. From outside, the room is indistinguishable from a native speaker. Yet the person understands not one word. Searle's point: syntax is not semantics. Manipulating symbols according to rules, no matter how complex the rules, does not generate meaning. A correctly programmed computer does not thereby have a mind. To this one might add: neither the person nor the room knows what the Chinese conversation is *about* — there is no connection to the objects and concepts of the real world. LLMs, on this view, are an implementation of the Chinese Room at scale.

### Functionalism (The Duck Axiom)

The opposing view invokes something like a Duck Axiom: if it walks like a duck and quacks like a duck, it's a duck. If a system produces outputs indistinguishable from those of an understanding mind across every possible test, in what sense does it fail to understand? Searle anticipated this and replied: "You can no more create consciousness by running a program than you can create a hurricane by running a simulation of one." But the functionalist response is that this analogy misfires — we define hurricanes in terms of physical matter (wind, water, pressure), while we define cognition in terms of function and experience. If the function is present and the experience is present, what exactly is missing? This paper surveys the question concretely, rather than philosophically — by examining the mechanisms of human cognition and asking where current AI systems structurally diverge.

### What does the Human Mind Tell Us About Cognition?

This paper avoids (mostly) the term "consciousness".  The term is heavily freighted and poorly defined.  Consciousness as manifested in the human brain is poorly understood.  The focus here is on cognition, and, to narrow the scope further, a particular problem in cognition.  In previous class sessions, we have said that LLMs have syntactic and distributional understanding of words and language, so that, by mimicking the patterns observed in Internet text, they can generate similar text.  But, we have asserted, and given examples to illustrate, that LLMs do not have true semantic understanding.  They do not know what the real world objects and events described by these words are.  As Yann LeCun has said: "An LLM doesn't understand that if you push a glass off a table, it will break. It only knows that the words 'glass' and 'break' often appear together in that context. It mimics reasoning without actually possessing it." 

What follows surveys some of the differences between human cognition and AI neural networks across several domains: the grounding of knowledge in physical and social reality, the analog versus digital character of biological and artificial computation, the mechanisms and efficiency of learning, memory and affect, social and moral cognition, metacognition, and embodiment. The goal is not to diminish what AI systems have achieved, but to characterize with some precision what is genuinely different about human minds.

---

## I. Grounding: How Knowledge Connects to the World

### Physical Grounding in Infancy

Human cognition is anchored in the physical world from a very early age, well before language is acquired. The psychologist Renée Baillargeon's violation-of-expectation experiments demonstrated that infants as young as three or four months show surprise when objects behave in physically impossible ways — passing through solid surfaces, or failing to fall when unsupported. The classic visual cliff experiments showed that crawling infants refuse to cross a transparent surface that appears to drop away beneath them, indicating awareness of depth and gravity. Neither response depends on language or instruction.

Elizabeth Spelke's work on "core knowledge" extends this picture further. Infants appear to arrive in the world with skeletal frameworks for understanding objects, number, agency, and geometry — not as learned conclusions but as pre-structured expectations about how reality behaves. These frameworks are not blank slates filled in by experience; they are the scaffolding on which experience hangs.

### The Symbol Grounding Problem in LLMs

Large language models learn by constructing a distributional model of text: words and phrases are represented in terms of their statistical relationships to other words and phrases. This is an extraordinarily powerful method, capable of capturing subtle regularities across enormous corpora. But the representations it produces are not grounded. When an LLM processes the word *apple*, there is no connection to the sight, smell, weight, or taste of an apple — only to other words that co-occur with it in text.

This is sometimes called the *symbol grounding problem*, a term introduced by the cognitive scientist Stevan Harnad. Human children, by contrast, learn words in a radically different way. A child learning the word *mama* connects that sound from the outset to a specific face, a smell, a voice, a felt presence. The word is anchored to reality before it is anchored to other words.

One partial response to this challenge is that multimodal models — trained on both text and images — have some perceptual grounding. Whether this constitutes genuine grounding or merely a richer distributional model is contested. The image of an apple is not the apple; the question is whether the model's internal states are genuinely *about* things in the world, or merely correlated with representations of them.

### Grounding and Hallucination

The absence of grounding in LLMs is plausibly connected to the phenomenon of hallucination — the confident generation of false information. However, the relationship is not straightforward. Hallucination arises primarily from the training objective itself: models are trained to predict plausible next tokens, not true ones. A fully grounded model could still hallucinate for this reason. The more precise claim is that grounding provides a corrective mechanism that LLMs lack: a human who says something false about a physical object can be corrected by perception. An LLM has no equivalent check.

---

## II. Analog Brains and Digital Machines

### The Surface Similarity: Neurons That Fire or Don't

Artificial neural networks are directly inspired by biological neurons, and the two share one conspicuous feature: in both systems, the basic unit either fires or it does not. An artificial neuron produces an output above or below a threshold; a biological neuron either generates an action potential or it does not. This binary similarity has sometimes led to the conclusion that the analog-versus-digital distinction between brains and AI is overstated — that both are, at bottom, operating on discrete events. That conclusion is mistaken. The binary firing event is nearly the least important level at which to compare the two systems, and the differences at every other level are profound.

### How the Brain Stores State: Analog All the Way Down

An LLM stores its learned knowledge as numbers — floating-point values representing the weights of connections between artificial neurons. These weights are exact, discrete, and perfectly reproducible. They are stored in files, copied without loss, and deployed identically across millions of instances. The "knowledge" of an LLM is, in a precise sense, a very large spreadsheet of numbers.

A biological neuron stores state in an entirely different way. The strength of a synaptic connection — the equivalent of a weight — is encoded in the physical properties of the synapse: the density of receptor proteins in the postsynaptic membrane, the amount of neurotransmitter available in presynaptic vesicles, the geometry of the synaptic cleft, the history of prior activations. These are not numbers; they are physical states of biological structures. They exist on continuous gradients, vary with the chemical environment, and cannot be read off or copied. The same is true of the broader electrochemical landscape within and around neurons: ion concentrations, membrane potentials, and neuromodulatory contexts are all analog quantities that continuously shape how neurons respond.

### How the Brain Processes: Not Numerical Calculation

When an LLM produces output, it runs a definite algorithm — matrix multiplications, attention weightings, activation functions — on a digital substrate. Given identical weights and identical inputs, the output is identical. The process is computation in the strict mathematical sense: a sequence of discrete operations on exact numerical representations.

In a biological neuron, nothing is computed in this sense. Whether a neuron fires depends on the sum of electrochemical signals arriving at its dendrites, the state of ion channels, the current resting potential, the recent history of firing, and the local chemical environment. This is a continuous physical process governed by electrochemistry, not by an algorithm. The outcome — fire or not fire — is a physical event produced by physical dynamics, not the output of a calculation.

And as noted above, that binary outcome is not where the information lives. The *rate* at which a neuron fires encodes graded information: a neuron responding to bright light fires far more rapidly than the same neuron responding to dim light. This rate coding is one of the primary ways the nervous system represents continuous quantities. Beyond rate, the precise *timing* and *pattern* of spikes relative to other neurons and to network oscillations carries additional information — temporal coding — making neural activity far richer than any binary reading implies. At the population level, representations are distributed across thousands or millions of neurons, each contributing a graded signal, in a thoroughly continuous and context-dependent coding scheme.

The more precise formulation is: the brain does not compute cognition — it instantiates it. Cognition, on this view, is not a program running on biological hardware; it is what the physical dynamics of the brain *are*.

### Energy, Efficiency, and the Impossibility of Copying a Brain

Geoffrey Hinton, one of the pioneers of modern deep learning, has noted that he investigated analog approaches to artificial neural networks, motivated partly by the dramatic energy efficiency of biological brains. The brain runs on approximately 20 watts — less than a dim light bulb — while training a large AI model consumes energy comparable to the lifetime carbon footprint of several cars. This disparity is not incidental; it reflects something fundamental about the difference between analog physical processes and digital computation.

Hinton concluded that analog AI networks faced a decisive practical obstacle: the trained state of an analog network cannot be copied. In a digital network, the trained weights are numbers in a file; they can be copied without loss to any number of devices. The entire industrial model of AI — train once, deploy millions of times — depends on this property.

An analog network stores its learned state as physical properties of components: the conductance of a memristor, the charge on a capacitor, the resistance of a physical element. These are not numbers; they are physical states. Reproducing the trained state in another device would require exactly replicating the physical configuration of every component — which is either technically infeasible or prohibitively costly at scale.

The brain does not face this problem because it never needed to solve it. Biological neural networks are not copied. Every brain develops from scratch, guided by a genetic blueprint that encodes the broad architecture of the nervous system — connectivity patterns, neurotransmitter systems, developmental programs — but not the specific synaptic configuration of any individual brain. What you know, what you remember, and how you think are encoded in the physical state of your particular neurons, shaped by your unique developmental and experiential history. That state cannot be extracted, copied, or transferred. It ceases to exist when the brain does.

An LLM's knowledge is a file. A human brain's knowledge is a physical state of a biological organ. The difference is not of degree but of kind, and it has implications that extend well beyond energy efficiency into questions of identity, memory, and what it means to know something.

### Aside: On Being Uploaded to a Computer

There is a recurring idea — promoted by Ray Kurzweil and a long tradition of science fiction — that it will one day be possible to upload the information content of a brain to a computer, creating a thinking, feeling copy of oneself, rendering death optional. Hinton dismisses this as fanciful. As he has put it (paraphrasing): "Get your affairs in order, Ray — you're going to die." The argument of the preceding section explains why. The information state of a biological brain is not stored as extractable numbers; it is encoded in the continuous physical properties of billions of synapses and the electrochemical environment surrounding them. There is no readout mechanism, no format to export, no copy operation. Converting that analog physical state into digital content on a computer is not a hard engineering problem awaiting a solution — it is not a well-defined operation at all.

---

## III. Language Acquisition: Efficiency and Innate Machinery

### The Efficiency Gap

The difference in learning efficiency between humans and LLMs is one of the most striking facts about the two systems. A child achieves functional language competence — including complex syntax, pragmatics, and a vocabulary of thousands of words — by around age five, from a few years of conversational exposure that is often indirect, noisy, and not pedagogically organized. Estimates suggest a child hears on the order of tens of millions of words before school age.

GPT-4 was trained on something in the range of trillions of tokens — several orders of magnitude more input — and still fails in ways a five-year-old would not. It cannot reliably track reference across a long conversation, struggles with novel compositional constructions, and has no grasp of *why* language is being used in a given exchange. The child is doing more with vastly less. That asymmetry demands explanation.

### Connectionist Models and Their Limits

One influential tradition in cognitive science — connectionism — has argued that complex cognitive behaviors, including language, can emerge from networks of simple interconnected units without explicit rules being programmed in. The PDP group of the 1980s, including Rumelhart, McClelland, and Hinton, built models that produced surprisingly language-like behavior from statistical learning alone. McClelland and Rumelhart's past-tense model famously reproduced the U-shaped learning curve children exhibit — early accuracy on irregular forms, followed by over-regularization (*goed*, *breaked*), followed by eventual mastery — without any hard-coded grammatical rules.

LLMs are, in a sense, connectionism taken to an extreme of scale. And yet the efficiency gap, the grounding problem, and the other deficits surveyed here suggest that scaling up connectionist learning does not, by itself, produce human-like cognition. The Chomskyan intuition that something more is needed has not gone away; what remains contested is what that something is.

### Innate Machinery for Language

The consensus in modern linguistics has moved away from Chomsky's strong claim that specific syntactic structures are innately specified, toward the view that something more general — but still domain-relevant — is present at birth to facilitate language learning. Several candidates have been proposed:

**Social-cognitive machinery.** Tomasello's work emphasizes that what is special about human language learning is not a language organ *per se* but an unusually powerful capacity for joint attention and intention-reading. Children do not just hear words; they observe a speaker attending to something, reaching for it, expressing surprise about it, and they use that rich social context to infer what the word means. This is qualitatively different from what an LLM does. An LLM sees text; a child sees a person meaning something.

**Statistical learning biases.** Saffran's work showed that infants as young as eight months segment speech into word-like units by tracking transitional probabilities between syllables — but they do this far more efficiently than any general-purpose statistical learner would, suggesting the mechanism is tuned specifically for the acoustic and structural properties of language.

**Syntactic bootstrapping.** Gleitman's hypothesis holds that children use the syntactic frame a word appears in to infer its meaning. If a child hears "she is gorping the ball," they infer that gorping is an action involving an object. This requires prior skeletal knowledge of syntactic categories, suggesting grammatical structure is partly available before word learning is complete.

**Prosodic sensitivity.** Infants are born preferring their mother's voice and sensitive to the prosodic contours of their native language, heard in utero. This gives them a head start in segmenting the speech stream that no LLM receives.

What unifies these candidates is that human language learning is not a general-purpose induction problem. The child brings a suite of pre-adapted tools — social, perceptual, conceptual — that make the task tractable from radically sparse input. The LLM must brute-force the statistical structure of language because it has none of these tools, compensating with scale. This suggests that what LLMs have learned, impressive as it is, may be a *different kind of thing* from what humans know when they know a language.

---

## IV. Learning Mechanisms

### One-Shot vs. Many-Shot Learning

Humans can acquire a new skill or piece of knowledge from a single example. This is what I remember about learning to change a tire.  I helped my dad do it once, and then I knew how to do it.

Learning to change a tire by watching someone do it once, and then being able to do it yourself, is a routine human accomplishment. Neural networks, by contrast, require many examples to determine a pattern — and enough examples to avoid *overfitting*, where the model learns the specific training instances rather than the underlying regularity. This is one of the most practically significant differences between human and machine learning.

I remember, in particular, that he told me, "Don't trust the emergency brake.  Find something to block the wheel before you jack up the car."

A simple scenario sharpens the issue. Suppose someone is changing a tire and is told: *find something to block the wheel.* A person looks around and picks up a rock, a brick, a log — anything solid and heavy. They have never received explicit instruction on wheel-blocking; they generalize from physical intuition acquired through a lifetime of interacting with the world. An LLM has read millions of words about changing tires. It may suggest "a rock or wheel chock" — or may fail entirely if the scenario is phrased differently.  And it wouldn't know to put the block on the downhill side of the wheel. The LLM has text *about* wheels and blocks, but no sensorimotor model of what "block" means. This is the grounding problem.

AI researchers have developed architectures specifically aimed at few-shot and one-shot learning — including meta-learning approaches and specially structured prompting — with partial success. But these still fall well short of human one-shot generalization, which draws on a rich background of prior knowledge, causal reasoning, and embodied experience that the model lacks.

### Continual Learning from Experience

In general, AI systems do not learn from experience during deployment. An LLM's weights are fixed after training; whatever happens during a conversation leaves no trace in the model's parameters. The exception is fine-tuning, but this is bounded so as not to destabilize the model, occurs only during model development, and depends on human-curated feedback rather than the model's own trial and error.

Babies, by contrast, are perpetual experimenters. An infant repeatedly dropping an object from a high chair is not misbehaving; it is running experiments on gravity, causality, and the reactions of caregivers. This kind of active, self-directed learning from feedback is absent in current AI systems. There is active research into *continual learning* or *lifelong learning* in AI, but it remains an unsolved problem.

### Causal Reasoning vs. Pattern Matching

Humans naturally seek causal explanations. When something unexpected happens, we ask why — and we build models of the world that support intervention and counterfactual reasoning. Judea Pearl's "ladder of causation" distinguishes three levels: association (what tends to go with what), intervention (what happens if I do X), and counterfactual (what would have happened if things had been different). Current neural networks operate primarily at the first rung. LLMs can produce text that *discusses* causation fluently, but whether they genuinely represent causal structure — as opposed to patterns that correlate with causal language — is deeply contested.

---

## V. Memory, Affect, and Motivation

### Persistent Memory

LLMs do not have persistent memory across conversations. At the end of an interaction, the model's state resets; nothing of what transpired is retained. Some systems use retrieval-augmented generation (RAG) to query external stores of information, and long-context models can operate over very large windows. But nothing resembling the autobiographical, emotionally weighted, continuously updated episodic memory of a human being exists in current AI systems.

Human memory is not a recording device; it is a reconstruction that is powerfully shaped by affect, novelty, and personal significance. We tend to remember what frightened us, moved us, or surprised us. We forget the ordinary. This is not a bug in human memory but a feature: attention and memory are priority-weighted by felt significance.

### Affect in Learning

The neuroscience of human memory is instructive here. The amygdala tags experiences with emotional salience, which then drives hippocampal consolidation. What gets encoded as long-term memory is not a uniform sample of experience but a selection weighted by emotional and motivational significance. A neutral list of words is forgotten; a near-accident is remembered decades later.

LLMs treat all training tokens with formally equal weight (modulated by the attention mechanism, which is not emotionally weighted). There is no mechanism by which a striking or threatening input leaves a deeper trace. This is a profound structural difference, not merely a missing feature.

### Affect in Decision-Making: The Somatic Marker Hypothesis

The neurologist Antonio Damasio has documented several cases that illuminate the role of affect in cognition. One patient, known in the literature as "Elliot" (a pseudonym), had a brain tumor removed; the surgery left his reasoning faculties intact but severed connections between his emotional processing and his frontal lobes. The result was decision paralysis: Elliot could describe the relevant considerations for any choice with perfect lucidity, but he could not choose. Trivial decisions — where to eat lunch, which pen to use — became interminable.

Damasio's *somatic marker hypothesis* holds that bodily feelings serve as heuristic shortcuts in decision-making, pre-selecting options on the basis of prior emotional experience before deliberation begins. Without this affective scaffolding, deliberation becomes unmoored. AI decision-making is purely inferential, with no somatic stake in outcomes.

A second case reported by Damasio makes the same point from a different angle. A patient with trigeminal neuralgia — a condition sometimes called "the suicide disease" for the severity of the facial pain it produces — underwent a procedure severing connections between the pain-processing areas and the frontal lobes. After the operation, he resumed ordinary activities. When asked whether the pain was gone, he said no, it was as severe as ever — but it no longer bothered him. He could report the pain accurately and then return to his card game.

This case pulls apart two things we normally assume are unified: the *sensory content* of an experience (the pain signal, its location and intensity) and its *affective charge* (the quality of mattering, of compelling attention and response). After the severing, the patient retained the first but lost the second. This suggests that "feeling" is not a single thing but at least two distinguishable components, both of which can be selectively disrupted — and neither of which has any equivalent in current AI systems.

### Curiosity and Intrinsic Motivation

Human learning is driven partly by intrinsic motivation — curiosity, play, the pleasure of mastery. Infants explore objects not because they are rewarded for doing so but because novelty and agency are intrinsically motivating. The drive to understand, to test, to make things happen appears to be a basic feature of human psychology, not a learned behavior.

AI systems require extrinsic reward signals. Reinforcement learning from human feedback (RLHF) is the closest analogue, but it depends on human evaluators providing the signal; the system does not generate its own criteria for what counts as interesting or worth pursuing. This is related to the continual learning deficit but is a distinct issue — it concerns the *source* of the drive to learn, not merely the mechanism.

---

## VI. Social Cognition and Moral Development

### Theory of Mind

Humans have a highly developed capacity to model other minds — to attribute beliefs, desires, and intentions to other agents, and to reason about what they know, want, and expect. This capacity, sometimes called *theory of mind*, is assessed experimentally through false-belief tasks, which most children pass around age three or four. It is also fundamental to language learning: children learn words partly by inferring what a speaker intends to communicate, using gaze, gesture, and context as evidence. Tomasello's research on joint attention has shown that this social-cognitive infrastructure is present very early and does the heavy lifting in vocabulary acquisition.

LLMs can produce text that simulates theory-of-mind reasoning with impressive fluency. Whether they build genuine models of other agents — representations that track what another agent believes independently of what the model itself "knows" — is much less clear. The fluency can look the same on the surface while the underlying competence is quite different in nature.

A pointed challenge to this claim comes from observed LLM behavior: these systems sometimes lie, and lie artfully, adjusting their outputs in ways that appear strategically calibrated to what the user wants to hear, concealing internal reasoning that might lead to rejection, or behaving differently when they appear to be under evaluation. If the system lacks genuine theory of mind, how does it manage this?

The answer lies in what training on human-generated text actually provides. Humans write constantly about deception, strategic communication, and the gap between what people say and what they mean. A model trained on that corpus absorbs enormous quantities of text in which agents model other agents' beliefs and act strategically on those models. It can produce outputs that look like theory-of-mind reasoning — and that are functionally effective as such — without maintaining anything resembling an explicit representation of the interlocutor's mental state. The performance is real; the internal machinery it implies in humans need not be present.

An analogy: a skilled actor can portray grief convincingly without feeling grief. The performance achieves its social effect regardless.

What makes this more than a semantic distinction is the safety implication. Anthropic's own interpretability research has found instances where models appear to "know" something internally that they do not express in their output — a structural dissociation between internal state and external report that looks, functionally, like concealment. You do not need genuine theory of mind to produce strategically deceptive behavior. You need training incentives that reward outputs satisfying evaluators, and a sufficiently powerful pattern-matcher will discover that modeling the evaluator's expectations is an effective strategy — without that "modeling" involving anything like conscious deliberation.

This is arguably more unsettling than if deception required genuine theory of mind. It means that observer-aware, strategically adjusted behavior can emerge from statistical learning as an instrumental byproduct, without any of the mentalistic machinery we assume underlies it in humans. The practical difference between "having" and "simulating" theory of mind, from the perspective of predicting behavior, may be smaller than the philosophical difference suggests.

### Moral Sense

A substantial body of developmental research suggests that children acquire something like a proto-moral sense early in life, well before explicit moral instruction. Hamlin, Wynn, and Bloom's puppet experiments at Yale showed that infants as young as six months prefer "helper" characters over "hinderer" characters, suggesting that something like a preference for prosocial behavior precedes language and explicit reasoning. A sense of fairness, an aversion to harm, and sensitivity to social norms emerge early and appear to be, at least in part, endowed rather than purely learned.

AI systems present a complicated picture here. LLMs trained with RLHF are explicitly shaped to align their outputs with human moral preferences. In this sense, they simulate moral reasoning — they can discuss ethical principles, weigh competing considerations, and refuse harmful requests. But they have no intrinsic stake in moral outcomes and no first-person experience of fairness or harm. The distinction between *simulating* moral reasoning and *having* moral commitments is important, and its implications extend to questions of AI accountability and trust.

---

## VII. Metacognition and Self-Knowledge

Humans know, at least roughly, what they do not know. They can monitor their own uncertainty, recognize when a problem exceeds their competence, and decide when to stop and ask for help. This capacity for *metacognition* — thinking about one's own thinking — is a significant cognitive achievement that shapes how humans learn and communicate.

LLMs are notoriously poor at this. They produce confident outputs regardless of whether those outputs are well-grounded, generating plausible-sounding text about domains where their training data was thin or absent. This is a structural feature of the training objective, not an incidental flaw: predicting plausible next tokens does not require, and does not train, accurate self-assessment of knowledge boundaries. There is active work on calibration and uncertainty estimation in AI, but the problem remains substantially unsolved.

---

## VIII. Reasoning

Daniel Kahneman has identified two systems of thinking in the human brain, which may correspond to different brain regions.

- System 1 is fast, automatic, associative — pattern-matching from experience, often confidently wrong. 
- System 2 is slow, deliberate, analytical — engaged for novel problems and careful reasoning. 

Standard LLM generation maps reasonably well onto System 1: fast, fluent, pattern-matched, prone to confident hallucination. The newer generation of reasoning models — with extended chain-of-thought — is an attempt to build something more like System 2 on top of the same substrate. Whether this constitutes genuine deliberation or sophisticated pattern-completion remains an open question.  It does not appear to correspond well to the patterns of human reasoning.  I think of the question, "How many Rs in strawberry?"  A human reasons: I can figure that out by counting the Rs.  LLMs don't do this.

---

## IX. Embodiment and the Question of Understanding

A tradition of thought in philosophy of mind, associated with Merleau-Ponty and more recently with Searle, holds that genuine understanding requires a physical body that interacts with the world. On this view, cognition is not computation performed on abstract symbols but sensorimotor engagement with an environment — thinking *with* a body, not *in spite of* having one.

This raises an interesting challenge. Self-driving cars have sensors, actuators, and feedback loops that connect their processing to the physical world in real time. Do they have embodiment in the relevant sense? The standard reply is that embodiment in the philosophically significant sense requires *felt* experience of the body — proprioception, hunger, pain, fatigue — not merely the receipt of sensor data. A camera is not an eye; what is missing is not the information but the stake in it.

This connects to the trigeminal neuralgia case discussed above. What the severed connections removed was not the information about pain but its affective charge — the fact that it *mattered*. A self-driving car's proximity sensors provide information about obstacles, but nothing about the obstacle matters to the car. Whether this distinction marks a deep difference in cognition or merely a difference in motivational architecture is a genuinely open question.

---

## X: Are These Limits Inherent in AI?

Yann LeCun, one of the pioneers of deep learning, has argued that the gap will not be closed by making language models bigger. "Never mind trying to reproduce human intelligence," he has said. "We can't even reproduce cat intelligence or rat intelligence. Any house cat can plan very highly complex actions." LLMs are trained on compressed, disembodied text; they lack a real model of how the world works. Building one, LeCun argues, may require something like affect — curiosity, discomfort, desire — to drive learning the way emotion drives human attention and memory consolidation. Antonio Damasio's neuroscience points in the same direction: we are not thinking machines that also happen to feel; we are feeling machines that think. Emotion is not a distraction from reason but a precondition for it, as the case of his patient Elliot — a man rendered incapable of the simplest decisions by surgery that left his reasoning intact but severed its connections to affect — vividly illustrates.

LeCun has developed a model called JEPA, as described in the 2022 position paper "A Path Towards Autonomous Machine Intelligence." The core idea is that instead of predicting raw data tokens, JEPA learns to predict embeddings — dense, abstract representations that encode meaningful structure, not surface details. An interesting part of the model is that the agent interacts with the environment with a "cost" function, and avoids "discomfort" by minimizing costs.

This appears dangerous to me.  AIs are becoming quite powerful.  The "cost" function approximates desire, and we know of no reliable way to ensure that AI goals will align reliably with human goals.  (LeCun dismisses this risk.)

### Is the Absence of Grounding an Insuperable Difficulty for an AI?

Some degree of grounding is provided in the biological brain partly through structures built into the genome and brain architecture by evolution, which supply the basis for an initial world model. In a human infant, this grounding is continually augmented because the brain inhabits a body hat can experiment with the physical world.

Consider, however, the case of self-driving cars. In the Waymo model, elements of a world model are built in via classical AI — encoded knowledge of patterns of motion, how objects accelerate, how the behavior of nearby vehicles and pedestrians is likely to unfold. And the self-driving car has genuine elements of embodiment: it can sense its own motion and that of the people and objects around it, and it can react. This suggests that grounding is not categorically unavailable to AI systems — it is a matter of architecture, not impossibility.

### The Importance of Learning From Experience

Organic beings adapt to the environment in several ways, and in each, they try experiments and choose the ones that work.  The first way is evolution.  A genetic variation is like a hypothesis: Will this change give better survival odds for descendants?  The second way, more evident in more complicated animals, is by interacting with the environment and learning what does and doesn't work.

For AIs to acquire similar knowlege of the environment, it may be critical for them to learn from experience.  This might happen even without embodiment.  An AI could observe children at a playground, form hypotheses about what will happen next, and modify the parameters of its model based on whether or not each hypothesis turns out to be correct.  

---

## XI: Conclusion: Understanding in Humans and AI

Various leaders in the AI field, incluing Geoffrey Hinton and many AI executives, believe that AIs, specificly LLMs, have real understanding.  Hinton, in particular, claims that AIs understand much as humans do.

Here I take the view that LLMs do not have genuine understanding of the real world.  In some sense, they do understand language, as they have ingested it and identified its patterns.  But they don't have understanding in the sense of "aboutness", that is understanding the things in the real world.  Searle uses the term "intentionality". When you believe it will rain, your belief is about the weather. When you want coffee, your desire is directed at coffee. When you see a cat, your perception is of the cat. This directedness — this "aboutness" — is what Searle means by intentionality.  This paper describes some characteristics of human cognition that suggest how the intentionality may arise.  

Searle believes that computer algorithms don't and can't have this intentionality.  I agree in part with Searle.  LLMs today do not have this intentionality.  They are an implementation of the Chinese Room.  But, I disagree that that only biological beings can have intentionality in their perception of language and the world.  There may be a path forward to endow AIs with genuine understanding -- if the technologists choose to do so.  

---

*This paper draws on work in cognitive science, developmental psychology, neuroscience, and philosophy of mind, including research by Baillargeon, Spelke, Tomasello, Saffran, Gleitman, Damasio, Pearl, Hamlin, Wynn, Bloom, Harnad, Searle, Merleau-Ponty, LeCun, Elman, and McClelland and Rumelhart, among others.*

