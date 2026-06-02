# Human Craft — the AI-tell removal kit

> Make AI-assisted **writing, UI design, and images** read as deliberate human craft —
> not as the statistical "default" a chat model spits out.
> A set of [Claude Code](https://claude.com/claude-code) skills.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Claude Code](https://img.shields.io/badge/Built%20for-Claude%20Code-7C5CFF.svg)](https://claude.com/claude-code)
[![Multi-AI](https://img.shields.io/badge/Also%20works%20in-Codex%20%7C%20Gemini%20%7C%20Copilot%20%7C%20Cursor-4A90D9.svg)](#ai-platform-support)

English · [한국어](#한국어)

---

## What this is (and is not)

When you let an AI write a paragraph or design a landing page, it drifts toward the
**center of its training distribution** — the most average, most-seen output. People have
started calling that the *AI slop* look. In text it's the `delve`/`tapestry`/"it's not just X,
it's Y" voice. In UI it's the purple-to-indigo gradient, glassmorphism cards, Inter font, and
a 2×2 bento grid. In images it's waxy skin, six-fingered hands, and garbled signage.

**Human Craft** is a kit of Claude Code skills that *detect* those tells span-by-span and
*repair* them — preserving your meaning, your facts, and your intent, while removing the
machine fingerprint.

It is a **craft / quality tool**. It is **not**:

- an "Undetectable AI" detector-bypass service,
- a way to pass off AI work as human in academic, legal, or journalistic contexts where
  disclosure is required,
- a guarantee against any specific detector.

If a context requires you to disclose AI assistance, **disclose it.** See [`docs/ethics.md`](docs/ethics.md).

---

## Three skills

| Skill | What it cleans | Languages | Reference taxonomy |
|---|---|---|---|
| `humanize-writing` | Prose, posts, docs, emails | EN · 中文 · ES · AR · PT · 한국어 · any (universal tells) | [taxonomy](.claude/skills/humanize-writing/references/ai-tell-taxonomy.md) |
| `humanize-design` | Web/UI, landing pages, slide decks, HTML/CSS/React | Language-agnostic | [taxonomy](.claude/skills/humanize-design/references/design-slop-taxonomy.md) |
| `humanize-image` | Generated illustrations & photos — audit + fix brief | Language-agnostic | [taxonomy](.claude/skills/humanize-image/references/image-tell-taxonomy.md) |

Each skill follows the same loop: **detect → repair → verify (fidelity + naturalness) → grade.**

---

## The 4 principles (every skill obeys these)

1. **Intent is invariant.** Facts, numbers, proper nouns, direct quotes, brand rules, and the
   functional behavior of a design are preserved 100%. We change *how it reads/looks*, never
   *what it says or does*.
2. **Evidence-based, surgical edits.** We only touch spans/elements that a detector flagged.
   Un-flagged regions are left alone.
3. **Genre / brand stays.** A report doesn't become an essay; a B2B dashboard doesn't become a
   neobrutalist poster. We remove the *default*, not your *identity*.
4. **No over-editing.** Change-rate is monitored. Past a threshold the skill warns; past a hard
   ceiling it stops and asks you.

---

## Severity model

Tells are scored so the skill knows what to remove and what to leave.

- **S1 — decisive.** One occurrence is enough to read as AI. Always removed.
  *(e.g. "It's not just a tool, it's a journey"; a six-fingered hand; an em-dash–laden "delve" sentence.)*
- **S2 — strong.** Fine once or twice, a tell when stacked 3+ times.
  *(e.g. `Moreover` at the start of a sentence; one glassmorphism card.)*
- **S3 — weak.** Only a problem when it co-occurs with other tells.
  *(e.g. a single rounded-xl button; one rule-of-three list.)*

## Quality grades (after repair)

- **A** — 0 × S1, ≤2 × S2, big measurable improvement. Ship it.
- **B** — 0 × S1, ≤4 × S2. Good.
- **C** — 1–2 × S1 left, or 2+ over-editing signals. → run a 2nd pass.
- **D** — 3+ × S1, or heavy over-editing. → human review.

---

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

## Quickstart (≈5 minutes)

### 0. Prerequisite

Choose your AI platform. Claude Code is the reference implementation; all others work too.

**Claude Code** (reference — Mac / Windows / Linux)
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

**Cursor / Windsurf / GitHub Copilot:** open this folder in your IDE — no CLI needed.

### 1. Get the repo

```bash
git clone https://github.com/YOUR_NAME/human-craft.git
cd human-craft
```

### 2. Start Claude Code *inside this folder*

```bash
claude
```

> **Important:** launch it from inside `human-craft/`. Started elsewhere, the skills in this
> repo won't load and you'll just get plain Claude Code.

### 3. Paste your content and ask in plain language

**Writing**
```
de-slop this so it reads like a human wrote it:

[paste your AI draft]
```

**Design** (paste code, a URL, or describe it)
```
this landing page looks AI-generated — kill the slop but keep the layout working:

[paste your HTML/CSS/React, or a screenshot/URL]
```

**Image** (attach the image)
```
audit this generated image for AI tells and give me a fix brief
```

Any of these trigger phrases work: *"remove the AI tells," "de-slop this," "make it look
human-made," "kill the AI look," "humanize this draft / this UI."* No slash commands needed —
one natural sentence is enough.

### 4. What you get back

1. **Detection** — every tell, located, categorized, severity-tagged.
2. **Repair** — meaning/behavior preserved, only the machine fingerprint removed.
3. **Verification** — a fidelity audit (did meaning survive?) + a naturalness re-scan
   (did the tells actually go away, without over-editing?).
4. **Output** — the cleaned version, a diff of key changes, a quality grade (A/B/C/D),
   and any residual tells.

Detailed artifacts are written to `_workspace/{run-date-N}/` so runs never mix.

### 5. If you don't like it

Just say so, in plain words:

- *"only fix this paragraph / this component"* — re-run on a span
- *"only the vocabulary tells"* / *"only the gradient and the font"* — one category
- *"lower the intensity"* — conservative pass, S1 only
- *"keep more of the original tone / brand"* — lower the change-rate ceiling
- *"do a second pass"* — polish the current result again

---

## Do-NOT list (never flagged, never altered)

**Writing:** numbers, units, dates · proper nouns, names, product/model names · text inside
direct quotation marks · legal/regulatory wording · necessary technical terms.

**Design:** functional behavior, routes, form logic · accessibility features (these get *added*,
never removed) · required brand tokens you've pinned · real data and real metrics.

**Image:** the subject's identity and the factual content of the scene · anything that would
change what the image *documents*.

---

## Architecture (mirrors the agent harness pattern)

```
input  (text / design code / image)
   │
   ▼
[tell-detector]            ── span/element-level JSON report (category · severity)
   │
   ▼
[repairer]                 ── finding-based surgical edit, change-rate monitored
   │
   ▼
[parallel verification]
   ├─ [fidelity-auditor]   ── meaning/behavior equivalence checklist
   └─ [naturalness-reviewer] ── re-run detection: residual tells? over-editing?
   │
   ▼
[orchestrator]
   ├─ accept              → final + summary
   ├─ second pass         → up to 3 rounds
   ├─ rollback            → revert the offending edit
   └─ hold & report       → recommend human review
```

This kit is inspired by, and credits,
[`epoko77-ai/im-not-ai`](https://github.com/epoko77-ai/im-not-ai) (Korean-specialized writing
humanizer) and the [revfactory/harness](https://github.com/revfactory/harness) agent harness
pattern. Human Craft generalizes the idea to **multiple languages and multiple modalities.**

---

## Roadmap

- **v0 (this)** — three local Claude Code skills, English-first writing + web/UI design + image audit.
- **v1** — per-language writing packs (한국어 / 日本語 / 中文 / Español …), pluggable into the same engine.
- **v2** — a `brand-profile.yml` so teams pin their own fonts/colors/voice and the skill de-slops *toward the brand*, not toward generic.
- **v3** — optional web service (paste → highlighted tells → side-by-side diff → copy).
- **v4** — VS Code / browser extension.

See [`CONTRIBUTING.md`](CONTRIBUTING.md) to add a tell pattern or a language pack.

---

## License & ethics

MIT (code & taxonomies). The taxonomies are free for research and education.
This tool exists to improve craft, not to deceive. Read [`docs/ethics.md`](docs/ethics.md) before
using it anywhere disclosure matters.

---
<a name="한국어"></a>
## 한국어

AI에게 글을 쓰게 하거나 화면을 디자인하게 하면, 결과물은 학습 데이터의 **평균값(가장 흔한 출력)**
으로 수렴합니다. 사람들은 이걸 *AI 슬롭(slop)* 이라고 부릅니다. 글에서는 `delve`·"~할 수 있다"·
"단순한 X가 아니라 Y다" 같은 말투, UI에서는 보라→남색 그라데이션·글래스모피즘 카드·Inter 폰트·
2×2 벤토 그리드, 이미지에서는 밀랍 같은 피부·손가락 6개·뭉개진 글씨가 그 정체입니다.

**Human Craft** 는 그 "AI 티"를 **스팬(구간) 단위로 탐지하고, 의미·사실·의도를 100% 보존한 채
기계 지문만 제거**하는 Claude Code 스킬 모음입니다. 글·디자인·이미지 3개 모달리티를 다룹니다.

### 무엇이 아닌가
- "AI 탐지기 우회(Undetectable AI)" 도구가 **아닙니다.**
- 학술·법률·저널리즘처럼 **공개 의무가 있는 상황에서 AI 사용을 숨기는 용도가 아닙니다.**
- 특정 탐지기를 통과시켜 준다는 **보장도 없습니다.**

공개가 필요한 자리라면 **AI 사용 사실을 밝히세요.** ([`docs/ethics.md`](docs/ethics.md))

### 4대 철칙
1. **의도 불변** — 사실·수치·고유명사·직접 인용·브랜드 규칙·디자인의 기능은 100% 보존.
2. **근거 기반 수술적 수정** — 탐지된 구간/요소만 수정.
3. **장르·브랜드 유지** — 리포트를 에세이로, B2B 대시보드를 포스터로 바꾸지 않음.
4. **과윤문 금지** — 변경률 초과 시 경고, 상한 초과 시 중단.

### 5분 사용법
1. [Claude Code](https://claude.com/claude-code) 설치 → `claude --version` 확인
2. `git clone … && cd human-craft`
3. **이 폴더 안에서** `claude` 실행
4. 글/코드/이미지를 붙여넣고 한 문장으로 부탁: *"AI 티 없애줘", "슬롭 제거하고 레이아웃은 유지해줘",
   "이 생성 이미지 AI 티 점검해줘"*
5. 결과: 탐지 리포트 → 수정본 → 검증(의미 보존 + 자연도 재측정) → 등급(A/B/C/D)

이 레포는 [`epoko77-ai/im-not-ai`](https://github.com/epoko77-ai/im-not-ai)(한글 글 특화)와
[revfactory/harness](https://github.com/revfactory/harness) 아키텍처에서 영감을 받아,
**다국어 · 다중 모달리티**로 일반화한 프로젝트입니다.

---

Built with [Claude Code](https://claude.com/claude-code).
