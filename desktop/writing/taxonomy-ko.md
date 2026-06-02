# Writing AI-tell taxonomy — Korean (한국어)

Language-specific extension for `humanize-writing`. Load **after** the universal taxonomy
(`taxonomy.md`). Universal tells (W-D through W-L) apply to Korean prose too.

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
