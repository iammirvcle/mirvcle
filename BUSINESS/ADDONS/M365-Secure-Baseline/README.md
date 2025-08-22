# Microsoft 365 Secure Baseline — MFA, Legacy Auth, Basic CA

**What it does:** Establishes a tenant-wide secure baseline with **MFA**, blocks **legacy authentication**, and (optionally) applies a simple **Conditional Access** policy with a safe break-glass pattern.  
**Who it’s for:** SMBs that need fast identity hardening without complex tooling.

## Outcomes
- MFA enforcement for user sign-ins (Security Defaults **or** CA lite)
- Legacy auth (basic auth/IMAP/POP/SMTP Auth where applicable) blocked
- Documented break-glass account and monitoring

## Prerequisites
- Global Admin role in the tenant
- A dedicated **break-glass** account with a long, rotated password (store securely)

## Quick Start
### Option A — **Security Defaults** (fastest)
1. **Entra admin center** → Tenant properties → **Manage security defaults** → **Enable**.
2. Communicate MFA enrollment steps to users (Authenticator app).
3. **Deliverable:** screenshot of Security Defaults “Enabled”.

### Option B — **Conditional Access (lite)** (more control)
1. **Create break-glass account** (exclude from CA, monitor sign-ins).
2. **Conditional Access → New policy:** “Require MFA for all users”
   - **Users:** All users **except** break-glass & service accounts
   - **Cloud apps:** All cloud apps
   - **Conditions:** (optional) exclude trusted locations for staged rollout
   - **Grant:** Require **MFA**
   - **Enable:** On
3. **Block legacy auth**
   - **Azure AD → Security → Conditional Access → New policy:** “Block legacy auth”
   - Condition: **Client apps** → select **Other clients** and **Legacy authentication clients**
   - Grant: **Block access**
   - Enable: On
   - (Alternatively, disable legacy protocols in M365 admin where applicable)
4. **Test flow**
   - Test user without MFA should be **prompted** for MFA; with MFA enrolled, sign-in succeeds.
   - Legacy-auth client attempts should be **blocked**.
5. **Deliverables:** policy screenshots + sign-in logs (success/bl
