---
name: humanize-writing
description: >-
  Detect and remove "AI tells" from prose. Supports EN, 中文, ES, AR, PT, 한국어.
  NOT a detector-bypass tool.
---

# humanize-writing

Remove the machine fingerprint from text while keeping meaning 100% intact.

## When this triggers
"humanize", "de-slop", "remove AI tells", "make it sound human", "AI 티 없애줘". One sentence is enough.

## The 4 principles
1. **Intent invariant** — facts, numbers, proper nouns, direct quotes preserved exactly.
2. **Evidence-based** — edit only flagged spans. Leave clean spans alone.
3. **Genre stays** — don't turn a report into an essay.
4. **No over-editing** — warn >30%, hard-stop >50%, ask the user.

## Loop
1. **Detect.** Auto-detect the input language. Always read `taxonomy.md` (universal structural tells W-D through W-L plus English W-A through W-C). If a language-specific file is uploaded, also read it:
   - Korean → `taxonomy-ko.md`
   - Chinese → `taxonomy-zh.md`
   - Spanish → `taxonomy-es.md`
   - Arabic → `taxonomy-ar.md`
   - Portuguese → `taxonomy-pt.md`

   Produce a span-level JSON report (id · severity · span · text · fix_direction) plus metrics.

2. **Repair.** Read `playbook.md`. Apply the smallest edit that removes each tell. Track change-rate.

3. **Verify (parallel).**
   - *Fidelity:* did every fact / number / proper noun / quote survive?
   - *Naturalness:* re-run detection. Residual S1s? Over-editing signals?

4. **Grade & decide.** A → ship. B → ship with notes. C → second pass (max 3). D → human review.

## Do-NOT touch
Numbers · units · dates · proper nouns · names · product/model names · text inside direct quotes · legal/regulatory wording · necessary technical terms.

## Output
- cleaned text
- short diff of most important changes (before → after)
- grade (A/B/C/D) + residual tells
