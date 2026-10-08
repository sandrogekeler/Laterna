---
name: checkpoint
description: End-of-feature learning check. Explains what was built, asks Sandro 2-3 questions, and updates the learning docs and decision log.
disable-model-invocation: true
---

Run this after a feature or a meaningful step is finished.

1. **Summarise what was built** in plain language: what it does, which files changed, how data flows. Use a VFX analogy if one fits. Keep it under 15 lines.
2. **Check the docs are current.** For every new or changed module:
   - `docs/learn/<module>.md` exists and matches the code.
   - New terms are in `docs/learn/glossary.md`.
   - Non-obvious choices have an entry in `docs/DECISIONS.md`.
   Fix anything missing and say what you fixed.
3. **Ask 2–3 questions** that check understanding, not memory. Prefer "what would happen if…" and "why did we…" over "what is…". Ask them one at a time and wait for each answer.
4. **Give feedback** on each answer. If an answer shows a gap, explain that part again briefly and note it.
5. **Update `docs/learn/PROGRESS.md`:** add the feature to "Built", the concepts to "Learned", and any gaps to "Revisit".
6. If this finishes a phase, remind Sandro of the hand-change exercise: change something himself, without Claude, and write down what he learned in `PROGRESS.md`.
