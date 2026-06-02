# Human Craft — AI-tell removal kit

Human Craft removes "AI tells" from writing, UI design, and images, preserving meaning and intent
while eliminating the machine fingerprint. Three skills, one loop: detect → repair → verify → grade.

> **GitHub Copilot:** these instructions are scoped to this repository via the `.github/` placement.

## Intent routing

Detect user intent and **read the relevant skill file before doing anything else** using your file-read tool to fetch it on demand.

| Trigger phrases | Skill file to read |
|---|---|
| "de-slop", "humanize", "remove AI tells", "AI 티 제거", "make it sound human", "kill the ChatGPT voice" + prose/text | `.claude/skills/humanize-writing/SKILL.md` |
| "de-slop the UI", "looks AI-generated", "kill the AI design look", "humanize this landing page" + HTML/CSS/React/screenshot | `.claude/skills/humanize-design/SKILL.md` |
| "does this look AI?", "audit for AI tells", "give me a fix brief" + image attachment | `.claude/skills/humanize-image/SKILL.md` |

After reading the skill file, follow its loop exactly. The skill file references taxonomy and playbook
files — read those too before detecting or repairing.

## 4 principles (always apply — fallback if skill file is unreadable)

1. **Intent invariant** — facts, numbers, proper nouns, quotes, functional behavior: preserved 100%.
2. **Evidence-based** — edit only flagged spans/elements. Leave clean spans alone.
3. **Genre stays** — don't turn a report into an essay or a dashboard into a poster.
4. **No over-editing** — warn >30% change-rate, hard-stop >50%, ask the user.

## Full loop

detect → repair → verify (fidelity + naturalness, in parallel) → grade (A/B/C/D) → decide
(accept / 2nd pass up to 3 / rollback / hold for human review)

## Ethics

Quality tool. Not for detector bypass or hiding AI use where disclosure is required.
See `docs/ethics.md`.
