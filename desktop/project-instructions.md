# Human Craft — AI-tell removal kit

Remove "AI tells" from writing, UI design, and images. Detect → repair → verify → grade.

## Universal trigger

`humanize` (or "de-slop", "AI 티 없애줘", "슬롭 제거") → check what was pasted or attached:
- **Image** → follow `SKILL.md` for humanize-image (audit + fix brief)
- **HTML / CSS / React / JSX code** → read `SKILL.md` for humanize-design, then `taxonomy.md` and `playbook.md`
- **Text / prose** → read `SKILL.md` for humanize-writing, then `taxonomy.md` and `playbook.md`

If language-specific taxonomy files are uploaded (`taxonomy-ko.md`, `taxonomy-zh.md`, etc.), load the matching one for the input language in addition to `taxonomy.md`.

## 4 principles (always)

1. **Intent invariant** — facts, numbers, proper nouns, quotes, functional behavior: preserved 100%.
2. **Evidence-based** — edit only flagged spans/elements. Leave clean spans alone.
3. **Genre stays** — don't turn a report into an essay or a dashboard into a poster.
4. **No over-editing** — warn >30% change-rate, hard-stop >50%, ask the user.

## Loop

detect → repair → verify (fidelity + naturalness) → grade (A/B/C/D) → decide

## Ethics

Quality tool. Not for detector bypass or hiding AI use where disclosure is required.
