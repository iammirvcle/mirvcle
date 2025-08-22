# Cloud Tag Governance — Azure + AWS (Require, Append, Report)

**What it does:** Enforces and reports on required resource tags (e.g., `Environment`, `Owner`, `CostCenter`) across **Azure** and **AWS** so costs are attributable and cleanup is easy.  
**Who it’s for:** SMBs wanting basic governance and cost hygiene with minimal tooling.

## Outcomes
- Required/auto-applied tags at RG/Subscription (Azure) and Account (AWS)
- Monthly tag compliance report with remediation list

## Prerequisites
- Azure RBAC rights to assign Policy at RG/Subscription
- AWS permissions to create Config rules and (optionally) Organizations SCPs

## Quick Start (Azure)
1. **Choose tags**: `Environment`, `Owner`, `CostCenter`.
2. **Assign built-in policies** (Portal → Policy → **Definitions**):
   - **Require a tag and its value on resources**
   - **Append a tag and its default value**
3. **Assignments** (scope = Resource Group or Subscription):
   - Require: `Environment = Lab` (example)
   - Append: `CostCenter = 1000` (default)
4. **Compliance**: Policy → **Compliance** → Export non-compliant resources to CSV.
5. **(Optional) Remediation**: Create a remediation task for append/modify policies.

## Quick Start (AWS)
1. **AWS Config** → **Rules** → **Add rule**:
   - Managed rule: `required-tags`
   - Parameters: `tag1Key=Environment, tag2Key=Owner, tag3Key=CostCenter`
2. **(Optional) Organizations SCP** (guardrail at OU/Account):
   ```json
   {
     "Version": "2012-10-17",
     "Statement": [{
       "Sid": "DenyCreateWithoutTags",
       "Effect": "Deny",
       "Action": ["ec2:RunInstances","s3:CreateBucket","rds:CreateDBInstance","lambda:CreateFunction","*"],
       "Resource": "*",
       "Condition": {
         "Null": { "aws:RequestTag/Environment": "true" }
       }
     }]
   }

