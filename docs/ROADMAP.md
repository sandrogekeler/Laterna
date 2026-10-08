# Roadmap

Each phase must be usable on its own before the next starts. Full feature list: `docs/BRIEF.md`.

## Phase 0 — Verify and set up (current)

Nothing gets built until these are checked on Sandro's machine. Results go into `tests/fixtures/` and `docs/DECISIONS.md`.

- [x] Render machine OS: Windows now, Linux later.
- [ ] Render 5–10 frames with the USD Render ROP using **Render to Disk in Background**, with these ROP settings:
  - **Log Output** on. **Output Log** and **Error Log** pointing into one folder, e.g. `D:/laterna/logs/`. Note whether variables like `$HIPNAME` work in the file name.
  - **Alfred Style Progress** on.
  - **Verbose**: 3.
  - **Delete Files**: Never Delete. **USD Output Directory**: a fixed folder, e.g. `D:/laterna/usd/`.
  - **Print Command Line to Console** on. Copy the printed husk command into `tests/fixtures/README.md`.
- [ ] Watch the log while it renders: does it grow line by line, or only appear at the end? (Laterna needs the first.)
- [ ] Check whether the ROP settings can be saved once (preset or permanent defaults), so new ROPs have them already.
- [ ] Save one log from a failed render and one with a missing texture.
- [ ] While husk runs, check whether its command line (and the USD file path) is visible (Task Manager: add the "Command line" column on the Details tab).
- [ ] Open the render's USD file with `usd-core` (pip install, no Houdini) while husk renders it. Does it open? What's missing?
- [ ] Save one multi-AOV EXR from Karma. Note how AOVs are stored (one part with `diffuse.R` channels, or several parts).
- [ ] hython: run `hython -c "print('hello')"` from a terminal. Does Education allow it? Which licence does the License Administrator show while it runs? Note what changes with Indie.
- [ ] Windows CPU temperature: try LibreHardwareMonitor, see whether it needs admin rights and how another program can read its values.
- [x] Remote access: Tailscale (see DECISIONS).

## Phase 1 — Monitor

- **1a** Log reader: job list, progress (frame X of Y, time per frame, ETA), warnings and errors.
- **1a+** Process watching: spot husk renders without a log, tell crashed from finished.
- **1b** Hardware panel, notifications (ntfy), remote access (Tailscale).
- **1c** Output browser with thumbnails.

Caches (simulation file caches) are out of Phase 1 until defined: they produce no husk log.

## Phase 2 — Frame viewer

EXR + AOVs, A/B (side-by-side, wipe, difference), version compare, exposure/gamma.

## Phase 3 — USD inspector

Read-only prim hierarchy, variants, layers, references, materials, missing files.

## Later / maybe

From `docs/BRIEF.md`, plus:

- "Deep inspect" for USD via hython (full Houdini view, on demand).
- Sharing a render with others (e.g. a client) through Cloudflare Tunnel + Access.
