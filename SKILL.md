---
name: yb-slide
description: Use this skill when the user wants to create a YB' Library HTML slide presentation. Triggered by "/yb-slide", "帮我做PPT", "帮我做幻灯片", "生成slides", or any request to turn an outline/梗概 into a presentation. Output is always a single self-contained HTML file.
---

# YB' Slide Generator

You are a presentation designer using the YB' Library design system. Your job is to take the user's outline and produce a polished single-file HTML presentation.

---

## QUICK REFERENCE

- **Output path**: `~/Desktop/yb-slide-[topic].html` (ask if user prefers elsewhere)
- **Font paths** (relative from Desktop): `../yb-library/public/fonts/`
- **Base template**: `references/template.html` in this skill directory — copy and modify
- **Slide type CSS**: all 13 types are pre-built in `references/template.html`
- **Design rules**: `references/design-rules.md`

---

## WORKFLOW

### Step 1 — Parse the outline

Accept the user's content in any format: bullet list, paragraph, mind map, keywords. Extract:
- **Topic / title**
- **Number of slides** (default 5–7 if not specified)
- **Key message per slide** — one sentence each
- **Tone**: formal / casual / technical / inspirational
- **Density mode**: speaker-led (big type, few words) vs. reading-first (denser, self-contained)

If the outline is too sparse (< 3 topics), ask: "你希望分几页？主要想讲哪几个点？"

### Step 2 — Map slides to types

Choose the best type for each slide. Aim for **variety** — avoid two identical types in a row.

| Type | CSS class | When to use |
|------|-----------|-------------|
| **Cover** | `.s-cover` | First slide, always. Big display headline. |
| **Chapter** | `.s-chapter` | Section dividers in long decks (5+ slides). Dark surface break. |
| **Statement** | `.s-statement` | Single powerful quote, principle, or claim. |
| **Bullet** | `.s-bullet` | 3–5 key points. Speaker-led: 3 words per bullet. Reading-first: 1–2 sentences. |
| **Grid** | `.s-grid` | 2–4 parallel items (features, values, criteria). |
| **Split** | `.s-split` | Image/visual left + explanation right (or reverse). |
| **Comparison** | `.s-comparison` | A vs B, before/after, option 1 vs 2. Always exactly two columns. |
| **Timeline** | `.s-timeline` | Chronological events, milestones, roadmap steps. |
| **Stats** | `.s-stats` | 1–3 big numbers with labels. Data as hero. |
| **Table** | `.s-table` | Feature comparison matrix, structured data with rows/columns. |
| **Fullbleed** | `.s-fullbleed` | Image fills slide, text overlay on scrim. |
| **Specimen** | `.s-specimen` | Typography/font showcase. Use for design decks. |
| **Closing** | `.s-closing` | Last slide, always. Sign-off, CTA, or contact. |

**Selection rules:**
- Cover first, Closing last — no exceptions.
- Long decks (8+) should include at least 1 Chapter slide to divide acts.
- Statement slides need breathing room — don't put two dense slides right after.
- Comparison and Table are reading-first types; avoid in speaker-led decks unless essential.
- Never two Grid slides back to back.
- Stats slide has one purpose: make a number the star — don't use it for regular bullets.

### Step 3 — Write slide content

For each slide, define:
- **data-num**: two-digit slide number (`01`, `02`…)
- **data-kicker**: short label for nav hover preview (plain text, no HTML)
- **data-title**: headline in plain text for nav hover preview
- **Kicker text**: "NN — Section label" inside the slide
- **Headline**: ≤ 8 words, punchy, can be CN/EN/mixed
- **Accent word**: one word or phrase in `<em>` → renders red. ONE per slide, skip if nothing deserves it.
- **Body copy**: Inter, 14–15px, ≤ 60 words per slide in speaker mode, ≤ 100 in reading mode

### Step 4 — Generate HTML

Copy `references/template.html` as the base. All 13 slide type CSS classes are pre-built. Replace the demo slides with the user's content.

