# Decisions

One entry per non-obvious choice. Newest at the bottom. Pending decisions are listed at the end.

```
## YYYY-MM-DD — Title
**Decision:** what we chose
**Why:** reason in plain language
**Alternatives:** what else was possible and why not
**Trade-off:** what we give up
```

---

## 2026-10-07 — Python backend instead of the Konnekt stack (Wails/Go)

**Decision:** The backend is written in Python.
**Why:** The libraries Laterna needs (OpenUSD, OpenEXR/OpenImageIO, NVIDIA GPU stats) are all available for Python. Python is also Houdini's scripting language, so what Sandro learns here carries over to TD work.
**Alternatives:** Wails/Go (Konnekt stack): no OpenUSD bindings for Go were found, and Wails makes a desktop app, so remote access would need a separate server anyway.
**Trade-off:** Konnekt experience with Go doesn't carry over. Python is slower than Go, which doesn't matter at this scale.

## 2026-10-07 — React frontend in the browser

**Decision:** The interface is a React web app, opened in any browser (desktop or phone).
**Why:** One interface works locally and remotely. Sandro has seen React in Konnekt.
**Alternatives:** Native desktop app (no phone access); server-rendered pages with less JavaScript (simpler, but less suited to a live-updating viewer).
**Trade-off:** Two languages in one project (Python and JavaScript/TypeScript).

## 2026-10-07 — EXR files are decoded on the server, not in the browser

**Decision:** The Python backend reads EXRs and sends the browser one AOV at a time.
**Why:** The three.js EXR loader only reads channels named R, G, B, A, Y. It skips layered AOV channels such as `diffuse.R`.
**Alternatives:** Decode in the browser with three.js (loses AOVs); write a custom browser decoder (too complex).
**Trade-off:** More data sent over the network; the server does the work. To be confirmed with a real Karma EXR in Phase 0.

## 2026-10-07 — Custom "Laterna Tutor" output style instead of the built-in Learning style

**Decision:** Claude uses the project output style `.claude/output-styles/laterna-tutor.md`.
**Why:** The built-in Learning style asked Sandro to write code he didn't understand, with three-sentence instructions and no memory of earlier progress. The custom style only assigns tasks on concepts already explained, explains each task in full, and reads `docs/learn/PROGRESS.md` to know what Sandro has done.
**Alternatives:** Built-in Learning style (see above); Default style with no hands-on tasks (less learning).
**Trade-off:** Slower progress. An output style is an instruction, not a guarantee, so it may need tuning.

## 2026-10-07 — Phase 0 before any code; Phase 1 split into 1a/1b/1c

**Decision:** Verify assumptions on Sandro's machine first, and build Phase 1 in three parts.
**Why:** Claude works in an environment without Houdini, so real logs and files are needed as test fixtures. Phase 1 had seven features, too many for one usable step.
**Alternatives:** Start coding and adjust (risk of building on wrong assumptions about husk output).
**Trade-off:** No visible app for a while.

## 2026-10-07 — Code runs on Windows and Linux

