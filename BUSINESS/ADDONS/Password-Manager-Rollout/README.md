# Password Manager Rollout — Policy, Guides, Adoption Plan

**What it does:** Delivers an org-wide rollout of a modern password manager (Bitwarden/1Password), including policy, user guides, import steps, and staged adoption.  
**Who it’s for:** SMBs improving credential hygiene and MFA usage.

## Outcomes
- Approved policy with MFA enforced for vault access
- Staff onboarded in phases with import instructions and support tips

## Prerequisites
- Chosen platform account (Bitwarden/1Password/etc.)
- Email list or IdP group for inviting users

## Quick Start
1. **Decide policy** (templates provided):
   - Minimum length 14+, generator defaults, 2FA required for vault, shared collections usage.
2. **Create org** and **enforce 2FA** for all users.
3. **Prepare imports**:
   - Export CSV from browsers/legacy managers (use `templates/sample-import.csv`).
4. **Communications** (templates provided):
   - Announcement, enrollment steps, support channels.
5. **Rollout phases**:
   - Phase 1 (IT/Admins), Phase 2 (Leads), Phase 3 (All hands).
6. **Verify**:
   - Admin dashboard shows enrolled users & vault 2FA enabled.
   - Spot-check shared collections permissions.

## Outputs / Deliverables
- `templates/Policy.md`, `templates/User-Guide.md`, `templates/Change-Comms.md`
- `output/Adoption-Tracker.csv` (invited, enrolled, pending)
- `screenshots/admin-2fa-enforcement.png`, `screenshots/import-success.png`

## Evidence (Screenshots)
- Admin “Enforce 2FA” setting
- User enrollment / app sign-in with 2FA
- Successful import confirmation

## Notes
- Keep break-glass access documented and stored securely.
- Provide a **lost-device** / recovery SOP in `templates/`.

## Outcome (example)
Onboarded 95% of users in 10 days; enforced 2FA for vault access and migrated >800 saved credentials with minimal disruption.

