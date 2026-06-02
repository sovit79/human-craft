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
