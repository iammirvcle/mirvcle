# Cost Guard — Budgets, Tags, and Idle Resource Report (Azure + AWS)

**What it does:** Prevents surprise bills by enforcing budgets/alerts, tag governance, and reporting idle resources to clean up.  
**Who it’s for:** SMBs with growing cloud spend and no FinOps practice yet.

## Outcomes
- Monthly budget with alerts at 50/80/100%
- Required/auto tags (Env, Owner, CostCenter)
- CSV of idle resources to remove (VMs stopped, unattached disks, old snapshots)

## Prerequisites
- Access to Azure and/or AWS consoles
- Read rights for billing/cost and resource listings

## Quick Start
1. **Budgets**
   - Azure: Cost Management → **Budgets** → create `$X` monthly budget with email action.
   - AWS: Billing → **Budgets** → create cost budget with 50/80/100% alerts (email via SNS).
   - Save screenshots to `screenshots/budgets/`.
2. **Tags (governance)**
   - Azure Policy assignments for `Require/Append` tags (Env/Owner/CostCenter).
   - AWS: enable **Config** rule(s) and/or SCPs for tag requirements.
   - Save compliance screenshots.
3. **Idle report**
   - Export stopped/unused VMs, unattached disks, aged snapshots (console exports or CLI if available).
   - Save CSVs to `output/idle-resources-azure.csv` and `output/idle-resources-aws.csv`.
4. Compile `output/Cost-Guard-Report.md` with recommended deletions or downsizing.

## Outputs / Deliverables
- `output/Cost-Guard-Report.md` (summary + actions)
- `output/idle-resources-azure.csv`, `output/idle-resources-aws.csv`
- `screenshots/budgets/*`, `screenshots/tag-compliance/*`

## Evidence (Screenshots)
- Budget definitions + alert recipients
- Tag compliance / policy assignments
- Sample idle resource list

## Notes
- Start with **read-only** policies; switch to enforcement after 1–2 weeks.

## Outcome (example)
Cut projected monthly spend by ~18% by removing idle resources and enforcing tags tied to chargeback.

