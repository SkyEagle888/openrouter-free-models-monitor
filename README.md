# openrouter-free-models-monitor

Monitor the changes (add/remove/update) of [OpenRouter's free models](https://openrouter.ai/models?q=free).

## How It Works

- Fetches the model list from [OpenRouter API](https://openrouter.ai/api/v1/models) and filters for free models (IDs ending with `:free`)
- Compares against the previously stored list to detect additions and removals
- Sends Discord notifications **only when changes are detected** (silent on no-change runs)
- Updates `models.json`, `MODELS.md`, and `CHANGELOG.json` in the repository
- Runs automatically every 6 hours via GitHub Actions

## Setup

### Prerequisites

- Python 3.10+
- Discord webhook URL (optional, for notifications)

### Local Run

```bash
pip install -r requirements.txt
python monitor.py
```

### GitHub Actions Secrets

| Secret | Description |
|--------|-------------|
| `DISCORD_WEBHOOK_URL` | Discord webhook URL for notifications |
| `CLOUDFLARE_API_TOKEN` | (Optional) Cloudflare API token for Pages deployment |
| `CLOUDFLARE_ACCOUNT_ID` | (Optional) Cloudflare account ID |

## Project Structure

```
├── monitor.py          # Main monitoring script
├── models.json         # Current free model list
├── CHANGELOG.json      # Change history
├── MODELS.md           # Human-readable model list
├── dashboard/          # Web dashboard
│   ├── index.html
│   ├── app.js
│   └── styles.css
└── .github/workflows/
    └── monitor.yml     # GitHub Actions workflow
```
