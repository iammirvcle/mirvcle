# Intune Device Baseline — BitLocker, Defender, Firewall, Updates, Apps

**What it does:** Deploys a practical Windows 10/11 baseline with **BitLocker**, **Defender AV**, **Firewall on**, **Update rings**, and a **standard app set** (winget), plus basic compliance reporting.  
**Who it’s for:** SMBs standardizing Windows endpoints quickly.

## Outcomes
- Encrypted, protected devices with consistent policies
- Compliance visibility and faster, repeatable builds

## Prerequisites
- Intune/Microsoft Endpoint Manager (e.g., M365 Business Premium)
- At least 1 test device enrolled (Autopilot optional)

## Quick Start
1) **Compliance Policy** (Devices → Compliance)
   - Require **BitLocker** = On
   - Require **Secure Boot** = On (if hardware supports)
   - Antivirus = On & up to date
   - Password/PIN required
   - **Deliverable:** export settings (JSON) to `templates/Compliance.json`

2) **Configuration Profiles** (Devices → Configuration)
   - **BitLocker** (Settings catalog): OS drive encryption enabled; store keys in AAD.
   - **Defender**: real-time protection, cloud protection, periodic scans.
   - **Firewall**: Domain/Private/Public profiles **Enabled**.
   - **Deliverable:** export each profile to `templates/*.json`, screenshots when **Succeeded**.

3) **Update Rings** (Windows updates for Business)
   - Create a ring (e.g., **Pilot**): quality updates 7 days, feature updates 14 days; deadlines as per policy.
   - **Deliverable:** screenshot of ring settings and device assignment.

4) **Apps (standard set)**
   - Use your **winget** installer (from your repo) or add apps via **Win32/Microsoft Store**:
     - Example set: 7-Zip, Edge/Chrome, VS Code, Teams, Adobe Reader.
   - **Deliverable:** `templates/AppList.md` + install status screenshot.

5) **Assignments & Scope**
   - Assign profiles/rings/apps to a pilot group (5–10 devices), monitor **Device status** until **Succeeded**.

6) **Validate on device**
   - **BitLocker:** `manage-bde -status` (C: locked, key escrow in AAD).
   - **Defender:** Security settings show ON & updated.
   - **Firewall:** all profiles enabled.
   - **Updates:** ring applies; pending updates within policy.
   - **Apps:** installed.

## Outputs / Deliverables
- `templates/Compliance.json`, `templates/*Profiles.json`, `templates/AppList.md`
- `output/Compliance-Report.csv` (export device compliance)
- `screenshots/` — profile success, BitLocker status, Update ring, Company Portal installs

## Evidence (Screenshots)
- Intune policy **Device status** = Succeeded
- Device `manage-bde -status`
- Company Portal (installed apps)

## Notes
- Stage deployment: **Pilot** group first, then expand.
- Keep a small **Exception** group for edge cases.

## Outcome (example)
Brought 8 pilot devices to compliant state (BitLocker + AV + Firewall) in one afternoon; reduced build time with a standard app set via winget/Company Portal.
