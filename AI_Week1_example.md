---
marp: true
theme: ai-course
paginate: false
---

<!--
  AI COURSE THEME — USAGE REFERENCE & CHEAT SHEET
  ================================================
  
  SETUP (one time only):
  1. Place ai-course-theme.css in ./themes/ai-course-theme.css
  2. Add to VS Code settings.json:
     "markdown.marp.themes": ["./themes/ai-course-theme.css"]
  3. Use this front matter at the top of every slide deck (as above).

  SLIDE CLASS REFERENCE:
  ─────────────────────────────────────────────────────────────
  <!-- _class: title -->          Title slide (dark, full bleed)
  <!-- _class: divider progress --> Section divider + category color
  <!-- _class: book-cards progress --> 2-up book card layout
  <!-- _class: overview-grid -->  Course overview 6-card grid
  <!-- _class: closing -->        Closing slide (matches title style)
  (default, no class)             Standard content slide

  CATEGORY CLASSES (add alongside layout class):
  ─────────────────────────────────────────────────────────────
  progress    AI Progress & Policy    → teal   #4EC9C0
  alignment   Alignment & Safety      → amber  #F0A500
  social      Social Impact           → coral  #E05C5C
  cognition   Human Cognition         → purple #7B68EE
  technical   Technical Foundations   → green  #5CB85C

  SPECIAL INLINE ELEMENTS:
  ─────────────────────────────────────────────────────────────
  <div class="callout">Instructor note text</div>
  <span class="badge-warning">⚠ CAUTION</span>
  <span class="badge-star">⭐ START HERE</span>
  <span class="muted">Caption or secondary text</span>
-->

---

<!-- _class: title -->

<div class="accent-bar"></div>
<div class="deco-panel"><div class="circle3"></div></div>

<div class="title-content">
<div class="course-label">Understanding Artificial Intelligence</div>

# Course Overview &<br>Suggested Reading

## Week 1 · For the Curious Non-Specialist
</div>

<div class="title-footer">History · Capabilities · Limitations · Society · Future</div>

---

<!-- Standard content slide (no class needed) -->

## AI Progress & Policy

# What This Course Covers

- Seven weeks of accessible, honest AI discussion
- No technical background required
- Books range from essential to "read with skepticism"
- Instructor notes included throughout

<div class="callout">
<strong>Instructor:</strong> The goal is to leave you with a working mental model of AI — not hype, not panic.
</div>

---

<!-- _class: overview-grid -->

<div class="header-label">Course Structure</div>

<div class="grid-container">
  <div class="grid-card">
    <div class="grid-number">1</div>
    <div class="grid-text">
      <div class="grid-title">Course Overview</div>
      <div class="grid-subtitle">Suggested Reading</div>
    </div>
  </div>
  <div class="grid-card">
    <div class="grid-number">2</div>
    <div class="grid-text">
      <div class="grid-title">A Brief History</div>
      <div class="grid-subtitle">of Artificial Intelligence</div>
    </div>
  </div>
  <div class="grid-card">
    <div class="grid-number">3</div>
    <div class="grid-text">
      <div class="grid-title">Current Capabilities</div>
      <div class="grid-subtitle">What AI can do today</div>
    </div>
  </div>
  <div class="grid-card">
    <div class="grid-number">4</div>
    <div class="grid-text">
      <div class="grid-title">Current Limitations</div>
      <div class="grid-subtitle">Where AI still falls short</div>
    </div>
  </div>
  <div class="grid-card">
    <div class="grid-number">5</div>
    <div class="grid-text">
      <div class="grid-title">AI vs. Human Cognition</div>
      <div class="grid-subtitle">Minds, brains, and programs</div>
    </div>
  </div>
  <div class="grid-card">
    <div class="grid-number">6</div>
    <div class="grid-text">
      <div class="grid-title">Effects on Society</div>
      <div class="grid-subtitle">Positive and negative</div>
    </div>
  </div>
</div>

<div class="footer">Artificial Intelligence for Lay People · Week 1</div>

---

<!-- _class: divider progress -->

<div class="divider-content">

# AI Progress<br>& Policy

<div class="rule"></div>
<div class="reading-label">Suggested Reading</div>

</div>

<div class="footer">Artificial Intelligence for Lay People · Week 1</div>

---

<!-- _class: book-cards progress -->

<div class="cards-container">
  <div class="book-card">
    <div class="card-stripe"></div>
    <div class="card-body">
      <div class="card-title">The Coming Wave</div>
      <div class="card-meta">Mustafa Suleyman · 2023</div>
      <div class="card-rule"></div>
      <div class="card-desc">
        AI and synthetic biology as an unstoppable wave — valuable and dangerous. Offers a regulatory roadmap to avoid dystopia. Essential reading for understanding where we are headed.
        <br><br>
        <span class="badge-star">⭐ START HERE</span>
      </div>
      <div class="card-tag">AI Progress & Policy</div>
    </div>
  </div>
  <div class="book-card">
    <div class="card-stripe"></div>
    <div class="card-body">
      <div class="card-title">Artificial Intelligence: A Guide for Thinking Humans</div>
      <div class="card-meta">Melanie Mitchell · 2019</div>
      <div class="card-rule"></div>
      <div class="card-desc">
        Clear history and inner workings by a practitioner. Highly readable.
        <br><br>
        <div class="callout"><strong>Instructor:</strong> Dated — she predicted language AI was decades away. It wasn't.</div>
      </div>
      <div class="card-tag">AI Progress & Policy</div>
    </div>
  </div>
</div>

<div class="footer">Artificial Intelligence for Lay People · Week 1</div>

---

<!-- _class: divider alignment -->

<div class="divider-content">

# Alignment<br>& Safety

<div class="rule"></div>
<div class="reading-label">Suggested Reading</div>

</div>

<div class="footer">Artificial Intelligence for Lay People · Week 1</div>

---

<!-- _class: book-cards alignment -->

<div class="cards-container">
  <div class="book-card">
    <div class="card-stripe"></div>
    <div class="card-body">
      <div class="card-title">The Alignment Problem</div>
      <div class="card-meta">Brian Christian · 2021</div>
      <div class="card-rule"></div>
      <div class="card-desc">
        Making AIs act in accordance with human values. It turns out this is much harder than Asimov's Three Laws would suggest.
        <br><br>
        One of the most important books on where AI development could go wrong — and what people are doing about it.
      </div>
      <div class="card-tag">Alignment & Safety</div>
    </div>
  </div>
  <div class="book-card">
    <div class="card-stripe"></div>
    <div class="card-body">
      <div class="card-title">AI Snake Oil</div>
      <div class="card-meta">Narayanan & Kapoor · 2025</div>
      <div class="card-rule"></div>
      <div class="card-desc">
        Predictive AI is widely oversold. The hype leads to real and harmful outcomes when unproven systems are deployed in high-stakes decisions.
        <br><br>
        A useful corrective to breathless media coverage.
      </div>
      <div class="card-tag">Social Impact</div>
    </div>
  </div>
</div>

<div class="footer">Artificial Intelligence for Lay People · Week 1</div>

---

<!-- _class: closing -->

<div class="accent-bar"></div>
<div class="deco-panel"></div>

<div class="closing-content">

# See you next week.

## Next up: A Brief History of Artificial Intelligence

</div>

<div class="closing-footer">History · Capabilities · Limitations · Society · Future</div>
