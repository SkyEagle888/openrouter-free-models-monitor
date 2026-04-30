## Requirements Baseline

### Project Goal
Monitor OpenRouter's free AI model catalog for additions, removals, and updates. Notify via Discord. Provide an interactive dashboard.

### Source
- Adapted from: `nvidia-nim-models-monitor` (https://github.com/SkyEagle888/nvidia-nim-models-monitor)
- Target API: `https://openrouter.ai/api/v1/models`
- Free model page: `https://openrouter.ai/models?q=free`

### Assumptions
- All free model IDs end with `:free`
- Use same storage mechanism (JSON files in repo)
- Use same Discord notification pattern with "OpenRouter" branding

### Functional Requirements
- FR-1: Fetch model list from OpenRouter API and filter free models by `:free` suffix
- FR-2: Detect added/removed models by comparing with previous state
- FR-3: Store current models in `models.json`
- FR-4: Log changes with timestamp in `CHANGELOG.json` (max 100 entries)
- FR-5: Generate human-readable `MODELS.md` grouped by provider
- FR-6: Send Discord notifications on change (webhook via env var)
- FR-7: Run automatically every 6 hours via GitHub Actions
- FR-8: Deploy dashboard to GitHub Pages on each run
- FR-9: Provide interactive dashboard with charts, filters, change history

### Non-Functional Requirements
- NFR-1: Python 3.10 compatible
- NFR-2: No database dependency (file-based storage)
- NFR-3: Dashboard must work as static HTML (no server-side rendering)
- NFR-4: Monitor script must handle API failures gracefully (exit code 1)

### Constraints
- GitHub Actions secrets: `DISCORD_WEBHOOK_URL` (required), Cloudflare (optional)
- GitHub Pages: `gh-pages` branch
- Model classification based on keyword patterns in model ID
