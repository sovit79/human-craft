# Multi-AI Platform Support + Multilingual Writing Packs — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Add platform entry files for Codex, Gemini CLI, Copilot, and Cursor; add Korean, Chinese, Spanish, Arabic, and Portuguese writing AI-tell taxonomy files; update README for multi-AI and multilingual quickstart.

**Architecture:** Reference approach — `.claude/skills/` stays the single source of truth. Each platform file routes intent and tells the AI which skill file to read; no content duplication. Language packs live under `references/lang/{code}/` and extend the existing taxonomy schema.

**Tech Stack:** Markdown only. No build step, no tests to run. Verification = file existence + key section presence checks via PowerShell.

---

## File map

| Action | Path |
|---|---|
| Create | `AGENTS.md` |
| Create | `GEMINI.md` |
| Create | `.github/copilot-instructions.md` |
| Create | `.cursorrules` |
| Modify | `.claude/skills/humanize-writing/SKILL.md` |
| Create | `.claude/skills/humanize-writing/references/lang/zh/ai-tell-taxonomy.md` |
| Create | `.claude/skills/humanize-writing/references/lang/es/ai-tell-taxonomy.md` |
| Create | `.claude/skills/humanize-writing/references/lang/ar/ai-tell-taxonomy.md` |
| Create | `.claude/skills/humanize-writing/references/lang/pt/ai-tell-taxonomy.md` |
| Create | `.claude/skills/humanize-writing/references/lang/ko/ai-tell-taxonomy.md` |
| Modify | `README.md` |

---

## Task 1: Create platform entry files

**Files:**
- Create: `AGENTS.md`
- Create: `GEMINI.md`
- Create: `.github/copilot-instructions.md`
- Create: `.cursorrules`

All four files share the same skeleton. Platform-specific notes are called out in each step.

- [ ] **Step 1: Create AGENTS.md**

```markdown
# Human Craft — AI-tell removal kit

Human Craft removes "AI tells" from writing, UI design, and images, preserving meaning and intent
while eliminating the machine fingerprint. Three skills, one loop: detect → repair → verify → grade.

> **OpenAI Codex:** this file is loaded automatically before any task. A global override can live at
> `~/.codex/AGENTS.md`; repo-level (this file) applies to all contributors; subdirectory files
> override for specific parts of the codebase.

## Intent routing

Detect user intent and **read the relevant skill file before doing anything else.**

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
```

- [ ] **Step 2: Create GEMINI.md**

```markdown
# Human Craft — AI-tell removal kit

Human Craft removes "AI tells" from writing, UI design, and images, preserving meaning and intent
while eliminating the machine fingerprint. Three skills, one loop: detect → repair → verify → grade.

> **Gemini CLI:** this file is loaded as context for every prompt. Note: Gemini supports `@file.md`
> import syntax to embed file contents eagerly. This repo intentionally does NOT use that here —
> skill files are read on demand via your file-read tool so only the relevant skill loads per task.

## Intent routing

Detect user intent and **read the relevant skill file before doing anything else** using your
file-read tool.

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
```

- [ ] **Step 3: Create .github/copilot-instructions.md**

Create the `.github/` directory if it doesn't exist, then write the file.

```markdown
# Human Craft — AI-tell removal kit

Human Craft removes "AI tells" from writing, UI design, and images, preserving meaning and intent
while eliminating the machine fingerprint. Three skills, one loop: detect → repair → verify → grade.

> **GitHub Copilot:** these instructions are scoped to this repository via the `.github/` placement.

## Intent routing

Detect user intent and **read the relevant skill file before doing anything else.**

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
```

- [ ] **Step 4: Create .cursorrules**

```markdown
# Human Craft — AI-tell removal kit

Human Craft removes "AI tells" from writing, UI design, and images, preserving meaning and intent
while eliminating the machine fingerprint. Three skills, one loop: detect → repair → verify → grade.

> **Cursor / Windsurf:** this file is injected into the system prompt for every Composer, Chat, and
> inline edit request in this project.

## Intent routing

Detect user intent and **read the relevant skill file before doing anything else.**

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
```

- [ ] **Step 5: Verify all 4 files exist**

```powershell
Test-Path AGENTS.md, GEMINI.md, .github\copilot-instructions.md, .cursorrules
```

Expected: four `True` values.

Also spot-check that each file contains the routing table:

```powershell
Select-String "humanize-writing/SKILL.md" AGENTS.md, GEMINI.md, .github\copilot-instructions.md, .cursorrules
```

Expected: 4 matches.

- [ ] **Step 6: Commit**

```bash
git add AGENTS.md GEMINI.md .github/copilot-instructions.md .cursorrules
git commit -m "feat: add platform entry files for Codex, Gemini CLI, Copilot, Cursor"
```

---

## Task 2: Update SKILL.md with language detection

**Files:**
- Modify: `.claude/skills/humanize-writing/SKILL.md`

The current detect step reads only `references/ai-tell-taxonomy.md`. Replace it with a language-aware version.

