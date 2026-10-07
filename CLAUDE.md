# Laterna

Personal render monitor and USD inspector for a Houdini/Solaris (Karma) workflow. It is also a learning project: Sandro must be able to explain and extend every part without AI.

## Status

Phase 0: verification and setup. No application code yet. See `docs/ROADMAP.md`.

## Stack (see `docs/DECISIONS.md`)

- Backend: Python (FastAPI planned). OpenUSD via `usd-core`, EXR via OpenImageIO/OpenEXR, GPU via `nvidia-ml-py`.
- Frontend: React in the browser, served by the backend.
- Render machine: NVIDIA GPU. Houdini Education now, Indie later.

## Commands

None yet. Add build/test/run commands here when Phase 1 starts.

## Where things live

- `docs/BRIEF.md`: project brief (goals, phases, non-goals).
- `docs/ROADMAP.md`: phases and the current checklist.
- `docs/DECISIONS.md`: every non-obvious choice. Add an entry when you make one.
- `docs/ARCHITECTURE.md`, `docs/CONVENTIONS.md`: structure and code style.
- `docs/learn/`: beginner explanations. `docs/learn/PROGRESS.md` records what Sandro has learned and built.
- `tests/fixtures/`: real husk logs, EXRs and USD files from Sandro's machine. Houdini is not available in Claude's environment, so these are the ground truth.

## Rules

- Work in small steps. Propose a plan before any change touching more than one module.
- Prefer simple, readable code over clever code.
- Stay inside the current phase. Ask before adding anything from a later phase.
- Houdini/USD/Karma behaviour: if unsure, say so and propose how to verify on Sandro's machine. Never guess.
- Every new module gets a `docs/learn/<module>.md` page in the same session.
- Update `docs/learn/glossary.md` when a new technical term appears.