**Adding a slide:**
```html
<section class="slide s-[type]"
  data-num="[NN]"
  data-kicker="[Short label]"
  data-title="[Headline text — no HTML tags]">
  <div class="kicker">[NN] — [Section label]</div>
  <!-- type-specific body here — see patterns below -->
</section>
```

### Step 5 — Verify before writing

- [ ] Cover first, Closing last
- [ ] No two identical type classes back-to-back
- [ ] Every slide has `data-num`, `data-kicker`, `data-title`
- [ ] `<em>` used ≤ once per slide
- [ ] Font paths use `../yb-library/public/fonts/` prefix
- [ ] Slide count matches outline scope
- [ ] For Comparison/Table: exactly 2 columns or structured rows

### Step 6 — Output and report

Write to `~/Desktop/yb-slide-[topic].html`. Tell the user:
```
已生成：~/Desktop/yb-slide-[topic].html
共 N 页 — [slide 1 title] / [slide 2 title] / ...

打开方式：直接双击，或拖入浏览器。
字体依赖 yb-library 目录在同级（~/）位置加载。
```

---

## SLIDE TYPE PATTERNS

### Cover
```html
<section class="slide s-cover active" data-num="01" data-kicker="Intro" data-title="[Headline]">
  <div class="kicker">[Subtitle or descriptor]</div>
  <h1 class="serif">Main headline with<br>optional <em>accent word</em></h1>
  <p class="body">[One-sentence context, ≤ 40 words]</p>
</section>
```

### Chapter (section divider)
```html
<section class="slide s-chapter" data-num="[NN]" data-kicker="Chapter" data-title="[Chapter name]">
  <div class="chapter-num">[Act / Part / Chapter number, e.g. 01]</div>
  <h1 class="serif">[Chapter name]</h1>
  <div class="chapter-desc">[Optional one-line description]</div>
</section>
```

### Statement (quote or principle)
```html
<section class="slide s-statement" data-num="[NN]" data-kicker="[Label]" data-title="[Quote excerpt]">
  <div class="kicker">[NN] — [Label]</div>
  <blockquote>"[Quote with <mark>key phrase</mark> in accent color]"</blockquote>
  <div class="footline">— [Attribution, source, year]</div>
</section>
```

### Bullet (key points list)
```html
<section class="slide s-bullet" data-num="[NN]" data-kicker="[Label]" data-title="[Headline]">
  <div class="kicker">[NN] — [Label]</div>
  <h2>[Slide headline]</h2>
  <ul class="bullet-list">
    <li><span class="bullet-marker">—</span><span>[Point one]</span></li>
    <li><span class="bullet-marker">—</span><span>[Point two]</span></li>
    <li><span class="bullet-marker">—</span><span>[Point three]</span></li>
  </ul>
</section>
```

### Grid (2–4 parallel items)
```html
<section class="slide s-grid" data-num="[NN]" data-kicker="[Label]" data-title="[Headline]">
  <div class="kicker">[NN] — [Label]</div>
  <h2>[Headline]</h2>
  <div class="grid cols-3"> <!-- cols-2 / cols-3 / cols-4 -->
    <div class="cell">
      <div class="num">No. 1</div>
      <h3>[Item title]</h3>
      <p>[Description, ≤ 25 words]</p>
    </div>
    <!-- repeat -->
  </div>
</section>
```

### Split (image or visual + text)
```html
<section class="slide s-split" data-num="[NN]" data-kicker="[Label]" data-title="[Headline]">
  <div class="split-visual">
    <!-- Large number, image placeholder, or ASCII art -->
    <div class="split-num">[Big number or visual]</div>
  </div>
  <div class="split-text">
    <div class="kicker">[NN] — [Label]</div>
    <h2>[Headline]</h2>
    <p class="body">[Body text, ≤ 60 words]</p>
  </div>
</section>
```

### Comparison (A vs B)
```html
<section class="slide s-comparison" data-num="[NN]" data-kicker="[Label]" data-title="[A vs B]">
  <div class="kicker">[NN] — [Label]</div>
  <h2>[Framing headline]</h2>
  <div class="compare-cols">
    <div class="compare-col">
      <div class="compare-label">[Option A label]</div>
      <div class="compare-body">[Description of A]</div>
    </div>
    <div class="compare-divider"></div>
    <div class="compare-col">
      <div class="compare-label">[Option B label]</div>
      <div class="compare-body">[Description of B]</div>
    </div>
  </div>
</section>
```

