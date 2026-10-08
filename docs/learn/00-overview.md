# Laterna in plain language

Think of Laterna as a **render wrangler that never sleeps**, plus a light table for looking at frames.

When you hit Render on a USD Render ROP, Houdini hands the scene to **husk**, the program that actually renders with Karma. husk writes two things: images (EXRs) and a log (text describing what it's doing). Laterna watches both, the way you'd glance at the render view and the console, and turns them into a dashboard you can open on your phone.

## The two halves

- **The server** (Python) runs on the render machine. It's like a node network that never stops cooking: one node finds renders, one reads logs, one checks hardware, one lists output files. Its result is data.
- **The interface** (React) runs in a browser. It asks the server for that data and draws it: job list, progress bars, thumbnails.

They talk over **HTTP**, the same way your browser talks to any website. That's why the interface works on any device.

## What Laterna never does

It only looks. It never edits a render, a log, or a USD file. Like a viewer flipbook, not a node that cooks into your scene.

## Phases

0. Check how husk, Karma and USD actually behave on your machine.
1. Monitor: jobs, progress, hardware, outputs, notifications.
2. Frame viewer: EXRs, AOVs, A/B comparison.
3. USD inspector: browse the scene being rendered.