- [ ] **Step 1: Open the file and locate the detect step**

Read `.claude/skills/humanize-writing/SKILL.md`. Find this block (around line 26):

```
1. **Detect.** Read `references/ai-tell-taxonomy.md`. Produce a span-level JSON report
   (id · severity · span · text · fix_direction) plus metrics (sentence-length CV, triple count,
   sentence-initial connectives, decorative emoji count).
```

- [ ] **Step 2: Replace the detect step with the language-aware version**

Replace the block above with:

```markdown
1. **Detect.** Auto-detect the input language. Load taxonomy files in this order:
   - Always load: `references/ai-tell-taxonomy.md` (universal structural tells W-D through W-L,
     plus English vocabulary/phrase tells W-A through W-C).
   - Load the language-specific pack if the input is in a supported language:

     | Language | Pack file |
     |---|---|
     | Chinese (Simplified) 中文 | `references/lang/zh/ai-tell-taxonomy.md` |
     | Spanish Español | `references/lang/es/ai-tell-taxonomy.md` |
     | Arabic العربية | `references/lang/ar/ai-tell-taxonomy.md` |
     | Portuguese Português | `references/lang/pt/ai-tell-taxonomy.md` |
     | Korean 한국어 | `references/lang/ko/ai-tell-taxonomy.md` |

   - Other languages: apply universal tells (W-D through W-L) only. Note in output that no
     language pack is available yet — contributions welcome via `CONTRIBUTING.md`.

   Produce a span-level JSON report (id · severity · span · text · fix_direction) plus metrics
   (sentence-length CV, triple count, sentence-initial connectives, decorative emoji count).
```

Also update the description frontmatter line `English-first; preserves meaning` to reflect multilingual support. Replace:

```
  Detect and remove "AI tells" from prose so it reads as deliberate human craft, not the default
  output of a chat model. Use whenever the user pastes AI-generated or AI-assisted text and asks to
  "de-slop", "remove AI tells", "make it sound human / human-written", "kill the ChatGPT voice",
  "humanize this draft", or "fix the AI writing". English-first; preserves meaning, facts, quotes,
  and genre. NOT a detector-bypass tool — see docs/ethics.md.
```

with:

```
  Detect and remove "AI tells" from prose so it reads as deliberate human craft, not the default
  output of a chat model. Use whenever the user pastes AI-generated or AI-assisted text and asks to
  "de-slop", "remove AI tells", "make it sound human / human-written", "kill the ChatGPT voice",
  "humanize this draft", or "fix the AI writing". Supports English, 中文, Español, العربية,
  Português, 한국어; language-agnostic engine for all others. Preserves meaning, facts, quotes,
  and genre. NOT a detector-bypass tool — see docs/ethics.md.
```

Also update the `## When this triggers` line to note multilingual support. After the existing trigger phrase list, add:

```markdown
Works in any language; language-specific AI-tell patterns load automatically for Chinese (中文),
Spanish (Español), Arabic (العربية), Portuguese (Português), and Korean (한국어).
```

- [ ] **Step 3: Verify the change**

```powershell
Select-String "lang/zh" ".claude\skills\humanize-writing\SKILL.md"
```

Expected: one match showing the zh table row.

- [ ] **Step 4: Commit**

```bash
git add .claude/skills/humanize-writing/SKILL.md
git commit -m "feat(writing): add multilingual language detection to SKILL.md"
```

---

## Task 3: Create Chinese (zh) writing taxonomy

**Files:**
- Create: `.claude/skills/humanize-writing/references/lang/zh/ai-tell-taxonomy.md`

- [ ] **Step 1: Create directory and write file**

