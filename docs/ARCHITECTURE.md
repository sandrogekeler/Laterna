# Architecture

Draft. Fills in as Phase 0 answers come in.

```
Render machine                                         Any device
┌──────────────────────────────────────────┐          ┌──────────────┐
│ Houdini ─ USD Render ROP ─► husk         │          │ Browser      │
│                              │ log, EXRs │          │ (React UI)   │
│                              ▼           │  HTTP /  │              │
│ Laterna server (Python)                  │◄────────►│ desktop or   │
│  ├─ job watcher   (husk processes,       │
│  │                 output frames)         │ live     │ phone        │
│  ├─ log parser    (optional: errors)     │ updates  └──────────────┘
│  ├─ hardware      (CPU/GPU/RAM/disk)     │
│  ├─ outputs       (files, thumbnails)    │──► ntfy (notifications)
│  └─ web API       (serves data + UI)     │
└──────────────────────────────────────────┘
```

- Laterna never uses a Houdini licence and contains no SideFX code.
- Laterna only **reads**: logs, image files, USD files, hardware stats. It never changes a render.
- The server runs on the render machine. Remote access goes through Tailscale (private network), not through an open port. Cloudflare Tunnel may be added later for sharing.
