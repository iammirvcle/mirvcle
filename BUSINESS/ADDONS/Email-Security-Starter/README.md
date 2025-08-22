# Email Security Starter — SPF, DKIM, DMARC (Alignment & Reports)

**What it does:** Sets up sender authentication and alignment (SPF/DKIM/DMARC) to reduce spoofing/phishing, and proves it with screenshots and a simple report.  
**Who it’s for:** SMBs on M365/Google/workmail that need a fast improvement without new tooling.

## Outcomes
- SPF + DKIM enabled and aligned for your primary domain
- DMARC policy rolled out safely (p=none → quarantine → reject) with evidence

## Prerequisites
- Access to DNS for your domain (TXT/CNAME records)
- Admin rights in your email platform (e.g., Microsoft 365, Google Workspace)
- A reporting mailbox (e.g., `dmarc-reports@yourdomain.com`)

## Quick Start
1) **SPF (TXT)**
   - If on Microsoft 365:  
     `v=spf1 include:spf.protection.outlook.com -all`
   - If on Google Workspace:  
     `v=spf1 include:_spf.google.com -all`
   - If you have other senders (Mailchimp, Zendesk, etc.), add their documented `include:` mechanisms.  
   - **Deliverable:** add/confirm TXT at root (`@`). Screenshot DNS record.

2) **DKIM**
   - Enable DKIM in your mail platform; it will give you **two CNAME** records.
     - M365: create two CNAMEs, typically  
       `selector1._domainkey → selector1-yourdomain-com._domainkey.<initial-domain>`  
       `selector2._domainkey → selector2-yourdomain-com._domainkey.<initial-domain>`
   - Wait for DNS to propagate, then click **Enable**.  
   - **Deliverable:** DKIM “Enabled” screenshot.

3) **DMARC (TXT at `_dmarc`)**
   - Start safe:  
     `v=DMARC1; p=none; rua=mailto:dmarc-reports@yourdomain.com; fo=1; adkim=s; aspf=s`
   - After 1–2 weeks of clean reports, raise to `p=quarantine`, then `p=reject`.  
   - **Deliverable:** TXT record screenshot + final policy decision.

4) **Validate alignment**
   - Send a test email to an external mailbox (e.g., Gmail), open **Show original** and confirm:
     - **SPF:** pass (domain = yourdomain.com)
     - **DKIM:** pass (d=yourdomain.com)
     - **DMARC:** pass (policy and aligned identifiers)
   - **Deliverable:** Screenshot of passes.

## Outputs / Deliverables
- `templates/dns-records.md` — fill with your exact SPF/DKIM/DMARC records
- `output/dmarc-rollout-plan.md
