---
name: humanize-design
description: >-
  Detect and remove "AI slop" from web/UI designs. Language-agnostic.
  NOT a detector-bypass tool.
---

# humanize-design

Strip the generated-default fingerprint from a UI while preserving function.

## When this triggers
"humanize", "de-slop this UI", "looks AI-generated", "kill the AI design look". One sentence is enough.

## The 4 principles
1. **Intent invariant** — routes, form logic, data, functional behavior preserved exactly.
2. **Evidence-based** — change only flagged elements/tokens.
3. **Brand stays** — never swap one cliché for another.
4. **No over-editing** — surgical token/element swaps only.

## Inputs
HTML/CSS/React source (best), a screenshot, or a URL.

## Loop
1. **Detect.** Read `taxonomy.md`. Emit findings (id · severity · selector · evidence · fix_direction) and a slop_score + band (heavy ≥5 / mild 2–4 / clean 0–1).

2. **Repair.** Read `playbook.md`. Fix S1s first, thin S2 clusters, leave lone S3s. Use CSS variables; keep layout working.

3. **Verify (parallel).**
   - *Function:* renders, routes, submits, responds at breakpoints? Accessibility intact?
   - *Naturalness:* slop_score dropped without introducing a new cliché?

4. **Grade & decide.** A/B → ship. C → second pass. D → human review.

## Do-NOT touch
Functional behavior, routes, form logic, real data/metrics, pinned brand tokens.
Do ADD/FIX: accessibility (WCAG AA contrast, visible focus, ≥44px targets, real labels).

## Output
- patched code (or change list for screenshot/URL inputs)
- before/after slop_score
- grade + residual patterns
