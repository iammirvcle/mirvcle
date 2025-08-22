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
   - Require **Secure Boot** = On (if hardwa
