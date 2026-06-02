# Contributing

The most useful contribution is a **new tell pattern** or a **language pack**.

## Add a tell pattern
1. Open the relevant taxonomy:
   - writing → `.claude/skills/humanize-writing/references/ai-tell-taxonomy.md`
   - design  → `.claude/skills/humanize-design/references/design-slop-taxonomy.md`
   - image   → `.claude/skills/humanize-image/references/image-tell-taxonomy.md`
2. Add your pattern to the **Candidates** section at the bottom with:
   - **≥2 real-world examples** (a quote, a screenshot, a CSS snippet, an image region),
   - a proposed **severity** (S1/S2/S3) with one line of reasoning,
   - a **fix direction**.
3. Open a PR. A pattern with solid examples gets promoted to a numbered ID.

## Add a language pack (writing, v1 target)
The detection *engine* is language-agnostic; the *pattern list* is not. To add e.g. Japanese:
- create `references/lang/ja/ai-tell-taxonomy.md` following the same ID/severity/fix structure,
- focus on that language's specific tells (for Korean, translationese dominates; for others it may
  be different),
- include real examples.

## Style
- Keep severities honest: S1 = one occurrence outs it; S3 = only a tell in clusters.
- Every pattern needs a **fix direction**, not just a complaint.
- Don't add detector-evasion techniques. This is a quality kit (see docs/ethics.md).

## Credit
Inspired by epoko77-ai/im-not-ai and the revfactory/harness agent pattern.
