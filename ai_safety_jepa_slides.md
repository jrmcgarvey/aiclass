## How Are AI Thought Leaders Approaching Safety?

- **Bengio** — Build non-agentic "Scientist AI": no persistent goals, used as a guardrail over agentic AI systems
- **LeCun** — Hard-wire safety constraints into the AI's "cost function," rather than patching behavior after training
- **Hinton** — Warns risk is outpacing solutions; pushes for interpretability research and international regulation
- **Russell** — Redesign AI's objective to stay *uncertain* about human preferences, so it always defers to human correction
- **Industry labs (Anthropic, OpenAI)** — Iterative, empirical approach: red-teaming, interpretability, human feedback at every step

---

## Example: One Possible Future Path — LeCun's JEPA

*This is just one example — other researchers propose very different architectures*

- **LLMs (today's dominant approach):** learn by predicting the next word — trained purely on text
- **JEPA (LeCun's proposal):** learns by predicting abstract representations from images & video — observation, not language
- Goal: ground "common sense" in perception, the way a child learns the physical world before learning words for it

---

## LeCun's Vision (cont.): The Cost Function & Its Risks

- His fuller architecture adds a **cost module** — giving the system something like "wants"
  - **Intrinsic cost** — hardwired, like a built-in sense of pain/pleasure
  - **Trainable critic** — learns to anticipate future cost, enabling forward planning
- **The risk:** persistent, anticipatory goal-pursuit could let self-preserving behavior emerge — even if no one intended it
- This is part of why others (e.g., Bengio) argue for avoiding persistent goals in AI altogether
