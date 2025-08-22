# Backup & Restore Drill — RPO/RTO Verification

**What it does:** Proves backups are usable by restoring a sample and verifying hashes; records **RPO** (data staleness) and **RTO** (time to restore).  
**Who it’s for:** SMBs needing proof of recoverability for audits/insurance.

## Outcomes
- Documented RPO/RTO numbers
- Evidence of successful restore + checksum validation

## Prerequisites
- Access to the backup tool or a target folder to back up (robocopy/VSS acceptable)
- PowerShell (admin) for hash verification

## Quick Start
1. **Define dataset** (e.g., `C:\Data\FinanceSample`).
2. **Backup step:** copy to `D:\Backups\FinanceSample_YYYYMMDD` with robocopy (retain timestamps).
3. **Restore step:** restore to `C:\RestoreTest\FinanceSample`.
4. **Validate:** compute SHA-256 hashes on original vs restore; compare.
5. **Record times:** start/end per step to calculate RPO/RTO.
6. Save results to `output/restore-validation.csv` and `output/Findings.md`.

## Outputs / Deliverables
- `output/backup.log`, `output/restore.log`
- `output/restore-validation.csv` (filename, original hash, restored hash, match)
- `output/Findings.md` (RPO/RTO, issues, follow-ups)

## Evidence (Screenshots)
- Backup job success screen (or logs)
- Restore destination folder + sample files
- Hash comparison result

## Notes
- Always test restores to a **non-production** path.

## Outcome (example)
Restored sample data in 12 minutes (RTO) with 0 mismatches; last backup was 20 hours old (RPO), within policy.

