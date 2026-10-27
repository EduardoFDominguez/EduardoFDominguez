# Local Study Assistant

A study sidebar for Windows that sits beside a browser, PDF reader or slides and explains questions step by step with a language model running on the same computer. It also keeps notes and imported documents you can search and ask about. Everything runs locally: no accounts, API keys or cloud services.

**Stack:** Tauri 2 · Rust · React · TypeScript · Python · Ollama · SQLite
**Status:** early development, private source. Built with AI-assisted development (Claude Code).

## What it does

- **Explains a question from the screen:** you crop a region (or read a whole window); Windows OCR extracts the text, and the local model answers with a final result followed by numbered explanation steps. You can correct the extracted text or send the screenshot to a vision model instead.
- **Double-check:** an independent second solve, a SymPy comparison when both answers are plain math, and a judging step only when they disagree.
- **Documents and notes:** import PDFs and images, read scanned pages with OCR, ask about a page range with cited passages, keep Markdown notes, and search documents, notes and saved answers together. Backups go to one .zip file.

## Engineering highlights

- **Local-only trust boundary.** The Python backend listens on loopback only, and the Rust shell exposes an allowlist of backend methods to the frontend. Nothing leaves the computer at run time; network use is limited to setup.
- **Capture on demand only.** The screen is read only when you press a capture button or hotkey; screenshots stay in memory and go only to the local model.
- **Honest about model limits.** Agreement between two solves raises confidence but isn't treated as proof, and answers are labeled as unverified.

## Verification

Backend tests (unittest), frontend tests (Vitest) and Rust tests (`cargo test`, including real Windows OCR) are part of the repository; see the inventory for the latest dated results. Parts of the document flow have been checked by automated tests only, not by hand in the running app.

## Known limits

On the development laptop the model runs on the CPU, so an answer takes about 75 to 165 seconds. Windows OCR loses math notation such as integral signs and fraction bars. Document questions use keyword retrieval, so a passage worded differently can be missed. There is no installer yet.
