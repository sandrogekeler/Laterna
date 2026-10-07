# Roadmap

Each phase must be usable on its own before the next starts. Full feature list: `docs/BRIEF.md`.

## Phase 0 — Verify and set up (current)

Nothing gets built until these are checked on Sandro's machine. Results go into `tests/fixtures/` and `docs/DECISIONS.md`.

- [x] Render machine OS: Windows now, Linux later.
- [ ] Render a short sequence (5–10 frames) with the USD Render ROP. Find out:
  - [ ] Where husk's output (log) ends up. Can the ROP write it to a file?
  - [ ] Which husk options the ROP exposes (verbosity, extra command-line arguments, frame scripts).
  - [ ] Whether the temporary USD file stays on disk during and after the render, and where (`HOUDINI_TEMP_DIR`).
- [ ] Run the same render with husk from the command line using `-Va3` (progress + verbosity 3; check `husk --help` for exact syntax). Save the full log.
- [ ] Save one log from a failed render and one with a missing texture.
- [ ] While husk runs, check whether its command line (and the USD file path) is visible (Task Manager: add the "Command line" column on the Details tab).
- [ ] Open the render's USD file with `usd-core` (pip install, no Houdini) while husk renders it. Does it open? What's missing?
- [ ] Save one multi-AOV EXR from Karma. Note how AOVs are stored (one part with `diffuse.R` channels, or several parts).
- [ ] Confirm Education licence allows husk from the command line and hython. Note what changes with Indie.
- [ ] Windows CPU temperature: try LibreHardwareMonitor, see whether it needs admin rights and how another program can read its values.
- [ ] Decide remote access (see DECISIONS: pending).

## Phase 1 — Monitor

- **1a** Job list, progress (frame X of Y, time per frame, ETA), log parser.
- **1b** Hardware panel, notifications (ntfy), remote access.
- **1c** Output browser with thumbnails.

Caches (simulation file caches) are out of Phase 1 until defined: they produce no husk log.

## Phase 2 — Frame viewer

EXR + AOVs, A/B (side-by-side, wipe, difference), version compare, exposure/gamma.

## Phase 3 — USD inspector

Read-only prim hierarchy, variants, layers, references, materials, missing files.
