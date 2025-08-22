# Uptime Statuspage — Lightweight Site + Automated Health Checks

**What it does:** Publishes a simple static **status page** (GitHub Pages) and runs scheduled health checks via **GitHub Actions** (HTTP 200/latency), updating a JSON history and badges.  
**Who it’s for:** SMBs that want transparent uptime without managing a monitoring stack.

## Outcomes
- Public status page with current service health and uptime badges
- Daily/5-minute checks with a rolling history JSON

## Prerequisites
- GitHub repo with Pages enabled
- Endpoints to check (URLs)

## Quick Start
1. **Create site:**
   - `site/index.html` with your services and placeholders for badges.
2. **Add workflow:** `.github/workflows/uptime.yml`
   ```yaml
   name: Uptime Checks
   on:
     schedule: [{ cron: "*/5 * * * *" }]
     workflow_dispatch:
   jobs:
     ping:
       runs-on: ubuntu-latest
       steps:
         - uses: actions/checkout@v4
         - name: Check endpoints
           run: |
             python - <<'PY'
             import json, os, time, urllib.request
             endpoints = [
               {"name":"Website","url":"https://example.com"},
               {"name":"Client Portal","url":"https://portal.example.com"}
             ]
             os.makedirs("output", exist_ok=True)
             hist_path = "output/uptime-history.json"
             try:
               hist = json.load(open(hist_path))
             except: hist = []
             ts = int(time.time())
             for ep in endpoints:
               try:
                 t0=time.time(); code=urllib.request.urlopen(ep["url"], timeout=15).getcode(); dt=int((time.time()-t0)*1000)
                 status="up" if code==200 else f"code-{code}"
               except Exception as e:
                 status="down"; dt=None
               hist.append({"ts":ts,"name":ep["name"],"url":ep["url"],"status":status,"ms":dt})
             json.dump(hist[-5000:], open(hist_path,"w"))
             PY
         - name: Commit results
           run: |
             git config user.name "github-actions"
             git config user.email "actions@github.com"
             git add output/uptime-history.json
             git commit -m "update uptime" || echo "no changes"
             git push

3. Enable Pages: Settings → Pages → Branch = main → /site.
4. Badges: Add shields or simple text showing last status (optional JS reads the JSON).

Outputs / Deliverables
site/index.html (status page)
output/uptime-history.json (rolling results)
screenshots/pages-enabled.png, screenshots/checks-passing.png

Evidence (Screenshots)
GitHub Pages live site
Actions run log showing checks for each endpoint

Notes
Keep endpoints lightweight (HTTP GET). For auth’d checks, add synthetic token/ping endpoints.

Outcome (example)
Published a status page in under an hour; automated 5-minute checks and a rolling uptime history for two critical services.
