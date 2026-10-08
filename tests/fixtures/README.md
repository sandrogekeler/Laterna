# Fixtures

Real files from Sandro's render machine. Claude's environment has no Houdini, so these are the only ground truth for how husk, Karma and USD behave.

Collected in Phase 0 (see `docs/ROADMAP.md`). Keep files small: a few frames, low resolution.

| Folder | What goes in | Example name |
|--------|--------------|--------------|
| `logs/` | Full husk logs: a good render, a failed one, one with a missing texture | `husk_ok_Va3.log` |
| `exr/` | One single-layer and one multi-AOV Karma EXR | `karma_aovs.exr` |
| `usd/` | The USD file husk rendered (copied from the temp folder) | `shot_render.usd` |

For each file, add a line here saying how it was made (Houdini version, ROP settings or husk command).
