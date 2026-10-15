# Personal OS

A Windows desktop command center for the things a student has to keep track of: tasks, course deadlines, bills, a budget and job applications. All data lives as plain Markdown in an Obsidian vault, so it stays readable and editable without the app.

**Stack:** Python 3 · Tkinter · pystray · Pillow · unittest
**Status:** in daily personal use. Source is private because it is built around my own workflows.

## What it does

- **Tasks and planning:** natural-language entry such as *"Water the plants every Monday"* is parsed instantly, with no AI involved, into a due date and a recurrence rule. A ranked "Today" plan shows its reasons.
- **School:** read-only import of Canvas LMS assignments through the calendar feed, with exams and quizzes detected from titles.
- **Finance and career:** bill reminders, budget and savings goals, plus a job-application tracker with follow-ups and optional job search through public APIs.
- **Reminders:** tray icon, desktop widget and a persistent popup, with snooze and quiet hours.
- **Optional AI assistant:** Claude through the Claude Code CLI, with a local Ollama model as fallback. AI output is always a proposal that the user reviews. It never saves or submits anything on its own.

## Engineering highlights

- **Markdown as the source of truth, written safely.** Writes are atomic. Text outside the app's data blocks is never touched. An invalid block is reported, never rewritten. If a file changed in Obsidian after the app loaded it, the save stops instead of overwriting.
- **Daily automatic backups** of each data file, keeping 14 per file.
- **Layered design.** The UI never parses Markdown. It calls services (tasks, finance, career, reminders), which call the store. That separation is what makes the 100+ unit tests possible without a GUI.
- **Secrets stay out of files.** Feed links and API keys are read at runtime from Windows Credential Manager. Logs record events and counts only, never task text, amounts or URLs.
- **Lightweight on purpose.** I stayed with Tkinter plus a custom dark theme, instead of a browser-based framework, to keep memory use and dependencies small. The app has only two direct third-party dependencies.

## Verification

106 unit tests (unittest) pass. They cover the task model, Markdown store, recurrence, planning, Canvas parsing and services, and they run against temporary folders, not real data.

## Known limits

Reminders only fire while I'm signed in, by design (no background service). The Canvas feed has no submission status. The app isn't packaged as an installer.
