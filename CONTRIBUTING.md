# Contributing

The most useful contributions are a **new tell pattern**, a **language pack**, or a **rewriting playbook** for an existing language.

## Repository structure

```
skills/
  humanize-writing/
    SKILL.md                         ← skill instructions (source of truth)
    references/
      ai-tell-taxonomy.md            ← English tells (W-A … W-L)
      rewriting-playbook.md          ← English fix recipes
      lang/
        zh/ai-tell-taxonomy.md       ← Chinese tells
        es/ai-tell-taxonomy.md       ← Spanish tells
        ar/ai-tell-taxonomy.md       ← Arabic tells
        pt/ai-tell-taxonomy.md       ← Portuguese tells
        ko/ai-tell-taxonomy.md       ← Korean tells
  humanize-design/
    SKILL.md
    references/
      design-slop-taxonomy.md
      de-slop-playbook.md
  humanize-image/
    SKILL.md
    references/
      image-tell-taxonomy.md
```

> **Note:** `.claude/skills/` is auto-synced from `skills/` by CI — edit `skills/` only.

---

## Add a tell pattern (any language)

1. Open the relevant taxonomy in `skills/`:
   - English writing → `skills/humanize-writing/references/ai-tell-taxonomy.md`
   - Language pack → `skills/humanize-writing/references/lang/{code}/ai-tell-taxonomy.md`
   - Design → `skills/humanize-design/references/design-slop-taxonomy.md`
   - Image → `skills/humanize-image/references/image-tell-taxonomy.md`
2. Add your pattern to the **Candidates** section at the bottom with:
   - **≥2 real-world examples** (quote, screenshot, CSS snippet, image region)
   - proposed **severity** (S1/S2/S3) with one line of reasoning
   - a **fix direction**
3. Open a PR. A pattern with solid examples gets promoted to a numbered ID.

---

## Add a language pack (new language)

The detection engine is language-agnostic; the pattern list is not.

1. Create `skills/humanize-writing/references/lang/{code}/ai-tell-taxonomy.md` — follow the same `{LANG}-A` through `{LANG}-E` ID/severity/fix structure as existing packs (`zh`, `es`, `ar`, `pt`, `ko`).
2. Focus on that language's specific tells:
   - translationese (loan patterns from English)
   - stock openers
   - antithesis construction equivalent ("not just X, but Y")
   - connective overuse
   - conclusion tells
3. Include ≥2 real examples per pattern.
4. (Optional but valuable) Add `skills/humanize-writing/references/lang/{code}/rewriting-playbook.md` with fix recipes.

---

## Add a rewriting playbook for an existing language

Korean, Chinese, Spanish, Arabic, and Portuguese have taxonomies but no playbook yet. A playbook gives the repairer concrete fix recipes beyond the inline fix direction in the taxonomy.

Structure: follow `skills/humanize-writing/references/rewriting-playbook.md` (the English reference). Create `skills/humanize-writing/references/lang/{code}/rewriting-playbook.md`.

---

## Style rules

- Severities must be honest: S1 = one occurrence outs it; S3 = only a tell in clusters.
- Every pattern needs a **fix direction**, not just a complaint.
- Never add detector-evasion techniques. This is a quality kit. See `docs/ethics.md`.
- Edit `skills/` only — never edit `.claude/skills/` directly (CI overwrites it).

---

## Credit

Inspired by [epoko77-ai/im-not-ai](https://github.com/epoko77-ai/im-not-ai) and the [revfactory/harness](https://github.com/revfactory/harness) agent pattern.