```markdown
# Writing AI-tell taxonomy — Chinese Simplified (中文简体)

Language-specific extension for `humanize-writing`. Load **after** the universal taxonomy
(`references/ai-tell-taxonomy.md`). The universal tells (W-D through W-L) apply to Chinese prose
too — this file adds Chinese-specific vocabulary, opener, antithesis, connective, and conclusion tells.

> Source: cross-checked against AI-generated Chinese content samples (2025–2026), public analysis
> of ChatGPT Chinese output patterns, and the "AI写作特征" research community findings.

---

## ZH-A · Vocabulary tells (词汇特征)

Words that Chinese LLMs reach for by default across every topic.

| Severity | Examples |
|---|---|
| S2 | 值得注意的是 (it's worth noting), 不可否认 (undeniably), 尤为重要 (particularly important), 至关重要 (crucial/pivotal), 举足轻重 (play a key role), 彰显 (showcase/demonstrate), 赋能 (empower), 助力 (empower/facilitate), 赋予 (endow/give), 深度 (in-depth, as empty modifier) |
| S3 | 诸多 (numerous), 各方面 (various aspects), 全方位 (all-round), 多维度 (multi-dimensional) |

**Fix:** use concrete, specific words. 至关重要 → "决定性的" or just say why it matters.
赋能 → describe the actual mechanism. 彰显 → say plainly what it shows.

---

## ZH-B · Stock openers (套话开头)

| Severity | Examples |
|---|---|
| S1 | "在当今社会/时代，…" (In today's society/era…), "随着社会的不断发展，…" (As society continues to develop…), "在全球化的今天，…" (In today's globalized world…) |
| S2 | "首先，我们需要了解…" (First, we need to understand…), "让我们一起探讨…" (Let's explore together…), "毋庸置疑，…" (There is no doubt that…) |

**Fix:** start on the first real idea. Delete the runway sentence entirely.

---

## ZH-C · "不只是X，更是Y" antithesis structure

| Severity | Pattern |
|---|---|
| **S1** | "这不仅仅是一种工具，更是一种理念" (This is not just a tool, it's a philosophy) |
| **S1** | "不是…而是…" used as the primary sentence structure instead of a one-time contrast |

The Chinese form of the English "It's not just X, it's Y" construction. One occurrence reads as AI.

**Fix:** state the actual claim directly. If both halves matter, use "它既是X，也是Y" (it is both X and Y).

---

## ZH-D · Connective overuse (连接词滥用)

| Severity | Pattern |
|---|---|
| **S1** | 首先/其次/再次/最后 or 第一/第二/第三/第四 as paragraph openers across 3+ consecutive paragraphs |
| S2 | 此外/另外/除此之外/与此同时/值得一提的是 used as sentence-initial connectives throughout |
| S2 | 然而/但是/不过 alternating reflexively to simulate "balance" |

**Fix:** delete the connector and let the idea stand alone, or use "和/也/但" (plain conjunctions).

---

## ZH-E · Conclusion tells (结论套话)

| Severity | Pattern |
|---|---|
| S2 | "综上所述" (In summary), "总而言之" (All in all), "由此可见" (It can thus be seen) |
| S2 | "总结" / "小结" section at the end of every paragraph |
| S1 | A tidy moral or takeaway sentence ending every section: "这正是X的价值所在" (This is exactly where the value of X lies) |

**Fix:** good endings stop. Delete the label. Often delete the summary sentence entirely.

---

## Detector output format

Use the same JSON format as the universal taxonomy, with ZH-prefixed IDs:

```json
{
  "findings": [
    {
      "id": "ZH-C",
      "severity": "S1",
      "span": {"start": 140, "end": 188},
      "text": "这不仅仅是一个产品，更是一种生活方式",
      "note": "不只是X更是Y antithesis construction",
      "fix_direction": "直接陈述核心主张，删除对比结构"
    }
  ]
}
```

---

## Versioning

Candidates at the bottom with ≥2 real examples, proposed severity and fix direction.

### Candidates (unpromoted)
- *"无论是X还是Y，都…" (Whether X or Y, both…) as a reflexive hedging opener* — needs examples.
- *过度使用"探索" (explore) 和"洞察" (insight) as filler nouns* — needs examples.
```

- [ ] **Step 2: Verify**

```powershell
Test-Path ".claude\skills\humanize-writing\references\lang\zh\ai-tell-taxonomy.md"
Select-String "ZH-C" ".claude\skills\humanize-writing\references\lang\zh\ai-tell-taxonomy.md"
```

Expected: `True` then one match.

- [ ] **Step 3: Commit**

```bash
git add .claude/skills/humanize-writing/references/lang/zh/
git commit -m "feat(writing/lang): add Simplified Chinese AI-tell taxonomy (ZH-A through ZH-E)"
```

---

## Task 4: Create Spanish (es) writing taxonomy

**Files:**
- Create: `.claude/skills/humanize-writing/references/lang/es/ai-tell-taxonomy.md`

- [ ] **Step 1: Write file**

