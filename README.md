## About me

I'm a computer science student. I build desktop tools for Windows, mostly local-first apps that keep data on your own machine and AI tools where a person stays in control of every change.

I build with AI-assisted development (Claude Code). What I focus on is the parts that make that trustworthy: clear safety boundaries, approval steps enforced in code, and tests that check the behavior.

### Selected projects

| Project | What it is | Stack |
|---|---|---|
| [AI Coding Workbench](projects/ai-coding-workbench.md) | Desktop app that drafts a project with an LLM, then has Claude Code review it, with human approval gates enforced by a Rust state machine and tied to content hashes | Tauri, Rust, React, TypeScript, SQLite |
| [Personal OS](projects/personal-os.md) | Command center for tasks, course deadlines, bills and job applications, stored as plain Markdown in Obsidian with conflict-safe writes | Python, Tkinter |
| [Local AI Assistant](projects/local-ai-assistant.md) | Chat assistant on a local LLM (Ollama) that can only *propose* file changes and scripts; nothing runs without approval | Python (standard library), Tkinter |
| [Claude Selection Formatter](projects/obsidian-claude-formatter.md) | Obsidian plugin that turns highlighted notes into structured study notes in one undoable step | TypeScript, Obsidian API |

The source code for these projects is private. Each link above goes to a write-up of what the project does, how it's designed and how it's tested. I'm happy to walk through the code on request.

### Tools I've used in these projects

Python · TypeScript · Rust · React · Tauri · Tkinter · SQLite · Node.js · Vite · Vitest · unittest · Git
