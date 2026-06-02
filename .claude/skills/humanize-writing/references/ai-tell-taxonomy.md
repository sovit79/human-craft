# Writing AI-tell taxonomy (SSOT)

The single source of truth for `humanize-writing`. English-first; the *engine* is language-agnostic
(per-language packs land in v1). Each tell has an **ID**, a **severity** (S1/S2/S3), a **why**, and a
**fix direction**. The detector reports findings as spans against these IDs.

> Sourcing: cross-checked against *Wikipedia: Signs of AI writing*, public "overused ChatGPT word"
> catalogs (2025–2026), and the Max-Planck observation that AI vocabulary is now leaking into
> unscripted human speech. Lists go stale as models change — treat this as a living document.

---

## W-A · Vocabulary tells

Words that travel well across every topic, so models reach for them by default. Individually
harmless; as a cluster, a fingerprint. **Where there's one, there are usually others.**

| Severity | Examples |
|---|---|
| S2 | delve, tapestry, testament, underscore, leverage (verb), realm, landscape (metaphor), navigate (metaphor), foster, harness, elevate, unlock, embark, robust, seamless, vibrant, bustling, meticulous, intricate, multifaceted, nuanced, comprehensive, pivotal, crucial |
| S3 | plethora, myriad, paradigm, beacon, treasure trove, game-changer, cutting-edge, state-of-the-art, holistic, synergy, ecosystem (non-biological) |

**Fix:** don't swap one fancy word for another. Use the word you'd say out loud — `delve` → "dig
into / look at"; `leverage` → "use"; `robust` → "solid / reliable"; `utilize` → "use". Delete
empty intensifier-adjectives entirely if the noun stands on its own.

---

## W-B · Stock phrases & openers

| Severity | Examples |
|---|---|
| S1 | "In today's fast-paced world", "In the ever-evolving landscape of …", "When it comes to …", "Look no further", "Rest assured" |
| S2 | "It's important to note that", "It's worth noting that", "Needless to say", "At the end of the day", "That being said", "Let's dive in", "Let's delve into", "Buckle up" |

**Fix:** cut the runway and start at the actual first idea. A sentence that survives deletion of its
opener was carrying dead weight.

---

## W-C · The "not just X, it's Y" construction (and negative antithesis)

| Severity | Pattern |
|---|---|
| **S1** | "It's not just a *tool*, it's a *journey*." · "This isn't about *X* — it's about *Y*." · "More than just a *noun*." |

The single most recognizable AI sentence shape in 2025–2026. One occurrence reads as AI.

**Fix:** state the claim directly. "It's not just fast, it's reliable" → "It's fast and reliable" —
or pick the one that matters and drop the other.

---

## W-D · Rule of three

LLMs overuse triples to make shallow analysis feel complete: "adjective, adjective, adjective" or
"short phrase, short phrase, and short phrase."

- **S2** — one or two triples in a piece.
- **S1** — triples stacked across consecutive sentences/paragraphs (the "comprehensive" illusion).

**Fix:** break the rhythm. Use two items, or four, or one. Let some lists be uneven.

---

## W-E · Connective / transition overuse

Sentence-initial `Moreover`, `Furthermore`, `Additionally`, `However`, `Therefore`,
`Consequently`, `Thus`, `In addition`, `Notably`.

- **S2** — sprinkled throughout.
- **S1** — three or more consecutive sentences each opening with one.

**Fix:** most can be deleted with no loss. Humans use "and", "but", "so", or just a new sentence.

---

## W-F · Excessive balance & hedging

The "view from nowhere." "While X is true, it's also worth considering Y." "On one hand … on the
other hand." "This can vary depending on several factors." "There are pros and cons to consider."

- **S2** — present.
- **S1** — every claim immediately neutralized; the piece takes no position.

**Fix:** commit. Humans have opinions, even cautious ones — "I'd do X" / "I wouldn't do Y."
Hedging is fine *once*, around genuine uncertainty, not as a reflex on every sentence.

