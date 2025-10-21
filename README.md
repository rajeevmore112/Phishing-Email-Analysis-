### Phishing Email Analysis Report  
Author: Rajeev More  
Date: October 21, 2025  

## Objective
For this task I was asked to examine a set of suspicious emails and identify indicators of phishing.  
The goal was to practice reading email headers, spotting spoofed domains, recognizing social-engineering lures, and suggesting basic mitigation steps. 
This exercise helped me improve my practical skills in email forensics and phishing awareness.

## Disclaimer — Synthetic Samples:
All email samples in this repository are artificially generated (AI synthetic) for learning purposes. They do not contain real user data or active malicious code. 
I created and analyzed them only to learn and document phishing techniques. Still, treat any email links or attachments with caution in a real environment.

## Tools and Resources Used

- MXToolbox Email Header Analyzer - to check SPF/DKIM/DMARC and trace the delivery path.  
- Hook Security - where I referenced example formats and phishing patterns.
- Claude AI - To generate Synthetic Mails

## Quick Summary

I analyzed 10 synthetic phishing email samples. Most of them tried to imitate big companies (PayPal, Microsoft, banks, delivery services, etc.) 
and used urgency or fear to make the recipient act quickly.

|Sr | Imitated      | Auth Result                     | Theme                   | Risk        |
|---|---------------|---------------------------------|-------------------------|-------------|
| 1 | PayPal        | SPF Fail                        | Account suspension      | High        |
| 2 | Microsoft 365 | DKIM None, SPF Softfail         | Password expiration     | High        |
| 3 | Wells Fargo   | DMARC Fail                      | Fraud transaction       | High        |
| 4 | Amazon        | SPF Fail, DKIM Fail             | Fake order              | High        |
| 5 | IRS           | SPF None, DMARC None            | Tax notice scare        | High        |
| 6 | LinkedIn      | SPF Softfail                    | Connection/job lure     | Medium–High |
| 7 | Google Drive  | SPF Fail, DKIM Fail, DMARC Fail | Shared file lure        | High        |
| 8 | DHL           | SPF Neutral                     | Customs fee scam        | Medium–High |
| 9 | Apple         | SPF Fail, DMARC Fail            | Account disabled threat | High        |
| 10 | DocuSign     | SPF Softfail                    | Fake signing request    | High        |

## Detailed Findings (per sample)

### Sample 1 — Fake PayPal Account Suspension
- From: `service@paypa1-secure.com`  
- Header: `spf=fail`  
- Why suspicious: Domain looks like PayPal but uses a “1” instead of “l”. The message pressures the user with a 24-hour deadline and links to an HTTP address.  
- Risk: High  

### Sample 2 — Fake Microsoft 365 Password Expiration
- From: `no-reply@microsoft-services.net`  
- Header: `dkim=none; spf=softfail`  
- Why suspicious: The domain is not `microsoft.com`. It asks to update password immediately — a common credential harvesting trick.  
- Risk: High  

### Sample 3 — Fake Wells Fargo Alert
- From: `alerts@wellsfargo-online.com`  
- Header: `spf=neutral; dmarc=fail`  
- Why suspicious: Non-official domain plus urgent money transaction claim. Uses fear to force quick action.  
- Risk: High  

### Sample 4 — Fake Amazon Order Confirmation
- From: `order-update@amazon-services.co`  
- Header: `spf=fail; dkim=fail`  
- Why suspicious: Domain is not `amazon.com`. High-value item mentioned to create panic.  
- Risk: High  

### Sample 5 — Fake IRS Tax Notice
- From: `notices@irs-gov.org`  
- Header: `spf=none; dmarc=none`  
- Why suspicious: Real IRS uses `irs.gov`. The email threatens penalties and directs to a fake portal.  
- Risk: High  

### Sample 6 — Fake LinkedIn Connection Notification
- From: `notifications@linkedin-mail.net`  
- Header: `spf=softfail; dkim=none`  
- Why suspicious: Domain is not LinkedIn’s official domain and it lures with job opportunities or HR contacts.  
- Risk: Medium–High
- 
### Sample 7 — Fake Google Drive Share Notification
- From: `drive-noreply@googledrive-share.com`  
- Header: `spf=fail; dkim=fail; dmarc=fail`  
- Why suspicious: Looks like Google Drive but domain is different. Shared-file scams often aim to steal credentials or trick users into downloading malware.  
- Risk: High  

### Sample 8 — Fake DHL Package Delivery
- From: `deliveryinfo@dhl-express.net`  
- Header: `spf=neutral; dkim=none`  
- Why suspicious: Requests a small customs fee via email link — classic payment scam.  
- Risk: Medium–High  

### Sample 9 — Fake Apple ID Suspension
- From: `appleid@apple-support.com`  
- Header: `spf=fail; dmarc=fail`  
- Why suspicious: Domain is not Apple’s. Threatens data loss to force immediate action.  
- Risk: High  

### Sample 10 — Fake DocuSign Document Request
- From: `dse@docusign-notify.net`  
- Header: `spf=softfail; dkim=none; dmarc=none`  
- Why suspicious: DocuSign lookalike domain and urgent signing request. Could harvest credentials or deliver malware.  
- Risk: High  

## Common Patterns I Observed

- Typosquatting / domain tricks — small changes in domain names to confuse users.  
- Authentication failures — many samples showed SPF/DKIM/DMARC problems, which usually mean the sender was forged.  
- Urgency or threats — a lot of samples tried to scare users into acting immediately.  
- Generic greetings — not using the recipient’s real name.  
- Links to non-official sites — often asking for login, payment, or document signing.

## Practical Recommendations 

- Always check headers for `SPF`, `DKIM`, and `DMARC` results before trusting a message.  
- Hover over links to see the real URL — but do not click suspicious links.  
- Use VirusTotal or urlscan.io to inspect links if needed (do this in a safe environment).  
- Turn on Multi-Factor Authentication (MFA) wherever possible.  
- Report phishing emails to the relevant teams or the impersonated brand (e.g., PayPal, Amazon).  
- Run regular awareness sessions for colleagues — most attacks rely on human error.

## References & Resources

- Hook Security Phishing Email Examples: https://www.hooksecurity.co/phishing-email-examples  
- MXToolbox Email Header Analyzer: https://mxtoolbox.com/EmailHeaders.aspx  
- Claude AI: https://claude.ai/chat/e22212a7-1d85-47f5-b274-60e84f2e29f

## Repository contents

Phishing-Email-Analysis/
├── README.md ← (this report)
├── Phishing_Samples_Data.txt
├── screenshots
    ├── Mail samples from HookSecurity
