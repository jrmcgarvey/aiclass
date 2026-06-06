# Do LLMs Understand? Language, Mathematics, and the Limits of Pattern
### Discussion Group Presentation

---

## 1. Setting the Stage

Last session we looked at how neural networks and LLMs actually work — the transformer architecture, attention mechanisms, training on vast corpora of text. Today I want to push on a harder question that follows from that: *what does it mean for a system like that to "understand" anything?*

My starting position: LLMs have what we might call **distributional** understanding of language. They have learned, with extraordinary sophistication, which words and phrases tend to appear near which other words and phrases. What they do not have — or so I will argue — is any genuine connection to the physical world those words are supposed to refer to.

But I want to hold this lightly. It is a live philosophical debate, and some very smart people disagree.

---

## 2. Two Camps

### The "They Do Understand" Camp

**Geoffrey Hinton** (Turing Award, "Godfather of Deep Learning") has pushed back hard on the dismissal of LLMs as mere parrots. In a 2023 exchange with Gary Marcus, he wrote:

> "ChatGPT seems to me to be like an idiot savant whose understanding is different from mine but not entirely absent."

His point is that we should not treat understanding as binary — something humans have in full and machines have none of. He argues that LLMs create high-dimensional representations that capture genuine semantic relationships, not mere surface-level word co-occurrences.

**Dario Amodei** (CEO, Anthropic) has been more cautious but in a direction that leaves the door open. In February 2026 he said publicly:

> "We don't know if the models are conscious. We are not even sure that we know what it would mean for a model to be conscious or whether a model can be conscious. But we're open to the idea that it could be."

He has described Anthropic's interpretability work as looking for signs of internal states — finding, for example, neural activations associated with something like anxiety.

---

### The "They Don't Understand" Camp

**Yann LeCun** (also a Turing Award winner, recently left Meta to found AMI) has been the most forceful skeptic from within the AI research community:

> "LLMs perform well at the language level, but they don't understand the world. They lack common sense and causal relationships and are just a stack of a large number of statistical correlations."

He gave a concrete example:

> "An LLM doesn't understand that if you push a glass off a table, it will break. It only knows that the words 'glass' and 'break' often appear together in that context."

He lists four capabilities he sees as essential to real intelligence — understanding the physical world, persistent memory, genuine reasoning, and planning — and argues that LLMs can do none of these, or only in a "very primitive way."

**John Searle** (philosopher, UC Berkeley) made the foundational philosophical argument with his famous Chinese Room thought experiment (1980). A person in a room follows rules for manipulating Chinese symbols perfectly, passing the Turing Test — but understands nothing. His conclusion:

> "If the man in the room does not understand Chinese on the basis of implementing the appropriate program for understanding Chinese, then neither does any other digital computer solely on that basis, because no computer, qua computer, has anything the man does not have."

His key distinction: computers have *syntax* but not *semantics*. They manipulate symbols according to formal rules, but the symbols have no intrinsic meaning — no *intentionality*, no "aboutness." Meaning requires that a mental state be genuinely about something in the world, which Searle argues requires biological, embodied processes, not symbol manipulation.

**Bender, Gebru, McMillan-Major, and Mitchell** gave us the phrase "stochastic parrot" in their 2021 paper "On the Dangers of Stochastic Parrots." Their definition is precise and worth quoting in full:

> "Contrary to how it may seem when we observe its output, an LM is a system for haphazardly stitching together sequences of linguistic forms it has observed in its vast training data, according to probabilistic information about how they combine, but without any reference to meaning: a stochastic parrot."

Note the phrase "without any reference to meaning." This is Searle's point restated in technical language. The system operates purely at the level of form — the distribution of linguistic tokens — with no connection to what those forms refer to.

A commenter in the ongoing debate put the same point bluntly:

> "Simply put, LLMs represent words by their contexts. They have no referents for the words. That is not understanding."

**Gary Marcus** (cognitive scientist, NYU, founder of Robust.AI) is perhaps the most persistent and publicly visible critic of LLM claims to understanding. He has been in direct debate with both Hinton and LeCun — and is unusual among skeptics in coming from cognitive science rather than philosophy or AI engineering, which gives his objections a different flavor.

Marcus's core argument is that LLMs are impressive pattern matchers but remain fundamentally unreliable because they lack what he calls *genuine comprehension* — a stable, grounded model of what words refer to in the world. He points to hallucination not as a bug to be fixed but as a symptom of a deeper architectural limitation:

> "I do believe that LLMs do not really understand what they are saying."

He has also pushed back specifically on Hinton's dismissal of critics as confused, arguing that the errors LLMs make are qualitatively different from human errors — not occasional lapses but a systematic pattern of confabulation that reveals the absence of any underlying model of reality:

> "Humans rarely make things up wholesale. LLMs do."

Marcus's position is not that LLMs are useless — he acknowledges their practical value — but that the leap from impressive linguistic performance to genuine understanding is one that has not been made, and that the field does itself a disservice by conflating the two. He has also been a consistent voice warning that overstating LLM capabilities creates real risks: people deploying systems they don't understand, in contexts where hallucination has serious consequences.