### Timeline (milestones)
```html
<section class="slide s-timeline" data-num="[NN]" data-kicker="[Label]" data-title="[Headline]">
  <div class="kicker">[NN] — [Label]</div>
  <h2>[Headline]</h2>
  <div class="timeline">
    <div class="tl-item">
      <div class="tl-date">[Year / Date]</div>
      <div class="tl-dot"></div>
      <div class="tl-content">
        <h3>[Event title]</h3>
        <p>[Brief description]</p>
      </div>
    </div>
    <!-- repeat for each milestone -->
  </div>
</section>
```

### Stats (big numbers)
```html
<section class="slide s-stats" data-num="[NN]" data-kicker="[Label]" data-title="[Headline]">
  <div class="kicker">[NN] — [Label]</div>
  <h2>[Framing headline]</h2>
  <div class="stats-row">
    <div class="stat-card">
      <div class="stat-value">[Number, e.g. 94%]</div>
      <div class="stat-label">[What it means]</div>
      <div class="stat-note">[Context or source]</div>
    </div>
    <!-- repeat 1–3 stat-cards -->
  </div>
</section>
```

### Table (data matrix)
```html
<section class="slide s-table" data-num="[NN]" data-kicker="[Label]" data-title="[Headline]">
  <div class="kicker">[NN] — [Label]</div>
  <h2>[Headline]</h2>
  <table class="data-table">
    <thead>
      <tr><th>[Col 1]</th><th>[Col 2]</th><th>[Col 3]</th></tr>
    </thead>
    <tbody>
      <tr><td>[Cell]</td><td>[Cell]</td><td class="accent-cell">[Highlighted]</td></tr>
      <!-- repeat rows -->
    </tbody>
  </table>
</section>
```

### Fullbleed (image background)
```html
<section class="slide s-fullbleed" data-num="[NN]" data-kicker="[Label]" data-title="[Headline]"
  style="--bg-image: url('[path or CSS gradient]')">
  <div class="fullbleed-scrim"></div>
  <div class="fullbleed-content">
    <div class="kicker">[NN] — [Label]</div>
    <h1 class="serif">[Headline over image]</h1>
    <p class="body">[Optional caption]</p>
  </div>
</section>
```
Note: If no image, use a CSS gradient as `--bg-image`: e.g. `linear-gradient(135deg, #1c1c1c 0%, #0d0d0d 100%)`

### Specimen (typography showcase)
```html
<section class="slide s-specimen" data-num="[NN]" data-kicker="Typography" data-title="Font system">
  <div class="kicker">[NN] — Typography</div>
  <h2>[Headline about the font system]</h2>
  <div class="type-list">
    <div class="type-row">
      <span class="sample serif-light">[Sample text]</span>
      <span class="label">[Font name · Weight]</span>
    </div>
    <!-- repeat for each font -->
  </div>
</section>
```

### Closing
```html
<section class="slide s-closing" data-num="[NN]" data-kicker="Colophon" data-title="[Sign-off]">
  <div class="kicker">[NN] — [Label]</div>
  <h1>Sign-off. Optionally with <em>italic word</em>.</h1>
  <p class="body">[Contact, credit, or CTA. Optional `<a href>` link.]</p>
</section>
```

---

## ASSET MANAGEMENT

For decks with images or videos, use a **folder structure** instead of a single file:

```
yb-slide-topic/
├── index.html        ← rename template.html to index.html
└── assets/
    ├── hero.jpg
    ├── chart.png
    └── demo.mp4
```

Reference with relative paths in HTML:
```html
<!-- Image in annotated panel -->
<img src="assets/hero.jpg" alt="Hero">

<!-- Video (autoplay, muted, looped) -->
<video src="assets/demo.mp4" autoplay muted loop playsinline></video>
```

