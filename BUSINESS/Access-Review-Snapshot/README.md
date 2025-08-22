# Access Review Snapshot — Azure AD Roles & Local Admins

**What it does:** Exports Azure AD privileged roles, key group memberships, stale user accounts, and local admin membership on sample endpoints.  
**Who it’s for:** SMBs running quarterly access reviews (least-privilege).

## Outcomes
- CSVs for privileged roles and local admins per device
- List of dormant/inactive accounts to disable or remove

## Prerequisites
- Entra ID/M365 admin read access
- Windows device admin rights (for local admin check)

## Quick Start
1. **Azure AD / Entra ID:**
   - Export **Directory roles** and **User assignments** (Portal → Entra ID → Roles & administrators).
   - Save as `output/entra-roles.csv` and `output/entra-role-assignments.csv`.
2. **Groups:**
   - Export members for key groups (`Global Admins`, `Helpdesk`, `VPN Users`). Save to `output/groups-*.csv`.
3. **Stale users:**
   - Export last sign-in report (Sign-in logs or Users list with last activity). Save to `output/stale-users.csv`.
4. **Local admins (endpoints):**
   - Run a local admin membership export on sample devices and save as `output/local-admins-<device>.csv`.
5. Consolidate findings into `output/Access-Review-Findings.md` and tag risky entries.

## Outputs / Deliverables
- `output/entra-roles.csv`, `output/entra-role-assignments.csv`
- `output/groups-*.csv`, `output/stale-users.csv`
- `output/local-admins-*.csv`
- `output/Access-Review-Findings.md` with remediation list

## Evidence (Screenshots)
- Entra **Roles & administrators** page
- Example local **Administrators** group membership output

## Notes
- Keep at least one **break-glass** account documented and monitored.

## Outcome (example)
Removed 3 dormant accounts and 2 unnecessary local admins; reduced standing privilege exposure.

