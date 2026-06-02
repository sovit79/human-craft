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
