# Design-slop taxonomy (SSOT)

The single source of truth for `humanize-design`. Covers web/UI, landing pages, and HTML/CSS/React
output. Each tell has an **ID**, **severity**, **why**, and **fix direction**. The detector reports
findings as flagged elements/tokens (DOM selector, CSS property, or screenshot region).

> Sourcing: Adrian Krebs' 500-page Show HN audit (15 DOM/CSS patterns; 21% heavy slop, 46% mild),
> the "AI purple problem" design writing of 2025–2026, and the anti-slop guardrail language shipped
> with Claude's own front-end design skill. Models improve, defaults shift — living document.

> **Prime directive for this skill:** *de-slop toward intent/brand, never toward another generic.*
> Removing the purple gradient only to install a different cliché is a failed run.

---

## D-A · Color & gradient tells

| Severity | Pattern |
|---|---|
| **S1** | Purple/indigo → blue (or pink → purple) hero gradient on white. The single most-cited "we used AI" signal. |
| **S1** | Default dark mode with purple/violet accent, chosen because nothing was specified |
| S2 | Gradient-filled headline text; aurora/"blob" gradient background washes |
| S2 | Pastel rainbow accent set; timid, evenly-distributed palette with no dominant color |

**Fix:** commit to a cohesive palette with **one dominant color + sharp accents**, not an even
spread. Pull from a real source — an IDE theme, a cultural/print reference, the brand's actual
assets — via CSS variables. Flat color or a *subtle* same-hue gradient beats the indigo wash.
If dark mode, pick an accent that isn't violet and check body-text contrast (see D-H).

---

## D-B · Layout tells

| Severity | Pattern |
|---|---|
| **S1** | The canonical hero: centered eyebrow + ~64px headline + subhead + two CTAs, nothing else above the fold |
| S2 | Three-up feature cards row (always three, always equal) |
| S2 | 2×2 "bento grid" used regardless of whether the content is grid-shaped |
| S2 | "Trusted by" greyscale logo soup bar |
| S3 | Pricing toggle (monthly/annual) + FAQ accordion as reflexive section furniture |

**Fix:** break symmetry on purpose. Asymmetric hero, off-center focal point, an editorial
left-aligned headline. Let the *content* dictate column count (4 features → 4, or a 2+1). Use a
bento layout only when items genuinely differ in size/weight.

---

## D-C · Component & CSS-fingerprint tells

| Severity | Pattern |
|---|---|
| **S1** | Colored left-border card ("almost as reliable a sign of AI design as the em-dash is for text") |
| S2 | Glassmorphism — frosted translucent cards floating on a soft wash |
| S2 | Stock shadcn/ui default cards + Tailwind `rounded-xl` on every element |
| S2 | Soft drop shadow on everything; uniform large border-radius everywhere |
| S3 | Decorative sparkline widgets; side-tab accent borders; generic "stat counter" row |

**Fix:** pick a deliberate surface language and apply it with restraint — e.g. crisp 1px borders
*or* shadows, not both on everything; varied radii (some square, some round) chosen for meaning;
real depth via layout, not blur. If you use shadcn, restyle the tokens; don't ship defaults.

---

## D-D · Typography tells

| Severity | Pattern |
|---|---|
| **S1** | Inter / Roboto / Arial / system stack as the *only* typeface, chosen by default |
| S2 | Space Grotesk as the lone "I tried" upgrade |
| S2 | One weight, one size ramp, no display/text contrast; no personality |

**Fix:** choose a typeface with a point of view (a distinctive display face for headings + a clean
readable text face). Establish a real type scale and weight contrast. Typography is the cheapest,
highest-impact way to stop looking generated.

---

## D-E · Iconography & illustration tells

| Severity | Pattern |
|---|---|
| **S1** | Emoji used as feature icons (🚀 💡 ✨ 🔒) |
| S2 | Default Lucide/Heroicons line set, untouched, one per card |
| S2 | 3D floating geometric "blob" illustrations; isometric tiny-people; abstract gradient orbs |

**Fix:** use a consistent, intentional icon set (or custom marks) sized and colored to the system.
Replace stock 3D blobs with real product UI, real photography, diagrams, or nothing.

---

## D-F · Motion tells

| Severity | Pattern |
|---|---|
| S2 | Animated gradient blobs drifting in the background |
| S3 | Reflexive fade-up-on-scroll on every section with no choreography |

**Fix:** spend motion budget on **one** well-orchestrated moment — a staggered page-load reveal via
`animation-delay` beats scattered micro-interactions. CSS-only for HTML; Motion for React.

---

## D-G · Content-placeholder tells

| Severity | Pattern |
|---|---|
| S2 | Lorem-ipsum-flavored marketing copy; invented metrics ("10× faster", "99.9%") with no source |
| S2 | Generic three testimonials with avatar + name + title, none real |

**Fix:** real copy, real numbers, or honest placeholders clearly marked. Fake precision is itself
a tell. (Writing tells from `humanize-writing` apply to all on-screen copy.)

---

## D-H · Accessibility red flags (tell **and** real bug)

| Severity | Pattern |
|---|---|
| **S1** | Body text failing WCAG AA contrast — the most common functional defect in generated dark themes |
| S2 | Touch targets < 44px; focus states removed; placeholder used as the only label |

**Fix:** these are never "removed" — they're **fixed**. Meet AA contrast, restore visible focus,
size targets, add real labels. This is the one category where the skill *adds*.

---

## Severity in context

A page triggering **5+ patterns = heavy slop**; **2–4 = mild**; **0–1 = clean.** The skill targets
S1s first (each alone outs the page), then thins S2 clusters, and leaves lone S3s unless they pile up.

## Detector output format

```json
{
  "findings": [
    {
      "id": "D-A",
      "severity": "S1",
      "selector": ".hero",
      "evidence": "background: linear-gradient(135deg,#6366f1,#3b82f6)",
      "note": "default indigo→blue hero gradient",
      "fix_direction": "replace with brand palette; one dominant color + accent; flat or subtle same-hue"
    }
  ],
  "slop_score": 6,
  "band": "heavy"
}
```

## Versioning

New patterns → candidates at the bottom, ≥2 real examples each, proposed severity + fix.

### Candidates (unpromoted)
- *"Aurora" navbar blur with semi-transparent sticky header* — needs examples.
- *Identical 8px-grid spacing with no rhythm variation* — needs examples.
