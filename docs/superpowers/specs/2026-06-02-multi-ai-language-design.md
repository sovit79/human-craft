# Design: Multi-AI platform support + multilingual writing packs

Date: 2026-06-02  
Status: Approved

## Problem

Human Craft skills live in `.claude/skills/` and `CLAUDE.md` — mechanisms only Claude Code reads. Other AI platforms (OpenAI Codex, Gemini CLI, GitHub Copilot, Cursor) get no instructions. The writing skill is English-only; the repo targets a global audience.

## Goals

1. Make all three skills work in Claude Code, Codex, Gemini CLI, Copilot, and Cursor without moving the single source of truth.
2. Add writing AI-tell taxonomies for the 5 highest-usage languages (Chinese, Spanish, Arabic, Portuguese, Korean).
3. Update README for multi-AI quickstart and multilingual support.

## Non-goals

- Moving `.claude/skills/` to a different location.
- Adding language packs for design or image skills (language-agnostic by nature).
- Full rewriting-playbook per language (inline fix directions in taxonomy are sufficient for v0).

## Architecture

### Approach: Reference (B)

`.claude/skills/` remains the single source of truth. Each platform file tells the AI to read the relevant skill file at runtime. No content duplication.

```
human-craft/
├── CLAUDE.md                              (existing — no change)
├── AGENTS.md                              (new — OpenAI Codex)
├── GEMINI.md                              (new — Gemini CLI)
├── .github/
│   └── copilot-instructions.md            (new — GitHub Copilot)
├── .cursorrules                            (new — Cursor / Windsurf)
├── .claude/skills/humanize-writing/
│   ├── SKILL.md                           (update — add language detection)
│   └── references/
│       ├── ai-tell-taxonomy.md            (existing — English + universal structural)
│       └── lang/
│           ├── zh/ai-tell-taxonomy.md     (new — Simplified Chinese)
│           ├── es/ai-tell-taxonomy.md     (new — Spanish)
│           ├── ar/ai-tell-taxonomy.md     (new — Arabic)
│           ├── pt/ai-tell-taxonomy.md     (new — Portuguese / Brazilian)
│           └── ko/ai-tell-taxonomy.md     (new — Korean)
└── README.md                              (update — multi-AI + multilingual)
```

### Platform files (shared skeleton)

All four platform files follow the same pattern:

1. **Intent routing** — trigger phrases → which skill file to read
2. **Skill load instruction** — explicit path to `.claude/skills/{skill}/SKILL.md`
3. **4 principles inline** — fallback if file read fails
4. **Full loop summary** — detect → repair → verify → grade
5. **Ethics gate** — one line, pointer to `docs/ethics.md`

Platform-specific delta:
- `GEMINI.md`: note that `@file.md` import is available but eager; use file-read tool instead
- `AGENTS.md`: note hierarchical file discovery (global → repo → subdir)
- `.cursorrules`: always injected into system prompt on every request
- `copilot-instructions.md`: scoped to this repo via `.github/` placement

### Language detection in SKILL.md

```
Auto-detect input language.
Load always: references/ai-tell-taxonomy.md  (universal structural tells W-D through W-I)
Load if available: references/lang/{code}/ai-tell-taxonomy.md
  zh → Simplified Chinese
  es → Spanish
  ar → Arabic
  pt → Portuguese (Brazilian)
  ko → Korean
Other language: apply universal tells only; note language pack unavailable.
```

Universal tells that apply to all languages: W-D (rule of three), W-E (connective overuse), W-F (balance/hedging), W-G (conclusion tells), W-H (rhythm uniformity), W-I (structural/formatting), W-J (ornamentation), W-K (assistant voice), W-L (missing human signal).

Language-specific tells: W-A (vocabulary), W-B (stock phrases), W-C ("not just X, it's Y" — has equivalents in each language).

### Language taxonomy structure (per file)

Each `lang/{code}/ai-tell-taxonomy.md` follows the same schema as the English taxonomy:
- ID: `{LANG}-A` through `{LANG}-E` (vocabulary, openers, antithesis structure, connectives, conclusion tells)
- Severity: S1/S2/S3
- Real examples (≥2 per pattern)
- Fix direction

### README changes

- Add "AI platform support" section with platform → file → quickstart table
- Update top badge: add multi-AI badge
- Update "Three skills" table: add language support column
- Keep existing Claude Code quickstart; add platform-specific quickstarts below it
- Update Korean section at bottom to reflect multilingual support

## Files changed / created

| Action | File |
|---|---|
| Create | `AGENTS.md` |
| Create | `GEMINI.md` |
| Create | `.github/copilot-instructions.md` |
| Create | `.cursorrules` |
| Update | `.claude/skills/humanize-writing/SKILL.md` |
| Create | `.claude/skills/humanize-writing/references/lang/zh/ai-tell-taxonomy.md` |
| Create | `.claude/skills/humanize-writing/references/lang/es/ai-tell-taxonomy.md` |
| Create | `.claude/skills/humanize-writing/references/lang/ar/ai-tell-taxonomy.md` |
| Create | `.claude/skills/humanize-writing/references/lang/pt/ai-tell-taxonomy.md` |
| Create | `.claude/skills/humanize-writing/references/lang/ko/ai-tell-taxonomy.md` |
| Update | `README.md` |

## Acceptance criteria

- Claude Code: no behavior change (`.claude/skills/` untouched except SKILL.md language section).
- Codex: `AGENTS.md` present, intent routing correct, skill file paths valid.
- Gemini CLI: `GEMINI.md` present, same routing.
- Copilot: `.github/copilot-instructions.md` present.
- Cursor: `.cursorrules` present.
- Writing skill: auto-detects zh/es/ar/pt/ko and loads correct lang taxonomy.
- Each lang taxonomy: ≥4 ID entries, ≥2 real examples each, severity + fix direction.
- README: multi-AI table present, language support column present.