---

## W-G · Conclusion tells

"In conclusion", "In summary", "Ultimately", "All in all", "To sum up", plus a tidy moral/takeaway
appended to every section.

- **S2** — one explicit "In conclusion."
- **S1** — a wrap-up sentence ending *every* section.

**Fix:** good endings stop, they don't announce stopping. Cut the label; often cut the whole
summary sentence.

---

## W-H · Rhythm uniformity

The hardest tell to feel, the strongest signal. Human prose has high variance in sentence length —
a 3-word sentence next to a 40-word one. Fragments. AI prose clusters near the mean and repeats the
same opening structures and the same end-of-sentence cadence.

- **S2** — low sentence-length variance.
- **S1** — near-uniform length *and* repeated sentence openings throughout.

**Fix:** deliberately vary. Add a fragment. Add one very long sentence and one very short one.
Start sentences differently. Read it aloud — if it has no bumps, add some.

---

## W-I · Structural / formatting tells

| Severity | Pattern |
|---|---|
| S2 | A bullet list where prose would do; every bullet a bolded keyword + colon + explanation; nested bullets for simple ideas |
| S2 | Section headers in Title Case everywhere; a heading every 2–3 sentences |
| S3 | Numbered "Firstly / Secondly / Thirdly" where "first / then / finally" or nothing would read better |

**Fix:** convert canned lists back to prose when the items aren't truly parallel data. "Some things
include x, y, and z" reads human; a bulleted trio of full sentences reads generated.

---

## W-J · Visual ornamentation

| Severity | Pattern |
|---|---|
| **S1** | Emoji as section bullets / headers (✨ 🚀 💡 🔑 ✅) in non-social prose |
| S2 | Em-dash (—) overuse — multiple per paragraph as the default connector |
| S2 | Bold scattered on random keywords for "emphasis"; arrows (→) inside prose |

**Fix:** strip decorative emoji. Replace most em-dashes with a comma, a period, or parentheses;
keep one if it earns its place. Bold only true UI labels or defined terms, not vibes.

---

## W-K · Empty enthusiasm & assistant voice

"Absolutely!", "Great question!", "I'd be happy to help with that.", "Sure thing!", "Let's get
started!", reflexive exclamation marks, "Dive into the world of …".

- **S1** — chat-assistant interjections inside what's meant to be authored content.

**Fix:** delete. Authored prose doesn't address the reader like a service rep mid-task.

---

## W-L · Missing human signal (absence tells)

Not a phrase — a *lack*. No contractions where speech would have them. No concrete specific detail
(a name, a date, a number, a small real anecdote). No first-person stake. No mild mess. Perfectly
even-handed about everything.

- **S2** — reads competent but sourceless.

**Fix:** add one concrete specific the model couldn't have invented (a real number, a real example).
Use contractions where you'd speak them. Let a genuine opinion show.

---

## Detector output format

```json
{
  "findings": [
    {
      "id": "W-C",
      "severity": "S1",
      "span": {"start": 412, "end": 461},
      "text": "It's not just a product, it's a movement",
      "note": "negative-antithesis construction",
      "fix_direction": "state the claim directly; pick one half or merge"
    }
  ],
  "metrics": {
    "sentence_length_cv": 0.18,
    "triples": 4,
    "sentence_initial_connectives": 6,
    "decorative_emoji": 3
  }
}
```

---

## Versioning

New patterns go to the bottom of this file as **candidates** with ≥2 real-world examples each.
Promotion to a numbered ID requires the examples plus a proposed severity and fix direction.
See [`CONTRIBUTING.md`](../../../../CONTRIBUTING.md).

### Candidates (unpromoted)
- *"Here's the thing:" / "The truth is:" as a manufactured pivot* — needs examples.
- *Curly "smart quotes" as a weak co-occurrence signal* — needs examples.
