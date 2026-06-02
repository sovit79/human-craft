# Writing AI-tell taxonomy — Arabic (العربية)

Language-specific extension for `humanize-writing`. Load **after** the universal taxonomy
(`taxonomy.md`). Universal tells (W-D through W-L) apply to Arabic prose too.

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
