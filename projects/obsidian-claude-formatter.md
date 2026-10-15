# Claude Selection Formatter (Obsidian plugin)

Highlight messy notes in Obsidian, press a hotkey, and the selection is rewritten in place as organized study notes: key terms, bullets, numbered steps and headings, with the meaning kept. One undo restores the original.

**Stack:** TypeScript · Obsidian plugin API · CodeMirror · esbuild · Node test runner
**Status:** working, used in my own vault. Source is private for now.

## Engineering highlights

- **It reuses an existing, signed-in tool instead of handling credentials.** The plugin runs the official Claude Code CLI in non-interactive mode, so it never sees or stores an API key. It also removes `ANTHROPIC_API_KEY` from the child process so billing can't silently switch to the API.
- **Minimal privileges for the model.** Claude is started with no tools, no MCP connectors, no user settings or hooks, and no saved session. The text goes in on stdin, never as a command-line argument or through a shell.
- **The editor can't be corrupted.** Before replacing text, the plugin checks that the same note is still open, the selection hasn't moved and the text is unchanged. Otherwise it discards the result. The replacement is a single editor transaction (one undo step). Errors are shown as notices, never inserted into the note.
- **Only the selection leaves the machine.** It never sends the rest of the note or the vault.

## Verification

27 mocked unit tests (Node's built-in test runner) and a TypeScript type check pass. A separate live test suite makes real Claude Code calls.

## Known limits

Desktop only. Heading numbers are local to the selection. The model is told to treat the selection as data, but no model-based tool can fully rule out prompt injection.
