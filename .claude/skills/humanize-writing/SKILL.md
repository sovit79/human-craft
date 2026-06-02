---
name: humanize-writing
description: >-
  Detect and remove "AI tells" from prose so it reads as deliberate human craft, not the default
  output of a chat model. Use whenever the user pastes AI-generated or AI-assisted text and asks to
  "de-slop", "remove AI tells", "make it sound human / human-written", "kill the ChatGPT voice",
  "humanize this draft", or "fix the AI writing". Supports English, 中文, Español, العربية,
  Português, 한국어; language-agnostic engine for all others. Preserves meaning, facts, quotes,
  and genre. NOT a detector-bypass tool — see docs/ethics.md.
---

# humanize-writing

Remove the machine fingerprint from text while keeping its meaning 100% intact.

## When this triggers
Any of: "remove AI tells", "de-slop this", "make it read like a human wrote it", "kill the ChatGPT
voice", "remove translationese", "humanize this draft". One plain sentence is enough.

Works in any language; language-specific AI-tell patterns load automatically for Chinese (中文),
Spanish (Español), Arabic (العربية), Portuguese (Português), and Korean (한국어).

## The 4 principles (non-negotiable)
1. **Intent invariant** — facts, numbers, proper nouns, direct quotes preserved exactly.
2. **Evidence-based** — edit only flagged spans (see taxonomy). Leave clean spans alone.
3. **Genre stays** — don't turn a report into an essay or a memo into a blog post.
4. **No over-editing** — warn above 30% change-rate, hard-stop above 50%, and ask the user.

## Loop
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
2. **Repair.** Per finding, apply the smallest edit that removes the tell. Follow
   `references/rewriting-playbook.md`. Track change-rate.
3. **Verify (parallel).**
   - *Fidelity:* did every fact / number / proper noun / quote survive? If not → roll back that edit.
   - *Naturalness:* re-run detection. Residual S1s? Over-editing signals (lost voice, altered
     meaning, register drift)?
4. **Grade & decide.** A → ship. B → ship with notes. C → second pass (max 3). D → recommend human
   review and show what's still flagged.

## Do-NOT touch
Numbers · units · dates · proper nouns · names · product/model names · text inside direct quotes ·
legal/regulatory wording · necessary technical terms.

## Output
- the cleaned text,
- a short diff of the most important changes (before → after),
- a grade (A/B/C/D) + any residual tells,
- detailed artifacts under `_workspace/{run-date-N}/`.

## Reference files
- `references/ai-tell-taxonomy.md` — the 12 categories (W-A … W-L) with severities.
- `references/rewriting-playbook.md` — concrete fix recipes per category.
