# Laterna — Project Brief

**Name:** Laterna
**What it is:** Render monitor & USD inspector
**Owner:** Sandro
**Type:** Personal tool + learning project (built with Claude Code)
**Status:** Idea / pre-phase 1

---

## 0. The name

**Laterna** is Latin for *lantern*.

- **The lantern:** it keeps watch over renders through the night and throws light on what's happening.
- **The *laterna magica*:** the 17th-century magic lantern, an early image projector and ancestor of cinema. Laterna is, at its core, a viewer for images.
- **Two lenses, one image:** 19th-century magic lanterns often had two lenses to fade from one picture into another — an early A/B wipe, like the comparison viewer.

Possible sub-name for later: **Fenestra** (Latin: *window*) for the USD scene inspector — a window into the running scene.

---

## 1. What this is

A personal tool for my Houdini/Solaris (USD, Karma) workflow that lets me:

1. Watch renders and caches remotely (status, output files, logs, hardware usage).
2. Inspect the USD scene that is currently rendering, in a separate read-only viewer.
3. Compare render versions A/B.

It is also a **learning project**: the goal is not only a working tool, but for me to understand every part of it well enough to explain and extend it without AI.

## 2. Why

- No free tool covers this for a solo Houdini/Karma artist.
- Portfolio piece showing I can direct AI agents (Claude Code, MCP) to build real pipeline tooling.
- Learn pipeline/TD concepts: USD, render management, file watching, client/server apps.

## 3. Non-goals

- Not a Prism/ShotGrid replacement (no full asset/shot/task management).
- Not a render farm scheduler for multiple artists.
- Not distributed publicly or sold.

---

## 4. Features by phase

Each phase must be usable on its own before starting the next.

### Phase 1 — Monitor (core)
- Job list: running / finished / failed renders and caches.
- Progress per job (frame X of Y, time per frame, ETA).
- Hardware panel: CPU, GPU, RAM, VRAM, disk usage, temperatures.
- Output browser: files written per job, with thumbnails.
- Render log parser: highlight errors, warnings, missing textures, slow frames, memory spikes.
- Notifications on finish/fail (phone or desktop).
- Remote access from another device on my network.

### Phase 2 — Frame viewer
- View rendered frames (EXR) including AOVs/layers.
- A/B comparison: side-by-side, wipe/split, difference mode.
- Compare across versions of the same shot.
- Basic exposure/gamma controls for viewing.

### Phase 3 — USD scene inspector
- Open the USD stage being rendered, read-only, without touching the render.
- Browse prim hierarchy, variants, layers, references.
- Show materials, textures, and flag missing files.
- Optional: simple 3D preview.

### Later / maybe
- Launch or re-queue renders from the tool.
- In-app AI panel (Claude via MCP/API) to ask questions about logs or the scene.
- Cache management (sizes, cleanup of old versions).

---

## 5. Open decisions (decide with Claude Code, log in DECISIONS.md)

- **Stack:** reuse my Konnekt stack (Wails/Go + React) vs. Python (closer to Houdini/USD tooling) vs. web app (server + browser client).
- **How jobs are detected:** watch output folders / parse logs / wrap the render command / Houdini-side hooks.
- **Remote access:** local network only vs. secure tunnel.
- **EXR reading:** which library, and whether the viewer runs in the browser or natively.
- **USD access:** OpenUSD Python bindings vs. Houdini's hython (licence implications to verify).

Unverified assumptions to check before building:
- That opening a USD stage read-only while husk renders it is safe and practical.
- What Karma/husk logs actually contain (progress, memory, warnings), based on my own real logs.
- Which features my Houdini licence allows for command-line rendering / hython.

---

## 6. Learning setup

The code stays clean and normally commented. The explanations live in `docs/`.

```
docs/
├── learn/            # Plain-language explanations, beginner level
│   ├── 00-overview.md        # The whole system explained simply
│   ├── glossary.md           # Every technical term, explained with analogies
│   └── <module>.md           # One file per module: what it does, why, how data flows
├── DECISIONS.md      # One entry per decision: what, why, alternatives, trade-offs
├── CONVENTIONS.md    # Naming, folder structure, code style
└── ARCHITECTURE.md   # Diagram + short description of components
```

### Rules for learning docs
- Assume zero programming background. Use analogies from VFX where possible (e.g. "like a Houdini node network", "like a render queue").
- Every new module gets a `docs/learn/` page in the same session it is written.
- Every non-obvious choice gets a DECISIONS.md entry.
- After each feature, Claude explains what was built and asks me 2–3 questions to check understanding.
- Once per phase, I change something by hand, without Claude, and note what I learned.

### DECISIONS.md entry format
```
## YYYY-MM-DD — Title
**Decision:** what we chose
**Why:** reason in plain language
**Alternatives:** what else was possible and why not
**Trade-off:** what we give up
```

---

## 7. Notes for Claude Code

- Keep CLAUDE.md short: project summary, stack, commands, conventions. Point to `docs/` by path; do not import the learning docs.
- Work in small steps. Propose a plan before large changes.
- Prefer simple, readable solutions over clever ones; I need to understand them.
- Don't add features beyond the current phase without asking.
- When unsure about Houdini/USD/Karma behaviour, say so and suggest how to verify instead of guessing.

---

## 8. Portfolio framing

Presented honestly as: *"A personal pipeline tool I designed and directed, built with Claude Code as a learning project. Decisions and architecture are documented in `docs/`."*
