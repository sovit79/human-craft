# Image AI-tell taxonomy (SSOT)

The single source of truth for `humanize-image`. This skill **audits** a generated image and
produces a **fix brief** (an inpainting / re-prompt / post-processing plan). It does not regenerate
the image itself — it tells you exactly what reads as AI and how to fix each thing.

> Sourcing: 2026 detection guides (PixPipe, Which-One-Is-AI, ZSky, Undetectr) and inpainting fix
> guides. Each model generation has fewer/weaker artifacts — re-check against current models.
> The reliable strategy is **multiple indicators at once**, not any single test.

> **Scope:** this audits whether an image *reads as generated*. It does not, and must not, change
> what the image documents. Identity and factual scene content are in the Do-NOT list.

---

## I-A · Anatomy

| Severity | Pattern |
|---|---|
| **S1** | Hands/fingers: extra, fused, or missing digits; wrong joint angles |
| **S1** | Asymmetric paired features that should match: earrings, glasses arms, shoe details |
| S2 | Eyes: mismatched reflections, irregular pupils; teeth that blur into one mass |
| S2 | Ears, hairlines, or limbs that merge into background/other people |

**Fix brief:** inpaint the region, masking generously (include wrist + a little forearm for hands so
the model has context). Prompt explicitly: "realistic human right hand, five fingers, natural
proportions, matching skin tone and lighting." Never "fix the hand" — too vague.

---

## I-B · Text inside the image

| Severity | Pattern |
|---|---|
| **S1** | Any signage, label, book cover, or UI text that's garbled, misspelled, or nonsense glyphs |

Models don't read; embedded text is almost always wrong. One garbled sign = decisive.

**Fix brief:** inpaint the text region with the exact intended string, or compose real text in
post (the typographically correct, honest option). If text must be legible, add it as a real layer
rather than trusting generation.

---

## I-C · Texture / skin

| Severity | Pattern |
|---|---|
| **S1** | Waxy/plastic skin; pores too smooth; a uniform glossy sheen on forehead/cheeks/neck |
| S2 | Texture quality that shifts abruptly between patches (photoreal next to painterly) |

**Fix brief:** add subtle skin texture/grain in post; reduce the global "beauty-filter" smoothness;
match grain across the whole frame. In prompts, specify real-photo cues (film stock, natural skin).

---

## I-D · Lighting & shadows

| Severity | Pattern |
|---|---|
| **S1** | Shadow directions that contradict each other; a face lit left with the shadow falling left too |
| S2 | Highlights on different objects implying different light sources; reflections in eyes that don't match the scene |
| S2 | Missing, duplicated, or impossibly-shaped shadows |

**Fix brief:** decide one light direction and correct offending shadows/highlights in post.
At prompt time specify color temperature + quality ("warm tungsten key, cool fill, soft diffused") —
flat default lighting is itself a tell.

---

## I-E · Background & geometry

| Severity | Pattern |
|---|---|
| **S1** | Objects melting/merging; impossible architecture; windows onto incoherent space |
| S2 | Straight lines that wobble or converge unnaturally; foliage as a vague blurry mass, not leaves |
| S3 | Background detail/attention noticeably lower than the subject (model "spent" its budget on the subject) |

**Fix brief:** inpaint the broken region; straighten lines in post; add background structure or crop
the incoherent area out.

---

## I-F · Rendering signature

| Severity | Pattern |
|---|---|
| S2 | Color banding — visible steps in skies/gradients instead of smooth transitions |
| S2 | Halo/shimmer edges around the subject |
| S2 | The "default generator look": dead-center subject, heavy bokeh, dramatic teal-orange grade, hyper-detailed everything |

**Fix brief:** add subtle dithering/grain to kill banding; clean edge halos with a mask; re-grade
away from the teal-orange default; recompose off-center; dial back the "epic" so it reads like a
photograph someone actually took.

---

## I-G · Provenance & metadata (not visual, but decisive)

| Severity | Pattern |
|---|---|
| **S1** | C2PA / Content Credentials embedded by the generator; generator name in EXIF |

**Note (ethics):** this skill **reports** provenance metadata so you understand what a viewer/tool
could find. It does **not** strip C2PA or falsify metadata — removing provenance to misrepresent
origin is out of scope and against [`docs/ethics.md`](../../../../docs/ethics.md). Where origin
disclosure is required, keep the credentials and disclose.

---

## How to audit (the 5-second order, then deep)

1. **Hands & face** (I-A, I-C) → 2. **Any text** (I-B) → 3. **Background** (I-E) →
4. **Lighting/shadows** (I-D) → 5. zoom to 100% and scan systematically for I-F.
Then check **provenance** (I-G). Flag everything; weight by how many fire together.

## Auditor output format

```json
{
  "findings": [
    {"id": "I-A", "severity": "S1", "region": "subject right hand",
     "note": "six fingers", "fix_brief": "inpaint hand, mask wrist+forearm, explicit 5-finger prompt"},
    {"id": "I-B", "severity": "S1", "region": "background shop sign",
     "note": "garbled glyphs", "fix_brief": "inpaint with intended text or composite real text in post"}
  ],
  "verdict": "reads_as_generated",
  "top_fixes": ["hand inpaint", "sign text", "kill skin sheen"]
}
```

## Versioning

Candidates at the bottom, ≥2 examples, proposed severity + fix brief.

### Candidates (unpromoted)
- *Video tell bleed-over: "Sora hover" / feet not planting* (if the kit extends to video) — needs examples.
- *Repeating micro-pattern textures (fabric, foliage) that tile unnaturally* — needs examples.