```markdown
# Writing AI-tell taxonomy — Spanish (Español)

Language-specific extension for `humanize-writing`. Load **after** the universal taxonomy
(`references/ai-tell-taxonomy.md`). Universal tells (W-D through W-L) apply to Spanish prose too.

> Source: cross-checked against AI-generated Spanish content (2025–2026) from ChatGPT, Gemini, and
> Claude outputs in Spanish; "marcadores del texto de IA en español" analysis.

---

## ES-A · Vocabulary tells (léxico característico)

| Severity | Examples |
|---|---|
| S2 | crucial (crucial/pivotal), fundamental (fundamental/key), esencial (essential), implementar (implement), optimizar (optimize), potenciar (enhance/leverage), robusto (robust), agilizar (streamline), empoderar (empower), aprovechar (leverage) |
| S3 | paradigma (paradigm), sinergia (synergy), holístico (holistic), ecosistema (ecosystem, non-biological) |

**Fix:** use the word you'd say out loud. "crucial" → "importante" or "clave"; "implementar" → "aplicar / poner en práctica"; "robusto" → "sólido / fiable".

---

## ES-B · Stock openers (frases de apertura)

| Severity | Examples |
|---|---|
| S1 | "En el mundo actual / En el panorama actual…" (In today's world / In the current landscape…), "En la era digital / En la era de la IA…" (In the digital/AI age…), "En un mundo en constante cambio…" (In a constantly changing world…) |
| S2 | "Es importante destacar que…" (It's important to highlight that…), "Cabe mencionar que…" (It's worth mentioning that…), "Vale la pena señalar que…" (It's worth pointing out that…), "No cabe duda de que…" (There is no doubt that…) |

**Fix:** start on the first real idea. The opener is always filler.

---

## ES-C · "No se trata solo de X, sino de Y" antithesis

| Severity | Pattern |
|---|---|
| **S1** | "No se trata solo de una herramienta, sino de una forma de vida" (It's not just a tool, it's a way of life) |
| **S1** | "No es solo X — es Y" used as the primary rhetorical move |

**Fix:** state the claim directly. If both halves matter: "Es una herramienta que también define un estilo de vida."

---

## ES-D · Connective overuse (conectores en exceso)

| Severity | Pattern |
|---|---|
| **S1** | En primer lugar / En segundo lugar / En tercer lugar / Finalmente / Por último stacked across 3+ consecutive paragraphs |
| S2 | Asimismo, Por otro lado, Sin embargo, No obstante, Además, Por su parte — used sentence-initially throughout as the default transition |
| S2 | "Es importante mencionar que" / "Es fundamental destacar que" as filler intros to every new point |

**Fix:** delete the connector. Use "y / pero / así" or just a new sentence. One "sin embargo" earns its place; five don't.

---

## ES-E · Conclusion tells (frases de cierre)

| Severity | Pattern |
|---|---|
| S2 | "En conclusión", "En resumen", "Para concluir", "En definitiva", "A modo de conclusión" |
| S1 | A wrap-up moral closing every section: "Esto demuestra la importancia de X en nuestra sociedad" |

**Fix:** end on the last real point. Delete the label.

---

## Detector output format

```json
{
  "findings": [
    {
      "id": "ES-B",
      "severity": "S1",
      "span": {"start": 0, "end": 32},
      "text": "En el panorama actual, es crucial",
      "note": "stock landscape opener + S2 vocabulary cluster",
      "fix_direction": "start on the first real idea; remove opener entirely"
    }
  ]
}
```

---

## Versioning

### Candidates (unpromoted)
- *Reflexive use of "a nivel" (at the level of) as a filler phrase* — needs examples.
- *"Desde esta perspectiva" as a manufactured pivot* — needs examples.
```

- [ ] **Step 2: Verify**

```powershell
Test-Path ".claude\skills\humanize-writing\references\lang\es\ai-tell-taxonomy.md"
Select-String "ES-C" ".claude\skills\humanize-writing\references\lang\es\ai-tell-taxonomy.md"
```

Expected: `True` then one match.

- [ ] **Step 3: Commit**

```bash
git add .claude/skills/humanize-writing/references/lang/es/
git commit -m "feat(writing/lang): add Spanish AI-tell taxonomy (ES-A through ES-E)"
```

---

## Task 5: Create Arabic (ar) writing taxonomy

**Files:**
- Create: `.claude/skills/humanize-writing/references/lang/ar/ai-tell-taxonomy.md`

- [ ] **Step 1: Write file**

