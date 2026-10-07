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

---

## Pending

- **Remote access.** Two options; the app itself is built the same way for both, so this can wait until Phase 1b.
  - *Tailscale*: a private network between your own devices. Nothing is exposed to the internet; the phone app joins the network. Free Personal plan (non-commercial, up to 6 users). Recommended: safest default.
  - *Cloudflare Tunnel* (used in Konnekt): gives the app a public web address. Must be combined with Cloudflare Access (a login page in front), otherwise anyone with the address can see the render machine's files.
- **How jobs are detected.** Candidates: find running husk processes and read their command line; parse husk logs; husk frame scripts (`--postframe-script`). Decide after Phase 0 shows what the USD Render ROP exposes.
- **USD access.** `usd-core` (free, no licence, but can't read Houdini-only parts like `.bgeo` references) vs. hython (full Houdini, uses a licence). Decide after Phase 0.
