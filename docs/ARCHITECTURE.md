## System Topology

- **Monitor Script** (`monitor.py`): Python script. Fetches OpenRouter API, detects changes, updates JSON/MD files, sends Discord webhook.
- **GitHub Actions** (`.github/workflows/monitor.yml`): Cron-triggered (every 6h). Runs monitor, commits changes, deploys.
- **Dashboard** (`dashboard/`): Static SPA. Loads `models.json` + `CHANGELOG.json` via fetch. Chart.js + DataTables + Tailwind CSS.
- **Landing Page** (`index.html`): Static HTML. Loads `models.json` for stats.

```
OpenRouter API → monitor.py → models.json / CHANGELOG.json / MODELS.md
                                      ↓
                              GitHub Actions (cron 6h)
                                      ↓
                         Git commit + push + GitHub Pages deploy
                                      ↓
                              Dashboard (static HTML/JS)
```

## Tech Stack & Dependencies

- **Runtime**: Python 3.10
- **Python deps**: `requests`, `pytz` (see `requirements.txt`)
- **Frontend**: Vanilla JS, jQuery 3.7.1, Chart.js 4.4.0, DataTables 1.13.7, Tailwind CSS (CDN)
- **CI/CD**: GitHub Actions (ubuntu-latest)
- **Deployment**: GitHub Pages (primary)

## Deployment & Infra

- **GitHub Actions workflow**: `monitor.yml` — cron `17 1,7,13,19 * * *` + manual trigger
- **GitHub Pages**: `gh-pages` branch, served from root
- **Secrets required**: `DISCORD_WEBHOOK_URL` (set), `GITHUB_TOKEN` (auto)

## Data Model & Schema

### `models.json`
- Type: `string[]` — sorted array of free model IDs (e.g., `google/gemma-3-4b-it:free`)
- Updated on change detection or initial run

### `CHANGELOG.json`
- Type: `{ "changes": ChangeEntry[] }`
- `ChangeEntry`: `{ timestamp: string (ISO 8601), added: string[], removed: string[], total_models: number }`
- Capped at 100 entries (`MAX_CHANGELOG_ENTRIES`)

### `MODELS.md`
- Human-readable markdown. Grouped by provider. Auto-regenerated each run.

### API Contract (OpenRouter)
- Endpoint: `GET https://openrouter.ai/api/v1/models`
- Response: `{ "data": [{ id, name, pricing: { prompt, completion }, architecture, context_length, ... }] }`
- Free model filter: `model_id.endswith(':free')` (also `pricing.prompt == "0"`)
