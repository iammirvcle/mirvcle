# Windows Event Forwarding (WEF) Starter — Centralize Security Logs

**What it does:** Sets up Windows Event Forwarding to collect Security event logs (e.g., 4624/4625) from endpoints to a single collector — no paid SIEM needed.  
**Who it’s for:** SMBs needing centralized visibility quickly.

## Outcomes
- Central collector receiving Security logs from pilot endpoints
- Daily digest (failed logons/top IPs) you can review without SIEM

## Prerequisites
- One Windows Server (collector) and 3–5 Windows endpoints
- Admin rights on all machines

## Quick Start
1. **Collector setup:**
   - On the server, enable **Windows Event Collector** service.
   - Configure a **Source-initiated subscription** (Subscriptions → Create).
2. **GPO for clients:**
   - Create a GPO enabling **Windows Remote Management (WinRM)** and point to the collector.
   - Link GPO to the OU containing pilot endpoints.
3. **Subscription filter:**
   - Include **Security** log; Event IDs `4624,4625` to start.
4. **Verify flow:** events appear on the collector under **Forwarded Events**.
5. (Optional) Use your **Failed Logons** summarizer daily to produce `output/failed-logons-summary.md`.

## Outputs / Deliverables
- `templates/wef-gpo-settings.md` — settings snapshot
- `output/failed-logons-summary.md` (optional daily)
- `screenshots/collector-forwarded-events.png`

## Evidence (Screenshots)
- Subscriptions list
- Forwarded Events with sample 4624/4625 entries

## Notes
- Start with a small scope; expand after verifying network/firewall exceptions.

## Outcome (example)
Established centralized log visibility for 5 endpoints in under 2 hours; delivered daily failed-login summaries.

