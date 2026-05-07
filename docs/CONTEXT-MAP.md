## Module Mappings

- [x] `monitor.py` | Core: fetch OpenRouter free models, diff, notify, persist | Validated: 2026-04-30
- [x] `models.json` | Data: current sorted list of free model IDs | Validated: 2026-04-30
- [x] `CHANGELOG.json` | Data: change history (capped 100 entries) | Validated: 2026-04-30
- [x] `MODELS.md` | Generated: human-readable model list grouped by provider | Validated: 2026-04-30
- [x] `dashboard/index.html` | UI: dashboard shell (title, charts, table, footer) | Validated: 2026-04-30
- [x] `dashboard/app.js` | Logic: charts, DataTable, filters, change history renderer | Validated: 2026-04-30
- [x] `dashboard/styles.css` | Styling: badges, cards, animations, responsive | Validated: 2026-04-30
- [x] `dashboard/README.md` | Docs: dashboard usage and customization guide | Validated: 2026-04-30
- [x] `index.html` | UI: landing page with stats, features, CTA | Validated: 2026-04-30
- [x] `.github/workflows/monitor.yml` | CI/CD: cron (6h), monitor run, commit, GitHub Pages deploy | Validated: 2026-04-30
- [x] `requirements.txt` | Deps: requests, pytz | Validated: 2026-04-30
- [x] `README.md` | Docs: project overview, setup instructions | Validated: 2026-04-30
- [x] `AGENTS.md` | Config: workflow rules, AI directives, token budgets | Validated: 2026-04-30

## File Responsibilities

| File | Role |
|------|------|
| `monitor.py` | API fetch, diff, Discord notify, JSON/MD write |
| `dashboard/app.js` | MODEL_TYPE_PATTERNS classification, Chart.js init, DataTable, provider filters |
| `dashboard/index.html` | Dashboard layout, CDN imports, DOM containers |
| `index.html` | Landing page, live stats from models.json |

## Validation Status

- `monitor.py` executed locally 2026-04-30: 29 free models detected ✅
- `models.json` populated with 29 entries ✅
- `CHANGELOG.json` initialized with first entry ✅
- `MODELS.md` regenerated ✅
- Dashboard/landing page: updated branding, not browser-tested yet ❌ → verified live on GitHub Pages ✅
- GitHub Actions workflow: monitor + GitHub Pages deploy ✅ | Cloudflare job removed ✅
- Discord notification: delivered ✅
- GitHub Pages: https://skyeagle888.github.io/openrouter-free-models-monitor/ ✅
