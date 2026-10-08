# Glossary

Every technical term, explained simply. Alphabetical. Add new terms as they appear.

**Backend / server** — The part of the program that does the work and holds the data, out of sight. Like the render farm machine you never look at directly.

**.bgeo.sc** — Houdini's binary geometry file, compressed. SideFX documents `.bgeo`, but not the compression part.

**Cloudflare Tunnel** — Gives a program on your machine a public web address without opening your router. Needs a login (Cloudflare Access) in front to stay private.

**Command line** — The full instruction a program was started with: its name plus options, e.g. which file to render and which frames. Like the settings on a ROP, written out as text.

**Cross-platform** — Code that runs on more than one operating system (here Windows and Linux) without changes. Like a Houdini scene that renders the same on any farm machine as long as paths aren't hard-coded.

**Engine licence** — A Houdini licence for running Houdini without its interface (scripts, batch jobs). hython uses one while it runs.

**EULA (End User License Agreement)** — The contract that says what you may and may not do with a piece of software. SideFX's EULA covers Houdini.

**Fixture** — A real sample file (a log, an EXR) kept in the project so tests can check the code against real data. Like a reference frame you compare new renders against.

**Frontend / interface** — The part you see and click. Like Houdini's UI on top of its engine.

**HTTP** — The language browsers and servers use to ask for and send data. Each request is like asking a colleague "send me frame 42" and getting it back.

**husk** — Houdini's command-line renderer for USD scenes. The USD Render ROP launches it behind the scenes.

**hython** — Houdini's own Python: all of Houdini, controlled by a script, with no interface. Like running Houdini headless on a farm machine.

**Log file** — A text file a program writes while it works, line by line: what it's doing, warnings, errors. husk's log is like the Houdini console, saved to disk.

**Module** — One file (or small group of files) that does one job. Like a single node in a network.

**Output style** — A setting that changes how Claude Code talks and works. Laterna uses a custom one, "Laterna Tutor".

**Partial loading** — Opening a USD scene without its heavy parts, or only one branch of it (`LoadNone`, population mask). Like loading a scene with everything as bounding boxes.

**Process priority** — How much the computer favours a program when sharing the CPU. Laterna runs low, so the render always comes first.

**Process** — A program while it's running. Each render husk does is one process; you can see them in Task Manager.

**Python** — The programming language of Laterna's server, and Houdini's scripting language.

**React** — A JavaScript library for building interfaces out of reusable pieces called components. Like building a UI from HDAs.

**Remote access** — Opening Laterna from another device, outside your home network.

**Tailscale** — A private network that connects only your own devices, wherever they are. Nothing is visible to the rest of the internet.

**usd-core** — The free, official Python package for reading USD files without Houdini.

**VPN (virtual private network)** — A private network built on top of the internet, so devices in different places act as if they were in the same building. Like working from home on the studio's network. Tailscale is a VPN.