**Decision:** Laterna must run on both Windows (now) and Linux (later). Nothing Windows-only in the core.
**Why:** The render machine runs Windows today and will move to Linux after an upgrade. Rewriting parts at that point would be wasted work.
**Alternatives:** Windows-only (simpler now, rework later).
**Trade-off:** File paths, process listing and hardware stats must go through cross-platform libraries (Python's `pathlib`, `psutil`, `nvidia-ml-py`). Features with no cross-platform library get a small per-system module.
**Known gap:** CPU temperature. `psutil` reads it on Linux only. On Windows it needs a separate tool such as LibreHardwareMonitor (needs admin rights; how Laterna reads its values is unverified). GPU stats via `nvidia-ml-py` work on both.

## 2026-10-07 — Remote access through Tailscale

**Decision:** Laterna is reached from other devices through Tailscale, a private network (VPN) between Sandro's own devices.
**Why:** Sandro is the only user. Laterna can browse render folders, so it should not have a public address. On Tailscale a wrong setting usually means "can't connect"; on a public address it can mean "everyone can see it". Free Personal plan, works on Windows, Linux, iOS and Android.
**Alternatives:** Cloudflare Tunnel + Cloudflare Access (used in Konnekt): a public web address with a login page in front. Opens in any browser without installing anything, but a mistake in Access exposes the render machine.
**Trade-off:** Every device needs the Tailscale app switched on. Other people can't look at a render without joining the network.
**Later:** Keep Cloudflare Tunnel + Access in mind for sharing features (e.g. showing a client a render's progress). Laterna itself doesn't change for either, so this can be added without rework.

## 2026-10-08 — Laterna installs nothing into Houdini

**Decision:** Laterna works with Houdini as it comes. No scripts, plugins or HDAs installed into Houdini. At most, built-in USD Render ROP settings are switched on (e.g. Log Output), ideally saved once as a preset.
**Why:** It should work out of the box, and a Houdini update should never break it.
**Alternatives:** A husk frame script (`Husk Post-Frame`) that reports each frame: more precise data, but it is code running inside the render, must be added to every ROP, and probably uses an Engine licence because it calls Houdini's `hou` module (inference, not tested).
**Trade-off:** Laterna only knows what husk writes to its log and what is visible from outside (files, processes).

## 2026-10-08 — Jobs detected by reading husk log files (provisional) — REPLACED, see "Jobs detected by watching processes"

**Decision:** Phase 1a reads the log files written by the USD Render ROP (Log Output). Watching husk processes is added afterwards, as its own step.
**Why:** Logs carry progress (with Alfred Style Progress on), warnings and errors. Log parsing can be built and tested in Claude's environment using real logs from `tests/fixtures/`. Process watching can't be tested there, and only shows *that* a render runs, not how far it is.
**Alternatives:** Process watching first (works with zero setup, but no progress); husk frame script (rejected, see above); watching output folders only (no progress within a frame, no errors).
**Trade-off:** Log Output has to be switched on in the ROP. A render without it is invisible to Laterna until process watching exists. Provisional until Phase 0 shows what the logs contain.

## 2026-10-08 — USD read with usd-core; hython later for deep inspection — REPLACED, see "Laterna never uses a Houdini licence"

**Decision:** Laterna reads USD files with `usd-core`. Later, an optional "deep inspect" can run a short hython script that opens the file with full Houdini, prints the result and exits.
**Why:** `usd-core` is free, needs no licence and runs inside Laterna's normal Python. hython sees everything (Houdini-only parts too), but uses an Engine licence while it runs, so it should only run on demand, never as Laterna's main engine. Learning hython is also useful TD knowledge.
**Alternatives:** Houdini's USD plugins loaded into Laterna's own Python: full view, but uses a batch licence and must match Houdini's exact USD version, which is fragile to set up. hython as the server itself: holds a licence all the time.
**Trade-off:** The normal inspector shows Houdini-only references (e.g. `.bgeo.sc`) as "needs Houdini" instead of their contents.


## 2026-10-08 — Laterna never uses a Houdini licence

**Decision:** Nothing Laterna does checks out a Houdini licence. No hython, no Houdini USD plugins, no Houdini libraries.
**Why:** A render must never be put at risk from Laterna. hython takes an Engine licence and falls back to the Core/FX licence interactive Houdini uses (SideFX FAQ). SideFX doesn't document what happens to a running process when licences run out; Sandro has seen a "no licence" popup force a re-login when opening another file. hython also loads all of Houdini, competing with the render for memory and CPU.
**Alternatives:** hython "deep inspect" on demand (replaced decision above).
**Trade-off:** Houdini-only content (e.g. `.bgeo.sc`) can't be opened by Laterna for now.
**Parked:** hython as an explicit opt-in, only if we hit a roadblock usd-core can't solve, and only after testing on Sandro's machine what a hython launch does to a running husk and to an open Houdini session. Never while a render is running unless that test shows it's safe.

## 2026-10-08 — Jobs detected by watching processes; log reader added on top

**Decision:** Phase 1a finds renders by watching for husk processes, reading their command line (USD file, frame range, output path), and watching the output folder for finished frames. Progress = frames written ÷ total, plus time per frame and ETA. Phase 1a+ adds the log reader for in-frame progress, warnings and errors when Log Output is on.
**Why:** Works with no settings in Houdini, so nothing breaks when switching files or PCs. The log reader is the easier part to add later and only adds detail.
**Alternatives:** Log reader first (replaced decision above): needs Log Output switched on in every ROP.
**Trade-off:** Without a log, no progress within a frame and no warnings/errors. Process watching can't be tested in Claude's environment, so it stays a thin layer; the logic behind it is tested with recorded examples (command lines, file timestamps) from Sandro's machine. Depends on Phase 0 confirming what husk's command line contains.

## 2026-10-08 — USD inspected with usd-core, on a copy, lightly

**Decision:** Laterna reads USD with `usd-core` only. It inspects a copy of the file, not the file husk is using, opens it partially (`LoadNone` or a population mask), and runs at low process priority.
**Why:** Free, no licence, and light on the render. Working on a copy avoids holding the original open: on Windows an open file can't be deleted, which could stop Houdini cleaning up its temp file (reasoning, not tested).
**Alternatives:** hython or Houdini's USD plugins (both use a licence, see above).
**Trade-off:** Houdini-only references show as "needs Houdini" with file name, size and date. Reading a huge scene still costs some memory.

## 2026-10-08 — Licences and rights (SideFX EULA, OpenUSD)

**Decision:** Laterna contains no SideFX software and never converts Houdini files. It may read files Houdini wrote (USD, EXR, logs, later `.bgeo` basics) to display information about them.
**Why:** Checked the SideFX EULA (version of 13 Oct 2021, the current one on sidefx.com), Section 4.1:
- (vii) no reverse engineering of the Software itself. Laterna doesn't touch Houdini's program code.
- (viii) no using "the file format of any file generated by the Software for purposes of by-passing any restrictions or requirements of the Software". Showing information about your own files doesn't bypass anything; a future `.bgeo` reader must stay a viewer, not a way to use Houdini data without Houdini.
- (x) no converting files made under a Non-Commercial licence (Education) into a commercial format. Laterna never converts or re-saves Houdini files.
- (ii) no distributing the Software. Laterna includes none of it.
OpenUSD uses the Tomorrow Open Source Technology License 1.0 (Apache 2.0 with a changed trademark section): free for any use. If Laterna is shared, its licence and notices must be included.
**Sharing with close ones:** allowed as far as these licences go, as long as Laterna stays free of SideFX code and ships the open-source licence notices. Each person needs their own Houdini licence for their own renders. Note: Education licences are for learning purposes only (EULA, Education License Type); that applies to how Houdini is used, not to Laterna.
**Trade-off:** This is a reading of the agreement, not legal advice. Re-check if the EULA changes or before sharing Laterna more widely.

---

## Pending

(None.)
