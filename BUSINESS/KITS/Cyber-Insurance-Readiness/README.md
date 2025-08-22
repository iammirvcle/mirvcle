# Cyber Insurance Readiness — Controls Report & Remediation Checklist

**What it does:** Produces a consolidated report proving basic controls (MFA, AV/Defender, Firewall, Patch, Backups) and a prioritized remediation checklist.  
**Who it’s for:** SMBs preparing for cyber-insurance questionnaires or renewal.

## Outcomes
- Single report showing control status with evidence links
- Clear “fix first” list that aligns to common insurer questionnaires

## Prerequisites
- Windows device with PowerShell 5.1+ or 7.x (admin)
- Access to Microsoft 365/Azure portal (for MFA/identity checks)

## Quick Start
1. Run the following **local checks** (use your internal tools or the suggested mirvcle labs):
   - Defender/Firewall posture → from **DefenderFirewall-Audit**
   - Patch age snapshot → **PatchCompliance-Snapshot**
   - Critical services health → **Services-Health**
   - Failed logons snapshot → **EventLog-FailedLogons**
   - (Optional) File integrity baseline → **FileIntegrity-Baseline**
2. Save all outputs into `./output/controls/`.
3. Document **MFA** status for admin accounts (screenshot from Entra/M365 admin).
4. Record **Backup** status (tool used, last test date, sample restore evidence).
5. Fill `templates/Readiness-Checklist.md` (included) and compile `output/Readiness-Report.md`.

## Suggested Steps (example commands)
- Defender/Firewall:
  - Export CSV + Findings.txt from your tool into `output/controls/defender-firewall.csv`.
- Patch age:
  - Export `patch-snapshot.csv` to `output/controls/`.
- Services health:
  - Export `services-health.csv` to `output/controls/`.
- Failed logons:
  - Export `failed-logons.csv` to `output/controls/`.
- Backup:
  - Include backup tool report or `backup-restore-validation.md`.

## Outputs / Deliverables
- `output/Readiness-Report.md` — control status + links to evidence
- `output/controls/*.csv|md` — raw evidence
- `templates/Readiness-Checklist.md` — prioritized remediation
- `screenshots/` — MFA status, backup success, policy settings

## Evidence (Screenshots)
- M365/Entra admin — **MFA enforcement** screen
- Windows Security baseline — Defender/Firewall ON
- Backup job success + test restore verification

## Notes
- Scope this run to a **pilot** group first (e.g., 5–10 devices), then scale.

## Outcome (example)
Delivered a readiness report within 1 business day; flagged outdated signatures on 2 devices and 1 admin without MFA; provided remediation with owners/dates.