He is worth noting as a **bridge figure** in this debate: someone who takes both the philosophical objections (Searle's Chinese Room, the stochastic parrot framing) and the empirical track record of LLM failures seriously, and tries to synthesize them into a practical research agenda.

---

## 3. A Philosophical Backstory (Briefly)

This debate has deep roots:

- **Lady Lovelace (1843)** said of Babbage's Analytical Engine: *"The Analytical Engine has no pretensions whatever to originate anything. It can do whatever we know how to order it to perform... but it has no power of anticipating any analytical relations or truths."*

- **Turing (1950)** named this "Lady Lovelace's Objection" and disputed it — arguing that we can program a machine to surprise us.

- **Dreyfus (1972)** in *What Computers Can't Do* made the case that human intelligence is rooted in embodied experience and tacit "background" knowledge that cannot be captured symbolically. He called AI research of his time an exercise in "tree climbing with one's eyes on the moon."

The stochastic parrot argument is the latest chapter in a long story.

---

## 4. The Puzzle: If They Don't Understand, Why Are They So Good?

Here is what makes this genuinely interesting rather than a settled question: LLMs produce remarkable results, results that in some domains exceed what any individual human can do.

**The recent mathematics results are striking.** In May 2026, OpenAI announced that an internal reasoning model had disproved Erdős' planar unit distance conjecture — an 80-year-old geometry problem that human mathematicians had worked on without success. Mathematicians described the AI's method as "clever" and "elegant," and one said it would qualify as a "Proof from The Book" — the concept Erdős used to describe proofs so perfect they might have been written by God.

A separate effort (the "First Proof" project) used LLMs to resolve 9 of 353 open Erdős problems, at a cost of a few hundred dollars per problem — a remarkable ratio of result to resource.

**How to explain this without granting full understanding?**

Here is the proposal I want to float for discussion:

---

## 5. Mathematics Is Language

The key insight is this: **mathematics is a form of language.**

It is a language with unusually strict rules of inference and an unusually tight relationship to physical reality — hence Wigner's famous puzzle about "the unreasonable effectiveness of mathematics." But it is, at bottom, a formal symbolic system. Proofs are sequences of valid transformations from premises to conclusions. The symbols — ∃, ∀, →, ∈ — have no more intrinsic connection to the physical world than the words "glass" or "break" do. Their meaning is defined by the rules of the formal system.

If this is right, then LLMs can emulate mathematical reasoning for the same reason they can emulate any other linguistic production: they have learned the patterns of valid mathematical inference from the vast corpus of mathematical text on the internet — textbooks, papers, proofs, exercises, solutions.

**This explains several things:**

- Why LLMs can produce impressive mathematical results (mathematics is linguistic pattern at a very deep level)
- Why LLMs still hallucinate proofs and need validation (they are pattern-matching, not actually checking logical validity)
- Why Lean — a formal proof verification language built on symbolic logic, not neural networks — is essential as a check. In the Erdős work, LLMs generated candidate proofs; Lean verified them. The intelligence was distributed: LLMs for generation, symbolic systems for verification.
- Why fine-tuning on mathematical corpora and stepwise "chain of thought" reasoning improve performance (both are ways of more closely aligning the model with the specific patterns of valid mathematical inference)

---

## 6. The Broader Claim

Mathematics is a special case of a more general observation: **a great deal of what we think of as human intelligence is, at bottom, linguistic production.**

Consider: scientific papers, legal briefs, philosophical arguments, medical diagnoses expressed in reports, software code, business strategy documents, poems, novels. All of these are language. An entity that has mastered the deep patterns of human language — not just surface grammar but the patterns of valid reasoning, evidence marshaling, narrative structure, rhetorical convention — can produce outputs that are indistinguishable from, and sometimes superior to, what an individual human expert produces.

**This does not mean LLMs understand everything, or even most things.**

LeCun's glass-breaking example is a real limitation. LLMs continue to make statements about the physical world that are nonsense, because the physical world is not reducible to linguistic patterns. They hallucinate facts. They are brittle in novel physical situations. They have no persistent memory of the world as it changes. For tasks that require genuine grounding in physical reality — robotics, scientific experiment design, causal reasoning about novel physical situations — the distributional semantics of text is insufficient.

But for tasks that are themselves linguistic in nature, LLMs may be not just useful but genuinely transformative.

---

## 7. Questions for Discussion

1. Is the claim that "mathematics is language" convincing? Does it matter that mathematicians report experiencing genuine *insight* — a felt sense of understanding — when they grasp a proof?

2. Hinton argues that the distinction between "mere pattern matching" and "real understanding" is not as clear as critics assume — that human understanding may itself be a form of very sophisticated pattern recognition. How do we respond?

3. If LLMs can produce valid mathematical proofs (verified by Lean), does it matter whether they "understand" them in a philosophically robust sense?

4. What kinds of tasks do you think are *not* reducible to linguistic pattern? Where do you expect LLMs to remain permanently limited?

5. Searle distinguishes intrinsic from derived intentionality — meaning that originates in a mind versus meaning we project onto artifacts. Is this distinction ultimately defensible?

6. Gary Marcus argues that LLM hallucination is not a fixable bug but a symptom of a deeper architectural absence — no grounded model of reality. Does the mathematics example (where Lean catches the hallucinations) suggest a workaround, or does it actually confirm his point?

---

## References and Sources

- Ada Lovelace, Notes on Menabrea's "Sketch of the Analytical Engine" (1843)
- Alan Turing, "Computing Machinery and Intelligence," *Mind* (1950)
- Hubert Dreyfus, *What Computers Can't Do* (1972; revised 1992)
- John Searle, "Minds, Brains, and Programs," *Behavioral and Brain Sciences* (1980)
- Bender, Gebru, McMillan-Major, Mitchell, "On the Dangers of Stochastic Parrots," FAccT (2021)
- Gary Marcus, "Deconstructing Geoffrey Hinton's Weakest Argument," *Marcus on AI* Substack (2024)
- Hinton, public exchanges on the Connectionists mailing list (2023–2024)
- LeCun, public lecture "Do LLMs Understand?" (November 2025)
- Amodei, interview on *Interesting Times* podcast, NYT (February 2026)
- "Advancing Mathematics Research with AI-Driven Formal Proof Search," arXiv:2605.22763 (May 2026)
- "AI just solved an 80-year-old Erdős problem," *Scientific American* (May 2026)
