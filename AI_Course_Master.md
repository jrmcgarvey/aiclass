# AI Course Master Reference
## "Understanding Artificial Intelligence" — Lay People Course

Paste this document at the start of any new Claude session to ensure consistent
slide style, course structure, and editorial voice across all weeks.

---

## COURSE STRUCTURE

**Format:** Multi-week session class for lay people (non-technical general audience)
**Weekly topics:**
- Week 1: Course Overview & Suggested Reading ✅ COMPLETE
- Week 2: A Brief History of Artificial Intelligence
- Week 3: Current Capabilities
- Week 4: Current Limitations
- Week 5: AI vs. Human Cognition
- Week 6: Effects on Society (positive and negative)
- Week 7: Likely Futures

*(Adjust week count/order as needed — this is the working plan.)*

---

## SLIDE STYLE GUIDE

### Tool & Setup
- **Library:** PptxGenJS (Node.js)
- **Module path:** `/home/claude/.npm-global/lib/node_modules/pptxgenjs`
- **Layout:** `LAYOUT_16x9` (10" × 5.625")
- **Font:** Calibri throughout (header and body)

### Color Palette (NEVER use # prefix on hex colors)
```
DARK_BG   = "1A1F2E"   // deep navy — title slides, section dividers, headers, footers
MID_BG    = "232A3B"   // medium navy — content slide backgrounds
CARD_BG   = "2A3247"   // card/box background
ACCENT1   = "4EC9C0"   // teal — primary accent, AI Progress & Policy category
ACCENT2   = "F0A500"   // amber/gold — secondary accent, Alignment & Safety category
WHITE     = "FFFFFF"
OFF_WHITE = "E8EDF5"   // body text on dark backgrounds
MUTED     = "8D96A8"   // captions, footers, secondary text
```

**Category accent colors (for section dividers and book cards):**
```
AI Progress & Policy       → ACCENT1 = "4EC9C0"  (teal)
Alignment & Safety         → ACCENT2 = "F0A500"  (amber)
Social Impact              → "E05C5C"             (red/coral)
Human Cognition            → "7B68EE"             (purple)
Technical Foundations      → "5CB85C"             (green)
```

### Typography
```
Course label (spaced caps):  10pt, bold, charSpacing: 3, color: ACCENT1
Slide section header:        14pt, bold, charSpacing: 2, color: category accent
Main title (title slide):    56pt, bold, WHITE
Subtitle:                    22pt, OFF_WHITE
Section divider title:       36pt, bold, WHITE, charSpacing: 4
Book card title:             15pt, bold, WHITE
Book author/year:            10pt, italic, category accent color
Body/description text:       12pt, OFF_WHITE
Muted/caption:               10–11pt, MUTED
Footer text:                 10pt, MUTED, centered
```

### Slide Architecture

**Every slide has:**
- Header bar: `x:0, y:0, w:10, h:0.85`, fill: DARK_BG
- Header underline: `x:0, y:0.85, w:10, h:0.045`, fill: category accent color
- Footer bar: `x:0, y:5.2, w:10, h:0.425`, fill: DARK_BG
- Footer text: `"Artificial Intelligence for Lay People  ·  Week N"`, 10pt, MUTED, centered

**Title slide (dark, full bleed):**
- Left accent bar: `x:0, y:0, w:0.12, h:5.625`, fill: ACCENT1
- Right decorative panel: `x:7.8, y:0, w:2.2, h:5.625`, fill: "1E2640"
- Three overlapping translucent circles in right panel (teal + amber, transparency 60–80%)
- Bottom strip replaces footer: `x:0, y:5.2, w:10, h:0.425`, fill: ACCENT1, dark text
- Bottom text: course topics summary (e.g. "History · Capabilities · Limitations · Society · Future")

**Section divider slides (dark background):**
- Left accent bar: `x:0, y:0, w:0.14, h:5.625`, fill: category accent
- Section name: 36pt bold, WHITE, charSpacing: 4, at y≈1.9
- Short rule below title: `w:2.0, h:0.06`, fill: category accent, at y≈2.7
- "SUGGESTED READING" label below rule: 11pt, category accent, charSpacing: 3

**Book card slides (2-up layout):**
- Two cards side by side: left at x:0.3, right at x:5.1, each w:4.55, h:4.3, y:0.9
- Card background: CARD_BG with outer shadow
- Top color stripe: `h:0.08`, fill: category accent
- Title at y+0.15, author/year at y+0.88, horizontal rule at y+1.22
- Description text starts at y+1.3
- Category tag chip (rounded rect) at y+3.98: 1.6" wide, semi-transparent accent fill

