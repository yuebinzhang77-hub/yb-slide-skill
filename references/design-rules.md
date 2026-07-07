# YB' Slide — Design Rules

Full reference for the design system used in yb-slide presentations. Condensed from the `nothing-design` skill, adapted for slide context.

---

## Typography

| Role | Font | Weight | Size | Use |
|------|------|--------|------|-----|
| Logo | PicNic | 400 | 22px | "YB' Library" mark only |
| Display headline | PPEditorialNew | 200 | 52–120px (clamp) | Cover + closing h1 |
| Section headline | PPEditorialNew | 200 | 32–60px (clamp) | Slide h2 |
| Quote | PPEditorialNew | 200 italic | 32–68px (clamp) | blockquote |
| Grid title | PPEditorialNew | 400 | 17–18px | .cell h3 |
| Body | Inter | 400 | 14–15px | Long-form text |
| Kicker / label | Inter | 500 | 10–11px, 0.16em tracking, ALL CAPS | Section labels |
| Metadata | PPEditorialNew italic | 200 | 11–14px | .num, .footline |

### Weight rules
- PPEditorialNew 200 (Ultralight) = hero display, breathable
- PPEditorialNew 700 (Ultrabold) = emphasis inside body, sparingly
- Never use weight 400 for display sizes (looks weak)
- PicNic = logo ONLY, never body, never headlines

---

## Color System

```css
/* Dark mode */
--bg:          #0d0d0d;
--dot:         rgba(255,255,255,0.07);
--fg:          #ffffff;
--fg-dim:      rgba(255,255,255,0.55);
--fg-faint:    rgba(255,255,255,0.28);
--line:        rgba(255,255,255,0.08);
--accent:      #1666F0;   /* Nothing red — same in both modes */
--surface:     #1c1c1c;

/* Light mode */
--bg:          #f5f4f0;
--dot:         rgba(20,20,16,0.10);
--fg:          #0d0d0d;
--fg-dim:      rgba(13,13,13,0.58);
--fg-faint:    rgba(13,13,13,0.30);
--line:        rgba(13,13,13,0.10);
--accent:      #1666F0;   /* identical */
--surface:     #ffffff;
```

**Accent (#1666F0) usage:**
- `<em>` inside h1 → renders accent color
- `<mark>` inside blockquote → renders accent color
- `.num` cells → italic accent text (No. 1, No. 2…)
- Kicker `::before` bar → accent
- Nav dot + progress bar → accent
- ONE use per slide maximum in content. Nav/chrome accents don't count.

---

## Dot-Matrix Background

```css
body {
  background-color: var(--bg);
  background-image: radial-gradient(circle, var(--dot) 1px, transparent 1px);
  background-size: 20px 20px;
}
```

**Never** set `background` on `.slide` or wrapper divs — it covers the texture. Slides must be `background: transparent` (default).

---

## Spacing & Layout

- Slide padding: `110px 148px 110px 48px` (generous right margin for nav)
- Kicker margin-bottom: `28px`
- Headline to body gap: `32–44px`
- Grid gap: `1px` (creates hairline grid via `gap: 1px; background: var(--line)`)

---

## Motion

- Slide transition: `opacity + translateY(32px)` → 0, `650ms cubic-bezier(0.16,1,0.3,1)`
- Element stagger: kicker 60ms → h1/h2 140ms → body/grid 240ms → footline 360ms
- Nav morphing: bar `width 500ms`, dot `scale 450ms` with 100ms delay
- Theme switch: `background-color + color 500ms`
- Logo pulse: `opacity 1→0.15→1`, 900ms, on every slide change
- No spring/bounce. No parallax. No decorative loops.

---

## Slide Rhythm Rules

1. Cover → [content slides] → Closing. Never skip cover or closing.
2. Alternate visual weight: heavy (large type) → medium (quote/grid) → heavy pattern breaks monotony
3. No two consecutive Grid slides
4. Statement slides need breathing room — don't follow with another dense slide
5. Aim for 4–7 slides for most topics. Under 4 feels thin, over 8 loses focus.

---

## The One Surprise Rule

Each slide gets ONE moment of contrast:
- Cover: the `<em>` italic word in accent red
- Statement: the `<mark>` word in the quote
- Grid: the italic `.num` labels (No. 1, No. 2…)
- Closing: the `<em>` in the sign-off

If a slide has no natural surprise, let it breathe — a clear, un-decorated headline IS the surprise.