```markdown
# Writing AI-tell taxonomy — Arabic (العربية)

Language-specific extension for `humanize-writing`. Load **after** the universal taxonomy
(`references/ai-tell-taxonomy.md`). Universal tells (W-D through W-L) apply to Arabic prose too.

> Source: cross-checked against AI-generated Arabic content (2025–2026); "علامات الكتابة
> الاصطناعية بالعربية" analysis and Modern Standard Arabic (MSA) register research.

---

## AR-A · Register & vocabulary tells (مؤشرات المفردات والأسلوب)

The strongest Arabic AI signal is excessive use of formal Modern Standard Arabic (MSA) in contexts
where a less formal register (or dialect-adjacent MSA) would be natural.

| Severity | Examples |
|---|---|
| **S1** | فضلاً عن ذلك (furthermore — formal filler), ومن الجدير بالذكر (it is worth noting — extremely formal opener), ولا يخفى على أحد (it's no secret to anyone — rhetorical filler), وتجدر الإشارة إلى أن (it should be noted that) |
| S2 | لا شك أن (there is no doubt that), من المهم أن نلاحظ (it is important to note), يُعدّ من أبرز (is considered one of the most prominent), يكتسب أهمية بالغة (acquires great importance) |
| S3 | ينبغي الإشارة إلى (it should be pointed out), في هذا السياق (in this context — as filler) |

**Fix:** use the register the audience expects. If writing for a general audience, avoid bureaucratic MSA phrases. Replace the filler opener with the actual point.

---

## AR-B · Stock openers (الافتتاحيات النمطية)

| Severity | Examples |
|---|---|
| **S1** | "في عصرنا الحالي / في ظل التطور المتسارع / في زمن العولمة…" (In our current era / amid rapid development / in the age of globalization…) |
| S2 | "يسعدنا أن نستعرض…" (We are pleased to present…), "دعونا نتناول…" (Let us address…), "لا يمكننا إغفال…" (We cannot ignore…) |

**Fix:** start on the first real idea.

---

## AR-C · "ليس فقط… بل أيضاً" antithesis structure

| Severity | Pattern |
|---|---|
| **S1** | "ليس هذا مجرد أداة، بل هو منهج متكامل" (This is not merely a tool, it is an integrated methodology) |
| **S1** | "لا يقتصر الأمر على X، بل يتجاوزه إلى Y" (The matter is not limited to X, it goes beyond to Y) as the primary rhetorical move |

**Fix:** state the claim directly. "هو أداة تعكس منهجاً" (It is a tool that reflects a methodology) — pick the core claim and state it.

---

## AR-D · Connective overuse (الإفراط في روابط الجمل)

| Severity | Pattern |
|---|---|
| **S1** | أولاً / ثانياً / ثالثاً / رابعاً stacked as paragraph openers across 3+ paragraphs |
| S2 | وأيضاً / وكذلك / وعلاوة على ذلك / فضلاً عن ذلك / إضافةً إلى ذلك repeating throughout as sentence starters |
| S2 | من ناحية أخرى / في المقابل / بالمقارنة مع used reflexively to simulate balance |

**Fix:** delete the connector. Arabic prose flows naturally without dense explicit connectives — trust the reader to follow logical sequence.

---

## AR-E · Conclusion tells (الخواتيم النمطية)

| Severity | Pattern |
|---|---|
| S2 | "خلاصة القول" (In summary), "وفي الختام" (In conclusion), "مما سبق يتضح أن" (From the above it is clear that), "يمكن القول إجمالاً" (It can be said in general) |
| S1 | A moral/takeaway sentence closing every section: "وهذا ما يجعل X ضرورةً لا غنى عنها" (And this is what makes X an indispensable necessity) |

**Fix:** end on the last real point. Delete the label.

---

## Detector output format

```json
{
  "findings": [
    {
      "id": "AR-A",
      "severity": "S1",
      "span": {"start": 0, "end": 24},
      "text": "ومن الجدير بالذكر أن",
      "note": "extremely formal MSA filler opener",
      "fix_direction": "start on the actual point; delete the opener"
    }
  ]
}
```

---

## Versioning

### Candidates (unpromoted)
- *"على الصعيد" (on the level of) as a vague scope-setting filler* — needs examples.
- *Excessive use of broken plural forms for effect rather than necessity* — needs examples.
```

- [ ] **Step 2: Verify**

```powershell
Test-Path ".claude\skills\humanize-writing\references\lang\ar\ai-tell-taxonomy.md"
Select-String "AR-C" ".claude\skills\humanize-writing\references\lang\ar\ai-tell-taxonomy.md"
```

Expected: `True` then one match.

- [ ] **Step 3: Commit**

```bash
git add .claude/skills/humanize-writing/references/lang/ar/
git commit -m "feat(writing/lang): add Arabic AI-tell taxonomy (AR-A through AR-E)"
```

---

## Task 6: Create Portuguese / Brazilian (pt) writing taxonomy

**Files:**
- Create: `.claude/skills/humanize-writing/references/lang/pt/ai-tell-taxonomy.md`

- [ ] **Step 1: Write file**

