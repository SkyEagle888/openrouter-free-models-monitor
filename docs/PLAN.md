## Implementation Roadmap

### Phase 1: Core Adaptation ✅
- [x] P1-1: Change `API_URL` in `monitor.py` to OpenRouter endpoint
- [x] P1-2: Add `:free` filter in `fetch_models()`
- [x] P1-3: Update Discord message templates ("NVIDIA" → "OpenRouter")
- [x] P1-4: Update `update_markdown()` title and labels
- [x] P1-5: Fix deprecation warning (`datetime.utcnow()` → `datetime.now(UTC)`)
- [x] P1-6: Fix Windows UTF-8 stdout encoding
- [x] P1-7: Validate locally (`python monitor.py` → 29 models detected)

### Phase 2: Data Reset ✅
- [x] P2-1: Reset `models.json` to `[]`
- [x] P2-2: Reset `CHANGELOG.json` to `{"changes": []}`

### Phase 3: Dashboard Rebranding ✅
- [x] P3-1: Update `dashboard/index.html` (title, header, subtitle, footer)
- [x] P3-2: Update `dashboard/app.js` (MODEL_TYPE_PATTERNS: instruct/vision/reasoning/code/base)
- [x] P3-3: Update `dashboard/styles.css` (badge styles for new categories)
- [x] P3-4: Update `dashboard/README.md` (full rewrite)

### Phase 4: Landing Page & CI/CD ✅
- [x] P4-1: Rewrite `index.html` landing page for OpenRouter
- [x] P4-2: Update `monitor.yml` workflow name, cron schedule (every 6h), Cloudflare project name

### Phase 5: Documentation ✅
- [x] P5-1: Expand `README.md` with setup instructions and structure

### Phase 6: Deployment ✅
- [x] P6-1: Commit and push all changes to GitHub
- [x] P6-2: Manually trigger GitHub Actions workflow to verify
- [x] P6-3: Enable GitHub Pages (`gh-pages` branch)
- [x] P6-4: Verify Discord notification delivery
- [x] P6-5: Verify dashboard loads on GitHub Pages

### Phase 7: Optional
- [x] ~~P7-1: Configure Cloudflare Pages deployment~~ → Cancelled: Cloudflare deployment removed

### Phase 8: Discord Silence on No-Change ✅
- [x] P8-1: Skip Discord notification when no changes detected (initial run still notifies)
- [x] P8-2: Update README.md and ARCHITECTURE.md to document silence behavior
- [x] P8-3: Validate locally with no-change scenario (`python monitor.py` → Discord skipped)
