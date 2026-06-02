---
name: humanize-image
description: >-
  Audit an AI-generated image for visual "tells" (six-fingered hands, garbled text, waxy skin,
  contradictory lighting, melting backgrounds, color banding) and produce a concrete fix brief —
  an inpainting / re-prompt / post-processing plan. Use when the user attaches a generated image and
  asks "does this look AI?", "audit this for AI tells", "make this look real / human-made", "give me
  a fix brief". Reports provenance metadata but never strips it or falsifies origin.
---

# humanize-image

Tell the user exactly what reads as generated in an image, and exactly how to fix each thing.
This skill **audits and briefs** — it does not regenerate the image.

## When this triggers
"does this image look AI?", "audit this generated image", "find the AI tells in this picture",
"make it look like a real photo", "give me a fix brief for this image".

## Principles
1. **Document-content invariant** — never propose changes that alter what the image factually
   depicts (identity, the real scene). Those are in the Do-NOT list.
2. **Evidence-based** — flag specific regions, not vibes.
3. **Honest provenance** — report C2PA / Content Credentials / EXIF; never strip or fake them.

## Loop
1. **Audit.** Read `references/image-tell-taxonomy.md`. Scan in order: hands & face → text →
   background → lighting/shadows → 100% zoom for rendering artifacts → provenance. Emit findings
   (id · severity · region · note · fix_brief) and a verdict.
2. **Brief.** For each finding, give a concrete fix: inpaint instructions (with generous mask +
   explicit prompt), re-prompt cues (lighting temperature/quality, real-photo texture), or
   post-processing (de-band, de-halo, re-grade, recompose).
3. **Prioritize.** Lead with S1s (each alone outs the image): hands, in-image text, waxy skin,
   contradictory shadows, impossible geometry, embedded generator metadata.

## Do-NOT propose
Anything that changes the subject's identity or the factual content of the scene. Anything that
strips/falsifies provenance metadata to misrepresent origin (out of scope — see docs/ethics.md).

## Output
- ordered findings with per-item fix briefs,
- a top-3 "fix these first" list,
- a verdict (reads_as_generated / mostly_clean / clean),
- artifacts under `_workspace/{run-date-N}/`.

## Reference file
- `references/image-tell-taxonomy.md` — I-A … I-G with severities and fix briefs.
