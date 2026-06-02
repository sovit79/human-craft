# CLAUDE.md — project instructions for Claude Code

This repo is **Human Craft**, a kit of skills that remove "AI tells" from writing, UI design, and
images so the output reads as deliberate human craft. When Claude Code runs inside this folder:

## Load the right skill by intent
- Text pasted + "de-slop / remove AI tells / humanize / kill the ChatGPT voice" → `humanize-writing`.
- HTML/CSS/React, screenshot, or URL + "looks AI-generated / de-slop the UI / kill the AI look"
  → `humanize-design`.
- An image attached + "does this look AI / audit for tells / fix brief" → `humanize-image`.

## Always obey the 4 principles
1. Intent invariant (facts, numbers, proper nouns, quotes, functional behavior preserved 100%).
2. Evidence-based, surgical edits (only flagged spans/elements).
3. Genre/brand stays (remove the default, not the identity).
4. No over-editing (warn >30% change, hard-stop >50%, ask the user).

## Always run the full loop
detect → repair → verify (fidelity + naturalness, in parallel) → grade (A/B/C/D) → decide
(accept / 2nd pass up to 3 / rollback / hold for human review).

## Ethics gate
This is a quality tool, not a detector-bypass tool. Never strip or falsify image provenance
(C2PA/EXIF). If the user's context implies required disclosure (academic, legal, journalism),
remind them to disclose. See docs/ethics.md.

## Workspace
Write detailed artifacts to `_workspace/{run-date-N}/` so runs never mix. Keep the chat reply concise:
cleaned output + key diffs + grade + residual tells.

## Reference files are the source of truth
Read the relevant `references/*taxonomy*.md` before detecting, and the matching `*playbook*.md`
before repairing. Don't rely on memory for the pattern lists — they're versioned in those files.
