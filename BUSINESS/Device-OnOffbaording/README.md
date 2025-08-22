# Device On/Offboarding Pack — Standardized Build & Secure Exit

**What it does:** Provides a repeatable checklist + scripts for clean device onboarding and secure offboarding, with auditable logs.  
**Who it’s for:** SMBs formalizing IT processes.

## Outcomes
- Faster, consistent onboarding (apps, settings, inventory)
- Secure and documented offboarding (data, keys, access)

## Prerequisites
- PowerShell (admin) on the device
- Access to BitLocker recovery keys (if used)
- Your approved app list (winget or offline installers)

## Quick Start
### Onboarding
1. Capture baseline inventory to `output/asset-inventory.csv`.
2. Install standard apps using the provided app list (winget) and log to `output/install-log.txt`.
3. Verify Defender/Firewall/Update settings.
4. Save `output/onboarding-checklist.md` with device owner + date.

### Offboarding
1. Export inventory + user data archive manifest.
2. Remove from groups/Azure AD; disable accounts as per policy.
3. Recover/record BitLocker keys; secure wipe if repurposing.
4. Save `output/offboarding-log.csv`.

## Outputs / Deliverables
- `output/asset-inventory.csv`, `output/install-log.txt`
- `output/onboarding-checklist.md`
- `output/offboarding-log.csv`
- `templates/user-handout.md` (optional)

## Evidence (Screenshots)
- App install log excerpt
- BitLocker key capture (redact secret values)
- Checklist excerpts

## Notes
- Align with HR/legal for offboarding steps and retention.

## Outcome (example)
Reduced setup time by ~45 minutes/device and eliminated missed offboarding steps with an auditable log.