**Course overview grid slide:**
- 6 cards in 2×3 grid, each `w:4.55, h:1.1`
- Left column x:0.3, right column x:5.1, rows at y: 1.1, 2.4, 3.7
- Number badge: left 0.5" strip in ACCENT1, dark number text
- Card title: 14pt bold WHITE; subtitle: 11pt MUTED

**Closing slide:**
- Matches title slide style (DARK_BG, decorative circles, ACCENT1 bottom strip)
- "See you next week." — 40pt bold
- Teaser line for next week's topic

### Shadow (reuse via factory function — NEVER reuse object)
```javascript
const makeShadow = () => ({ type: "outer", blur: 8, offset: 3, angle: 135, color: "000000", opacity: 0.20 });
```

### Critical PptxGenJS Rules
- NEVER use `#` prefix on hex colors
- NEVER reuse shadow/option objects across calls (use factory function)
- Use `bullet: true` not unicode `•`
- Use `breakLine: true` between array text items
- Set `margin: 0` when aligning text precisely with shapes

---

## EDITORIAL VOICE & INSTRUCTOR NOTES

The instructor's annotations are direct, opinionated, and sometimes funny. Preserve this voice.
Key examples from Week 1:

- **Zurita (2025):** "The 'author' actually generated most of the book using ChatGPT, so the analysis is shallow. Perhaps it belongs in the autobiography section of the library."
- **Searle:** "I find the argument mysterian." (i.e., points at a mystery without resolving it)
- **Chalmers:** "I haven't actually read this one... I think he is kind of a mysterian."
- **Gullhaug:** "a pamphlet really" — instructor used it to frame prompts and figure out how LLMs work
- **Technical papers (Bengio, Vaswani):** "I can't really understand these, but they are very important"
- **Mitchell (2019):** noted as "dated" because she predicted language AI was decades away — and it wasn't

**General tone:** Direct, intellectually curious, skeptical of hype and mysticism alike, willing to be critical of books, warm toward the audience.

---

## READING LIST (cumulative — all weeks)

### Week 1: Course Overview & Suggested Reading

**AI Progress & Policy**
- *The Coming Wave* — Suleyman (2023) ⭐ START HERE. AI + synthetic biology as unstoppable wave; valuable, dangerous; regulatory roadmap to avoid dystopia.
- *Artificial Intelligence: A Guide for Thinking Humans* — Mitchell (2019). Clear history & inner workings by a practitioner. Dated: predicted language AI was decades away.

**Alignment & Safety**
- *The Alignment Problem* — Brian Christian (2021). Making AIs act in accordance with human values. Harder than Asimov's 3 Laws.

**Social Impact**
- *The Chaos Machine* — Fisher (2023). Recommendation algorithms → outrage, disinformation, polarization, violence.
- *AI Snake Oil* — Narayanan & Kapoor (2025). Predictive AI oversold; hype leads to bad outcomes.
- *A Citizen's Guide to Artificial Intelligence* — Zerilli et al. (2025). Good summary of social issues.
- *Artificial Intelligence and its Impacts on Society* — Zurita (2025). ⚠️ Mostly ChatGPT-generated. Shallow.

**Human Cognition & Consciousness**
- *Thinking, Fast and Slow* — Kahneman (2011). Two-system human cognition; interesting contrast with AI.
- *The Feeling of What Happens* — Damasio (2025). Human consciousness rooted in body/emotion.
- "Minds, Brains, and Programs" — Searle (paper). Chinese Room argument. Instructor: "mysterian."
- *The Conscious Mind* — Chalmers. "Hard problem of consciousness." Instructor: unread; "kind of a mysterian."

**Technical Foundations**
- *The Inner Workings of Large Language Models* — Gullhaug. Short pamphlet; good for framing LLM prompts.
- "A Neural Probabilistic Language Model" — Bengio et al. (2003, paper). Foundational; very technical.
- "Attention is All You Need" — Vaswani et al. (2017, paper). Introduced the Transformer. Very technical.

---

## FILE NAMING CONVENTION
```
AI_Week1_Reading.pptx
AI_Week2_History.pptx
AI_Week3_Capabilities.pptx
... etc.
```

---

## HOW TO USE THIS DOCUMENT IN A NEW SESSION

Paste this entire document into a new Claude chat, then say:
> "Using the style guide above, please generate the slides for Week N: [topic]. Here is the content: ..."

Claude will have everything needed to match Week 1's style exactly.