```markdown
# Writing AI-tell taxonomy — Portuguese / Brazilian (Português / Português Brasileiro)

Language-specific extension for `humanize-writing`. Load **after** the universal taxonomy
(`references/ai-tell-taxonomy.md`). Universal tells (W-D through W-L) apply to Portuguese prose too.

> Brazilian Portuguese is the primary target (largest user base); EU-PT notes marked explicitly.
> Source: cross-checked against AI-generated Brazilian Portuguese content (2025–2026), "marcadores
> de texto gerado por IA em português" analysis.

---

## PT-A · Vocabulary tells (vocabulário característico)

| Severity | Examples |
|---|---|
| S2 | crucial (crucial/pivotal), fundamental (fundamental/key), implementar (implement), otimizar (optimize), alavancar (leverage), robusto (robust), nortear (to guide/steer — overused as metaphor), impulsionar (drive/boost), fomentar (foster), capacitar (empower) |
| S3 | paradigma (paradigm), sinérgico (synergistic), holístico (holistic), ecossistema (ecosystem, non-biological) |

**Fix:** use plain spoken Portuguese. "crucial" → "importante" / "decisivo"; "alavancar" → "usar" / "aproveitar"; "fomentar" → "incentivar".

---

## PT-B · Stock openers (aberturas padrão)

| Severity | Examples |
|---|---|
| **S1** | "No cenário atual / No mundo contemporâneo / No contexto atual…" (In the current scenario / contemporary world…), "Em um mundo em constante transformação…" (In a world in constant transformation…), "Na era digital / Na era da inteligência artificial…" (In the digital/AI age…) |
| S2 | "Vale ressaltar que…" (It's worth emphasizing that…), "Cabe destacar que…" (It's worth highlighting that…), "É importante mencionar que…" (It's important to mention that…), "É fundamental compreender que…" (It's fundamental to understand that…) |

**Fix:** start on the first real idea. Delete the opener.

---

## PT-C · "Não se trata apenas de X, mas de Y" antithesis

| Severity | Pattern |
|---|---|
| **S1** | "Não se trata apenas de uma ferramenta, mas de uma transformação" (It's not just a tool, it's a transformation) |
| **S1** | "Não é só X — é Y" as the primary rhetorical construction |

**Fix:** state the core claim directly. "É uma ferramenta que transforma o fluxo de trabalho."

---

## PT-D · Connective overuse (conectivos em excesso)

| Severity | Pattern |
|---|---|
| **S1** | Em primeiro lugar / Em segundo lugar / Em terceiro lugar / Por fim / Por último stacked across 3+ paragraphs |
| S2 | Além disso, No entanto, Portanto, Sendo assim, Dessa forma, Nesse sentido — used sentence-initially throughout |
| S2 | "É válido ressaltar que" / "É pertinente destacar que" as filler intros to every new point |

**Fix:** delete the connector. Use "e / mas / então" or just a new sentence.

---

## PT-E · EU vs. Brazilian Portuguese mixing (mistura de registros)

AI models often mix European Portuguese lexicon into Brazilian Portuguese content.

| Severity | Pattern |
|---|---|
| S2 | "utilizador" (EU) instead of "usuário" (BR); "telemóvel" (EU) instead of "celular" (BR); "autocarro" (EU) instead of "ônibus" (BR); "ecrã" (EU) instead of "tela" (BR) |
| S2 | EU verb forms and spellings leaking into BR text (e.g. "óptimo" instead of "ótimo", "acção" instead of "ação") |

**Fix:** pick one register and be consistent. For BR audiences, use BR lexicon throughout.

---

## PT-F · Conclusion tells (frases de encerramento)

| Severity | Pattern |
|---|---|
| S2 | "Em conclusão", "Em suma", "Sendo assim", "Portanto", "Em síntese", "Para finalizar" |
| **S1** | A wrap-up moral ending every section: "Isso demonstra a importância de X para o futuro" |

**Fix:** end on the last real point. Delete the label.

---

## Detector output format

```json
{
  "findings": [
    {
      "id": "PT-B",
      "severity": "S1",
      "span": {"start": 0, "end": 31},
      "text": "No cenário atual, é fundamental",
      "note": "stock landscape opener + S2 vocabulary",
      "fix_direction": "start on the first real idea; remove opener"
    }
  ]
}
```

---

## Versioning

### Candidates (unpromoted)
- *"A nível de" (at the level of) as vague scope filler* — needs examples.
- *"Num mundo cada vez mais" (In an increasingly X world) opener variations* — needs examples.
```

- [ ] **Step 2: Verify**

```powershell
Test-Path ".claude\skills\humanize-writing\references\lang\pt\ai-tell-taxonomy.md"
Select-String "PT-E" ".claude\skills\humanize-writing\references\lang\pt\ai-tell-taxonomy.md"
```

Expected: `True` then one match.

- [ ] **Step 3: Commit**

```bash
git add .claude/skills/humanize-writing/references/lang/pt/
git commit -m "feat(writing/lang): add Portuguese/Brazilian AI-tell taxonomy (PT-A through PT-F)"
```

---

## Task 7: Create Korean (ko) writing taxonomy

**Files:**
- Create: `.claude/skills/humanize-writing/references/lang/ko/ai-tell-taxonomy.md`

- [ ] **Step 1: Write file**

