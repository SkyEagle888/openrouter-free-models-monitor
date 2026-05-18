## Workflow Rules

- Python 3.10+ runtime. Windows 11 / PowerShell dev environment.
- GitHub Actions runner: `ubuntu-latest`. Never assume Windows on CI.
- Use `snip-bash` for large-output commands (git log, npm, docker, etc.).
- Use `bash` only for short commands (<20 lines output).
- Run `python monitor.py` locally to validate before commit.
- Never commit secrets. All config via GitHub Actions secrets.

## Context Loading Protocol

- At session start, always read `docs/CONTEXT-MAP.md` before exploring code.
- Use it as the primary navigation index. Load only files referenced there.
- Never load full directories or unrelated modules without explicit mapping.
- Load `docs/SCOPE.md` and `docs/PLAN.md` at session initialization for requirement baseline and phased task alignment.
- If combined file size exceeds 5KB, extract only the active phase, pending tasks, and requirement boundaries relevant to the current `CHANGE-LOG.md` objective.
- Validate implementation output against `PLAN.md` checkbox status before marking `- [x]`.
- Flag requirement deviations or scope drift in `CHANGE-LOG.md` immediately; do not auto-modify upstream references.

## Architecture & Token Control

- If `graphify-out/GRAPH_REPORT.md` exists
  - Before reading source files, running grep, or generating code, read `graphify-out/GRAPH_REPORT.md`.
  - Extract only the target modules, god nodes, and cross-dependencies relevant to the task.
  - Retrieve files strictly by path listed in the report. Do not traverse directories recursively.
  - After code changes, execute `graphify update .` before committing.

## Token Budgets

- Combined memory file footprint target: <50KB.
- `docs/CHANGE-LOG.md`: Retain last 30 sessions or 14 days. Auto-prune 🟢 Low after 7 days.
- If `CHANGE-LOG.md` >15KB, auto-trim low-priority entries and output warning.
- Archive pruned entries to `/docs/archive/CHANGE-ARCHIVE-YYYY-QN.md`.

## AI Directives

- Adapted from `nvidia-nim-models-monitor` → `openrouter-free-models-monitor`.
- Free models identified by `:free` suffix in model ID from `https://openrouter.ai/api/v1/models`.
- Same storage mechanism: `models.json`, `CHANGELOG.json`, `MODELS.md`.
- Same Discord notification pattern with "OpenRouter" branding.
- Schedule: every 6 hours via cron `17 1,7,13,19 * * *`.
- Dashboard: static HTML/JS (Chart.js, DataTables, Tailwind CSS) served via GitHub Pages.
- No database. All state in JSON files committed to repo.
