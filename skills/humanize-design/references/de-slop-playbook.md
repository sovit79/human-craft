# De-slop playbook (design)

Concrete fixes per taxonomy category. De-slop **toward intent/brand**, never toward a different
cliché. Surgical token/element swaps — don't rebuild what works.

## General order
1. Kill S1s (each alone outs the page): default indigo→blue gradient, default-purple dark mode,
   colored left-border cards, emoji icons, Inter-as-only-font, AA-failing body text.
2. Thin S2 clusters (glassmorphism, three-up cards, bento, soft shadows everywhere).
3. Leave lone S3s.
Use CSS variables throughout so the brand can be swapped in one place.

---

## D-A color
- Define a palette as variables: one **dominant** color + 1–2 sharp accents, not an even spread.
  Pull from a real source (IDE theme, print/cultural reference, brand assets).
- Replace the indigo→blue hero gradient with flat brand color or a *subtle same-hue* gradient.
- If dark mode: pick a non-violet accent; verify body-text contrast (D-H).
```css
:root{
  --bg:#0e0f13; --surface:#16181d; --text:#e7e9ee; --muted:#9aa0ab;
  --brand:#d8492b;   /* one dominant color, not purple */
  --accent:#1f9c8b;  /* one sharp accent */
}
```

## D-B layout
- Break the centered hero: left-align the headline, place an off-center focal element, vary above-
  the-fold content. Let content set column count (4 features → 4, or 2+1), not a reflexive three.
- Use bento only when items genuinely differ in size/weight.

## D-C components
- Pick **one** surface language: crisp 1px borders *or* shadows — not both on everything.
- Remove the colored left-border card pattern outright (it's an S1).
- Vary border-radius by role (some square, some round); drop the universal `rounded-xl`.
- If using shadcn, restyle the tokens (radius, shadow, color); never ship the defaults.

## D-D typography
- Choose a display face with personality for headings + a clean readable text face. Set a real
  scale and weight contrast. Avoid Inter/Roboto/Arial as the sole face.
```css
:root{ --font-display:"Fraunces",serif; --font-text:"Public Sans",system-ui; }
h1,h2{font-family:var(--font-display)} body{font-family:var(--font-text)}
```
(Pick faces that fit the brand — the point is *intent*, not these specific names.)

## D-E icons & illustration
- Use one intentional icon set (or custom marks), sized/colored to the system. Remove emoji icons.
- Replace stock 3D blobs / isometric people with real product UI, photography, diagrams, or nothing.

## D-F motion
- Spend the budget on one orchestrated page-load reveal (staggered `animation-delay`) instead of
  fade-up on every section. CSS-only for HTML; Motion for React. Remove drifting gradient blobs.

## D-G content
- Replace lorem-flavored copy and invented metrics with real text/numbers or clearly-marked
  placeholders. Apply `humanize-writing` to all on-screen copy.

## D-H accessibility (ADD/FIX — never remove)
- Body text ≥ 4.5:1 contrast (≥3:1 large). Restore visible `:focus-visible`. Targets ≥44px.
  Real `<label>`s, not placeholder-as-label.

---

## Verify before shipping
- Renders at mobile / tablet / desktop breakpoints; routes and forms still work.
- `slop_score` dropped **and** no new cliché was introduced.
- Contrast/focus/targets pass.

## Failure modes to avoid
- *Cliché-swap:* trading purple gradient for the exact "neobrutalism default" or "glassmorphism →
  claymorphism." Aim for the brand, not the next trend.
- *Function breakage:* restyling that kills a working grid, route, or form. Tokens first, structure last.
- *A11y regression:* prettier but lower contrast. Always re-check D-H after color changes.