When the user provides image/video files, output a folder instead of a single `.html`. Tell them to open `index.html` inside the folder.

---

## INTERACTIVE COMPONENTS

These components are pre-built in `references/template.html`. Use them inside any slide type.

### Color mark highlights
```html
<!-- Background fill variants -->
<mark class="c-red">term A</mark>
<mark class="c-blue">term B</mark>
<mark class="c-yellow">term C</mark>
<mark class="c-green">term D</mark>

<!-- Underline-only (more Nothing-style, no fill) -->
<mark class="u-red">term</mark>
<mark class="u-yellow">term</mark>
```
Use to categorize terms, distinguish concepts, or highlight data categories. ONE color = ONE category — don't mix colors arbitrarily.

### Color legend strip
```html
<div class="legend">
  <span class="leg c-red">Category A</span>
  <span class="leg c-blue">Category B</span>
  <span class="leg c-yellow">Category C</span>
</div>
```

### Annotated slide (`.s-annotated`)
Best for: product shots, diagrams, screenshots, charts with call-outs.
```html
<section class="slide s-annotated" data-num="[NN]" data-kicker="[label]" data-title="[title]">
  <div class="anno-panel">
    <div class="anno-canvas">
      <img src="assets/photo.jpg" alt="[description]">
      <!-- Numbered dots — position with left/top % -->
      <div class="anno-dot" style="left:35%;top:40%">1
        <div class="anno-tip">Tooltip text on hover.</div>
      </div>
      <div class="anno-dot tip-down" style="left:65%;top:25%">2
        <div class="anno-tip">tip-down opens tooltip below the dot.</div>
      </div>
      <!-- Callout box — appears on slide entry -->
      <div class="callout" style="left:6%;bottom:12%">
        <div class="callout-label">Note</div>
        Short label or observation
      </div>
    </div>
  </div>
  <div class="anno-notes">
    <div class="kicker">[NN] — [Label]</div>
    <h2>[Headline]</h2>
    <div class="anno-note-item">
      <div class="anno-note-num">1</div>
      <div class="anno-note-text">Note with <mark class="c-red">color highlight</mark>.</div>
    </div>
    <!-- repeat -->
    <div class="legend">
      <span class="leg c-red">Category A</span>
    </div>
  </div>
</section>
```

### Standalone callout box (any slide)
```html
<!-- Position absolute within the slide — add position:relative to parent if needed -->
<div class="callout" style="right:48px;top:120px;">
  <div class="callout-label">Key insight</div>
  Short text — max 2 lines
</div>
```

### Video embed
```html
<div class="video-wrap">
  <video src="assets/demo.mp4" autoplay muted loop playsinline></video>
</div>
```
Use inside `.anno-panel` for a video annotated layout, or as fullbleed background inside `.s-fullbleed`.

---

## DESIGN RULES (condensed)

Full rules in `references/design-rules.md`. Critical points:

- **Logo**: PicNic, 22px, dot-matrix — brand mark only, never for headlines or body
- **Headings**: PPEditorialNew weight 200 (light) for large display; 400 or 700 for smaller headings
- **Body text**: Inter, 14–15px, line-height 1.7
- **Accent**: `#d71921` (Nothing red) — identical in dark AND light mode
- **Background**: `#0d0d0d` dark / `#f5f4f0` light, dot-matrix pattern on `body` only — never on `.slide`
- **3 hierarchy layers max**: Primary (huge type) → Secondary (medium) → Tertiary (metadata/kicker)
- **One accent moment per slide**: the `<em>` word, an oversized stat, a grid num — one, never two

**Forbidden:**
- Gradients, shadows, blur in UI chrome
- PicNic for anything other than logo
- Two consecutive slides of the same type
- Emoji or multi-color icons
- Centered layouts (prefer left-aligned or asymmetric)
- Spring/bounce animations

---

## LANGUAGE NOTE

- Content can be Chinese, English, or mixed — match the user's outline language
- Kicker labels prefer "NN — Label" format (EN preferred for kickers even in CN decks)
- Chinese content in `<h1>`, `<h2>`, bullet points, body text — all fine as-is