```markdown
# Writing AI-tell taxonomy — Korean (한국어)

Language-specific extension for `humanize-writing`. Load **after** the universal taxonomy
(`references/ai-tell-taxonomy.md`). Universal tells (W-D through W-L) apply to Korean prose too.

> Credits: patterns sourced and cross-checked against epoko77-ai/im-not-ai (Korean-specialized
> writing humanizer), public "AI 글쓰기 특징" analysis (2025–2026), and real ChatGPT/Claude
> Korean output samples. Korean AI tells are dominated by English-to-Korean translationese and
> excessive formal register.

---

## KO-A · Vocabulary tells (어휘 특징)

Words Korean LLMs reach for by default. Many are transliterated English or overly formal Chinese-
character compounds that would feel stiff in natural spoken Korean writing.

| Severity | Examples |
|---|---|
| **S1** | 다양한 (various/diverse — massively overused as an empty modifier before any noun), 효과적인 (effective — used reflexively), 중요한 (important — attached to every claim), 필요한 (necessary — reflexive qualifier) |
| S2 | 탐색하다 (explore/navigate), 활용하다 (utilize/leverage — 쓰다/사용하다 is natural), 구현하다 (implement), 최적화하다 (optimize), 향상시키다 (enhance/elevate), 고려하다 (consider — reflexive hedging), 제공하다 (provide — overused as default verb) |
| S3 | 패러다임 (paradigm), 시너지 (synergy), 홀리스틱 (holistic), 에코시스템 (ecosystem) |

**Fix:** drop the empty modifier entirely (다양한 before a noun that speaks for itself), or replace with the specific word you'd say out loud. 활용하다 → 쓰다/사용하다. 향상시키다 → 높이다/나아지다.

---

## KO-B · Translationese openers (번역체 도입부)

| Severity | Examples |
|---|---|
| **S1** | "오늘날의 빠르게 변화하는 세상에서…" (In today's fast-changing world…), "현대 사회에서…" (In modern society…), "4차 산업혁명 시대에…" (In the era of the 4th Industrial Revolution…), "디지털 전환의 시대에…" (In the age of digital transformation…) |
| S2 | "주목할 만한 점은…" (What's worth noting is…), "중요한 것은…" (What's important is…), "간과할 수 없는 사실은…" (A fact we cannot overlook is…) |

**Fix:** start on the first real idea. The opener is always filler.

---

## KO-C · "단순한 X가 아니라 Y" antithesis (부정 대조 구조)

| Severity | Pattern |
|---|---|
| **S1** | "이것은 단순한 도구가 아니라 하나의 철학입니다" (This is not just a tool, it's a philosophy) |
| **S1** | "X뿐만 아니라 Y도 중요합니다" used as the *primary* construction in every paragraph rather than once |

**Fix:** 핵심 주장을 직접 말한다. "이 도구는 팀의 업무 방식을 바꿉니다." Choose the one true claim.

---

## KO-D · Connective overuse (접속어 남발)

| Severity | Pattern |
|---|---|
| **S1** | 첫째/둘째/셋째/넷째 or 첫번째/두번째/세번째 stacked across 3+ consecutive paragraphs |
| S2 | 또한 / 그러나 / 따라서 / 더불어 / 이와 함께 / 아울러 used as sentence starters throughout |
| S2 | "이처럼" / "이를 통해" / "이러한 관점에서" repeating as manufactured transitions |

**Fix:** delete the connector. 또한 → 그냥 다음 문장. 따라서 → "그래서" or nothing. Read aloud — if every paragraph starts with a connector, it sounds mechanical.

---

## KO-E · Formal ending overuse in casual context (어미 과잉 격식체)

| Severity | Pattern |
|---|---|
| S2 | Exclusive use of ~습니다/~입니다 throughout text meant for a general or informal audience where ~요 endings would be natural |
| S2 | "~하는 것이 중요합니다" / "~할 필요가 있습니다" / "~해야 합니다" as the default sentence ending for every claim |
| S2 | Excessive nominalization: verb → ~하는 것/~함 construction where the verb alone would read naturally |

**Fix:** match the register to the audience. For general writing, mixing ~요 endings reads human. Vary sentence-ending patterns: declarative, question, brief command.

---

## KO-F · Conclusion tells (결론 상투어)

| Severity | Pattern |
|---|---|
| S2 | "결론적으로", "정리하면", "요약하자면", "마지막으로", "종합해보면" |
| **S1** | A wrap-up moral sentence closing every section: "이것이 바로 X가 중요한 이유입니다" (This is exactly why X is important) |

**Fix:** end on the last real point. Delete the label sentence.

---

## Detector output format

```json
{
  "findings": [
    {
      "id": "KO-A",
      "severity": "S1",
      "span": {"start": 8, "end": 12},
      "text": "다양한",
      "note": "empty modifier — appears 7 times in this text",
      "fix_direction": "delete or replace with specific descriptor"
    }
  ]
}
```

---

## Versioning

### Candidates (unpromoted)
- *"~라고 할 수 있습니다" (it can be said that) as a reflexive hedge on every claim* — needs examples.
- *"글로벌" / "로컬" as empty scope qualifiers* — needs examples.
```

- [ ] **Step 2: Verify**

```powershell
Test-Path ".claude\skills\humanize-writing\references\lang\ko\ai-tell-taxonomy.md"
Select-String "KO-A" ".claude\skills\humanize-writing\references\lang\ko\ai-tell-taxonomy.md"
```

Expected: `True` then one match.

- [ ] **Step 3: Commit**

```bash
git add .claude/skills/humanize-writing/references/lang/ko/
git commit -m "feat(writing/lang): add Korean AI-tell taxonomy (KO-A through KO-F)"
```

---

## Task 8: Update README.md

**Files:**
- Modify: `README.md`

Four targeted edits. Make them in order.

- [ ] **Step 1: Update the badge line**

Find this line near the top of README.md:

```markdown
[![Claude Code](https://img.shields.io/badge/Built%20for-Claude%20Code-7C5CFF.svg)](https://claude.com/claude-code)
```

Replace with:

```markdown
[![Claude Code](https://img.shields.io/badge/Built%20for-Claude%20Code-7C5CFF.svg)](https://claude.com/claude-code)
[![Multi-AI](https://img.shields.io/badge/Also%20works%20in-Codex%20%7C%20Gemini%20%7C%20Copilot%20%7C%20Cursor-4A90D9.svg)](#ai-platform-support)
```

- [ ] **Step 2: Update the "Three skills" table to add language support column**

