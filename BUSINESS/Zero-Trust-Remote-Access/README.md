# Zero-Trust Remote Access — Remove Exposed RDP/SSH, Add JIT/MFA

**What it does:** Eliminates public RDP/SSH, enforces **Just-In-Time (JIT)** or bastion access, and requires **MFA** via IdP/VPN. Documents a safe **break-glass** path.  
**Who it’s for:** SMBs with remote admins/contractors and exposed management ports.

## Outcomes
- No public RDP/SSH listeners
- Documented, audited path to remote admin with MFA/JIT

## Prerequisites
- Cloud console access (Azure and/or AWS)
- IdP with MFA (Entra ID / Okta) or a VPN that supports MFA

## Quick Start (Azure)
1. **Shut the doors**:
   - NSG inbound rules: remove `0.0.0.0/0` for `3389`/`22`; restrict to VPN/bastion subnets only.
2. **Choose access method**:
   - **Azure Bastion** for portal-initiated RDP/SSH (no public IP on VMs), **or**
   - **Defender for Cloud JIT**: enable JIT on target VMs; open ports *only* on approved requests for limited time/IP.
3. **MFA**:
   - Require MFA via Conditional Access for admin sign-ins to the portal/Bastion.
4. **Break-glass**:
   - Maintain one documented path (e.g., privileged workstation inside VPN) with monitored usage.

## Quick Start (AWS)
1. **Shut the doors**:
   - Security Groups: remove `0.0.0.0/0` on `22`/`3389`.
2. **Choose access method**:
   - **SSM Session Manager** for shell access (no inbound SG needed), **or**
   - Bastion/EC2 Instance Connect with IP allowlists.
3. **MFA**:
   - Enforce MFA for admin users/roles; consider IAM Identity Center for SSO + MFA.
4. **Break-glass**:
   - One monitored emergency role with short-lived credentials.

## Outputs / Deliverables
- `templates/Access-Policy.md` (JIT/Bastion/SSM path, who approves, time windows)
- `screenshots/rules-before-after/*.png` (open ports removed)
- `output/Access-Review.md` (systems migrated, exceptions, target date to close)

## Evidence (Screenshots)
- NSG/SG rules **before/after**
- JIT request approval screen or SSM session log
- CA policy or MFA enforcement screen

## Notes
- Track exceptions with an **expiry date** and owner; re-review monthly.

## Outcome (example)
Eliminated public RDP/SSH across the tenant and moved admins to JIT/Bastion/SSM with MFA; reduced exposure while preserving operational access.
