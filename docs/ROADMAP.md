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
- [ ] While husk runs, copy its full command line (Task Manager: Details tab, add the "Command line" column). Does it contain the USD file path, the frame range and the output path?
- [ ] Does the temporary USD file exist from the start to the end of the render? How big is it? Does it reference other files next to it?
- [ ] Copy the render's USD file while husk renders it, and open the copy with `usd-core` (pip install, no Houdini). Does it open? What's missing?
- [ ] Save one multi-AOV EXR from Karma. Note how AOVs are stored (one part with `diffuse.R` channels, or several parts).
- [ ] Windows CPU temperature: try LibreHardwareMonitor, see whether it needs admin rights and how another program can read its values.
- [x] Remote access: Tailscale (see DECISIONS).

## Phase 1 — Monitor

- **1a** Process watching: find husk renders, read their command line, watch output frames. Job list, progress (frames written of total, time per frame, ETA), crashed vs finished.
- **1a+** Log reader (when Log Output is on): progress within a frame, warnings, errors.
- **1b** Hardware panel, notifications (ntfy), remote access (Tailscale).
- **1c** Output browser with thumbnails.

Caches (simulation file caches) are out of Phase 1 until defined: they produce no husk log.

## Phase 2 — Frame viewer

EXR + AOVs, A/B (side-by-side, wipe, difference), version compare, exposure/gamma.

## Phase 3 — USD inspector

Read-only prim hierarchy, variants, layers, references, materials, missing files.

## Later / maybe

From `docs/BRIEF.md`, plus:

- `.bgeo.sc` reader: show basic facts about Houdini geometry files (point/primitive counts, attributes), once the fundamentals are in place. Must stay a viewer (EULA 4.1(viii), see DECISIONS).
- hython as an opt-in fallback, only if usd-core hits a roadblock and only after testing its licence behaviour (see DECISIONS).
- Sharing a render with others (e.g. a client) through Cloudflare Tunnel + Access.