Find the table:

```markdown
| Skill | What it cleans | Reference taxonomy |
|---|---|---|
| `humanize-writing` | Prose, posts, docs, emails — English-first, language-agnostic engine | [taxonomy](.claude/skills/humanize-writing/references/ai-tell-taxonomy.md) |
| `humanize-design` | Web/UI, landing pages, slide decks, HTML/CSS/React | [taxonomy](.claude/skills/humanize-design/references/design-slop-taxonomy.md) |
| `humanize-image` | Generated illustrations & photos — audit + fix brief | [taxonomy](.claude/skills/humanize-image/references/image-tell-taxonomy.md) |
```

Replace with:

```markdown
| Skill | What it cleans | Languages | Reference taxonomy |
|---|---|---|---|
| `humanize-writing` | Prose, posts, docs, emails | EN · 中文 · ES · AR · PT · 한국어 · any (universal tells) | [taxonomy](.claude/skills/humanize-writing/references/ai-tell-taxonomy.md) |
| `humanize-design` | Web/UI, landing pages, slide decks, HTML/CSS/React | Language-agnostic | [taxonomy](.claude/skills/humanize-design/references/design-slop-taxonomy.md) |
| `humanize-image` | Generated illustrations & photos — audit + fix brief | Language-agnostic | [taxonomy](.claude/skills/humanize-image/references/image-tell-taxonomy.md) |
```

- [ ] **Step 3: Add "AI platform support" section**

Find the line `## Quickstart (≈5 minutes)` and insert this section **before** it:

```markdown
## AI platform support

Human Craft works in Claude Code (native), and in any AI platform that reads the repo's entry file
before answering. The skill content lives in `.claude/skills/` — all platforms read from there.

| Platform | Entry file | Launch |
|---|---|---|
| [Claude Code](https://claude.com/claude-code) | `CLAUDE.md` + `.claude/skills/` | `claude` inside this folder |
| OpenAI Codex | `AGENTS.md` | `codex` inside this folder |
| Gemini CLI | `GEMINI.md` | `gemini` inside this folder |
| GitHub Copilot | `.github/copilot-instructions.md` | open in VS Code with Copilot enabled |
| Cursor / Windsurf | `.cursorrules` | open this folder in Cursor |

All platforms use the same trigger phrases — one natural sentence is enough regardless of which AI you're using.

---

```

- [ ] **Step 4: Update the Quickstart "Prerequisite" section**

Find:

```markdown
### 0. Prerequisite

You need [Claude Code](https://claude.com/claude-code) installed (Mac / Windows / Linux).

```bash
claude --version
```
```

Replace with:

```markdown
### 0. Prerequisite

Choose your AI platform. Claude Code is the reference implementation; all others work too.

**Claude Code** (reference)
```bash
claude --version
```

**OpenAI Codex**
```bash
codex --version
```

**Gemini CLI**
```bash
gemini --version
```

**Cursor / Windsurf / GitHub Copilot:** open this folder in your IDE.

```

- [ ] **Step 5: Verify**

```powershell
Select-String "AI platform support" README.md
Select-String "EN · 中文 · ES · AR · PT · 한국어" README.md
Select-String "AGENTS.md" README.md
```

Expected: three matches.

- [ ] **Step 6: Commit**

```bash
git add README.md
git commit -m "docs: update README for multi-AI platform support and multilingual writing"
```

---

## Final verification

- [ ] **Check all expected files exist**

```powershell
$files = @(
  "AGENTS.md", "GEMINI.md", ".cursorrules",
  ".github\copilot-instructions.md",
  ".claude\skills\humanize-writing\references\lang\zh\ai-tell-taxonomy.md",
  ".claude\skills\humanize-writing\references\lang\es\ai-tell-taxonomy.md",
  ".claude\skills\humanize-writing\references\lang\ar\ai-tell-taxonomy.md",
  ".claude\skills\humanize-writing\references\lang\pt\ai-tell-taxonomy.md",
  ".claude\skills\humanize-writing\references\lang\ko\ai-tell-taxonomy.md"
)
$files | ForEach-Object { [PSCustomObject]@{ File = $_; Exists = (Test-Path $_) } } | Format-Table
```

Expected: all `Exists` values are `True`.

- [ ] **Check lang taxonomy IDs present**

```powershell
"ZH-C","ES-C","AR-C","PT-C","KO-C" | ForEach-Object {
  $id = $_; $lang = $id.Substring(0,2).ToLower()
  $file = ".claude\skills\humanize-writing\references\lang\$lang\ai-tell-taxonomy.md"
  [PSCustomObject]@{ ID = $id; Found = (Select-String $id $file -Quiet) }
} | Format-Table
```

Expected: all `Found` values are `True`.

- [ ] **Check SKILL.md has language detection**

```powershell
Select-String "lang/ko" ".claude\skills\humanize-writing\SKILL.md"
```

Expected: one match.

- [ ] **Check README has platform table**

```powershell
Select-String "AGENTS.md" README.md
```

Expected: one match.
