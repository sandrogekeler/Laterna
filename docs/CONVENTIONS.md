# Conventions

Tooling (package manager, linter, TypeScript or JavaScript) is decided at the start of Phase 1 and recorded in `DECISIONS.md`.

## General

- Clear names over short names: `frame_duration_seconds`, not `fd`.
- One module does one job. If you can't describe it in one sentence, split it.
- Comments say *why*, not *what*. Long explanations go in `docs/learn/`.
- Laterna never writes to render outputs, logs or USD files.
- Must run on Windows and Linux. Use `pathlib` for paths, never build them with `\` or `/` by hand. Tests must not depend on one system.

## Python

- Style: PEP 8. Names: `snake_case` for functions and variables, `PascalCase` for classes.
- Type hints on function signatures.
- Tests with pytest, using real files from `tests/fixtures/`.

## Frontend

- React function components, one per file, `PascalCase.tsx`/`.jsx`.

## Git

- Small commits, one idea each. Message says what changed and why.
