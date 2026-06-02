---
name: humanize-design
description: >-
  Detect and remove "AI slop" from web/UI designs and front-end code so they look intentionally
  crafted, not like the default a chat model emits (purple gradients, glassmorphism, Inter font,
  bento grids, colored left-border cards). Use when the user pastes HTML/CSS/React, a screenshot, or
  a URL and asks to "de-slop the UI", "make it not look AI-generated", "kill the AI design look",
  "humanize this landing page", while keeping layout and behavior working. De-slops toward
  intent/brand, never toward another generic.
---

# humanize-design

Strip the generated-default fingerprint from a UI while preserving its function and improving it
toward a real point of view (or the user's brand).

## When this triggers
"de-slop this UI", "it looks AI-generated, fix it", "kill the AI design look", "humanize this
landing page", "make this not look vibe-coded", "remove the purple-gradient look".

## The 4 principles
1. **Intent invariant** — routes, form logic, data, and functional behavior preserved exactly.
2. **Evidence-based** — change only flagged elements/tokens.
3. **Brand stays** — never swap one cliché for another. De-slop *toward* the brand or a deliberate
   aesthetic, not toward a different generic.
4. **No over-editing** — don't rebuild what works; surgical token/element swaps.

## Inputs
HTML/CSS/React source (best), a screenshot, or a URL. If only a screenshot/URL, describe findings
and produce concrete CSS/markup changes the user can apply.

## Loop
1. **Detect.** Read `references/design-slop-taxonomy.md`. Emit findings (id · severity · selector ·
   evidence · fix_direction) and a `slop_score` + band (heavy ≥5 / mild 2–4 / clean 0–1).
2. **Repair.** Read `references/de-slop-playbook.md`. Fix S1s first (each alone outs the page),
   thin S2 clusters, leave lone S3s. Use CSS variables; keep the existing layout grid working.
3. **Verify (parallel).**
   - *Function:* does it still render, route, submit, and respond at breakpoints? Accessibility
     intact or improved (contrast, focus, target size)?
   - *Naturalness:* re-score. Did the slop_score drop without introducing a new cliché?
4. **Grade & decide.** A/B → ship. C → second pass. D → human review.

## Do-NOT touch (and the one thing to ADD)
Do-NOT change: functional behavior, routes, form logic, real data/metrics, pinned brand tokens.
Do **add/fix**: accessibility (WCAG AA contrast, visible focus, ≥44px targets, real labels) — this
is the only category where the skill repairs rather than removes.

## Output
- patched code (or a concrete change list for screenshot/URL inputs),
- before/after slop_score,
- a grade + residual patterns,
- artifacts under `_workspace/{run-date-N}/`.

## Reference files
- `references/design-slop-taxonomy.md` — D-A … D-H with severities.
- `references/de-slop-playbook.md` — fix recipes (palette, type, layout, components, motion, a11y).
