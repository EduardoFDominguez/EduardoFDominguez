# Local AI Assistant

A floating "AI" button for Windows that opens a chat window backed by a language model running locally through Ollama. It has no cloud model, no API key and no telemetry. It can research the web and work with files, but it cannot change anything without the user's approval.

**Stack:** Python 3 (standard library only) · Tkinter · Ollama HTTP API
**Status:** working prototype. Source is private.

## Engineering highlights

- **The code limits what the model can do, rather than filtering topics.** Read-only tools run automatically within scope. Every file write, edit, delete, move or PowerShell script can only create a *preview*. No tool can approve or execute anything.
- **Approvals are bound to exact parameters.** Each pending action has a unique ID and a SHA-256 fingerprint of its parameters. It runs once, and it is refused if anything changed. Before writing, the target file is checked again. Writes are atomic and keep a backup.
- **Path scoping.** Every path is canonicalized (symlinks and junctions resolved, `..` collapsed) and checked against the folders the user approved. Device paths and alternate data streams are rejected.
- **Privacy-minimizing web research.** Only a short search query leaves the machine. Emails, phone and card numbers, local paths and passwords are stripped from it first, and the model's own web searches are blocked in any turn where it has read a local file.
- **PowerShell gated twice.** The user sees the exact script, a plain-language explanation and flagged system areas (registry, services, startup, installs). Running it needs an approval plus a second confirmation. Scripts that request elevation are refused.
- **A test that enforces the architecture.** A static test checks that subprocesses are created only in the PowerShell module.

## Verification

83 unit tests pass. They run against a fake Ollama server and a fake web, so they never touch real files, the internet or the real model. A separate integration test talks to the real local model.

## Known limits

A 24B-parameter model on a laptop CPU is slow (minutes per reply). Approved PowerShell scripts run with the user's own rights.
