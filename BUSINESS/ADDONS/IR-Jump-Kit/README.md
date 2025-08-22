# IR Jump Kit — First-Hour Triage (Windows)

**What it does:** A portable, repeatable first-hour playbook for Windows: collect key system info, event logs, network/process snapshots, and file-integrity diffs. Produces a clean evidence bundle with a chain-of-custody note.  
**Who it’s for:** SMBs that need a calm, consistent start to incident response without heavy tools.

## Outcomes
- Standardized evidence bundle within ~15 minutes
- Clear handoff artifacts for deeper investigation

## Prerequisites
- USB or secure share with this kit
- PowerShell 5.1+ (run as Administrator)

## Quick Start
1. **Prepare**: Copy `scripts/` to a clean USB; verify hashes (`templates/Hashes.txt`).
2. **Contain (if needed)**: Disconnect network cable/Wi-Fi or use your isolation SOP.
3. **Collect** (example commands in `scripts/`):
   - System & user context: `Get-ComputerInfo`, `whoami /groups`, `query user`
   - Running processes & services: `Get-Process`, `Get-Service`
   - Network snapshot: `Get-NetTCPConnection | Select Local*,Remote*,State,OwningProcess`
   - Key event logs (last 48h): Security 4624/4625, Sysmon (if present), Microsoft-Windows-Windows Defender/Operational
   - Scheduled tasks & startup: `Get-ScheduledTask`, registry Run keys
   - File integrity diff (if your FIM baseline exists)
4. **Package**: Save to `output/<HOSTNAME>-<YYYYMMDD-HHMM>/` with subfolders `/logs`, `/events`, `/screens`.
5. **Document**: Fill `templates/Chain-of-Custody.md` (who/when/what), and `Findings.md` (initial observations).

## Outputs / Deliverables
- `output/<HOST>/system-info.txt`, `processes.csv`, `services.csv`, `net-ports.csv`
- `events/security-4624_4625.evtx` (and exported CSV)
- `fim/report.json` (if applicable)
- `Findings.md` + `Chain-of-Custody.md`

## Evidence (Screenshots)
- Timestamped folder tree with artifacts
- Sample event timeline graph (optional Excel/Chart)

## Notes
- Keep collection **non-destructive**; do not kill processes unless containment requires it.
- If forensic imaging is required, escalate to your IR partner per policy.

## Outcome (example)
Assembled first-hour evidence (processes, ports, key events) in 12 minutes; identified suspicious service for follow-up while preserving artifacts.

