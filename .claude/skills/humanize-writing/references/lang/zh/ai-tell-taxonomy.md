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
