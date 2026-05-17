# How to Identify and Report a Phishing Email

- **Category:** Security
- **Tier:** Tier 1 (Help Desk)
- **Version:** 1.0
- **Last Updated:** May 2, 2026
- **Last Reviewed:** May 2, 2026
- **Applies To:** All Email Platforms (Outlook, Gmail, Yahoo, Webmail), All Users
- **Difficulty:** L1 (Basic)
- **Estimated Resolution Time:** 5-10 minutes
- **Required Access Level:** User
- **Severity:** P2 (Single User, Degraded — Security Threat Identification)
- **Keywords:** phishing, email, scam, spoof, security, report, suspicious, link, attachment, fraud
- **Prerequisite Knowledge:** Basic email usage, ability to hover over links and check sender addresses

---

## Symptoms

- Email appears to be from a legitimate company (bank, IT department, shipping company, government agency) but feels unusual
- Email creates a sense of urgency: "Your account will be suspended," "Payment required," "Immediate action needed"
- Sender email address looks slightly wrong (e.g., @microsft.com instead of @microsoft.com, @amaz0n.com instead of @amazon.com)
- Email contains links that do not match the displayed text when hovered over
- Unexpected attachment from an unknown or suspicious sender (especially .exe, .zip, .docm, .pdf with unusual name)
- Email requests personal information, login credentials, or payment details
- Email body contains poor grammar, spelling errors, or inconsistent formatting

---

## Common Error Codes

| Code | Meaning |
|------|---------|
| SPF Fail | Sender Policy Framework check failed — email not sent from authorized server |
| DKIM Fail | DomainKeys Identified Mail check failed — email signature invalid |
| DMARC Fail | Domain-based Message Authentication failed — both SPF and DKIM failed |
| Phish Alert | Email flagged by organizational security tool as potential phishing |

---

## Symptom-to-Step Mapping

| If You See This | Skip To |
|-----------------|---------|
| Sender address looks suspicious | Step 1 |
| Email contains links you're unsure about | Step 2 |
| Email creates pressure or urgency | Step 3 |
| Email has unexpected attachments | Step 4 |
| You already clicked a link or entered credentials | Step 7 |

---

## Triage Questions

Before starting troubleshooting, ask the user:

1. "Were you expecting this email, or did it arrive out of the blue?"
2. "Does the email ask you to click a link, open an attachment, or provide personal information?"
3. "Have you already clicked anything or entered any information?"
4. "Does the sender's email address look correct when you examine it closely?"

---

## Quick Checks (30 seconds)

1. Check the sender's actual email address (not just the display name) — does the domain match the company exactly?
2. Hover over any links in the email (do not click) — does the preview URL match where you expect to go?
3. Does the email address you by name, or use generic greetings like "Dear Customer" or "Dear User"?
4. Is there an unexpected attachment? Do not open it — verify with the supposed sender through a different channel
5. Were you expecting this email? If not, treat it as suspicious by default
6. If you believe your account has already been compromised, see: [Account Compromised — Immediate Response Checklist](./account-compromised-checklist.md)

---

## Step-by-Step Resolution

### Step 1: Verify the Sender's Identity
1. Look at the sender's email address carefully, not just the display name
   - A display name may show "IT Support" or "Microsoft" but the actual email could be from a free email service
2. Check for subtle misspellings in the domain:
   - @microsft.com instead of @microsoft.com
   - @amaz0n.com instead of @amazon.com
   - @paypa1.com instead of @paypal.com
   - @company-co.com instead of @company.com
3. Hover over the sender name to reveal the full email address
4. If the email claims to be from someone you know (colleague, manager) but the email address is different from their usual one, contact them through a different channel (phone, messaging app, or a new email to their known address) to verify

**What to tell the user:** "The display name on an email can be anything the sender wants it to be — it's like the return address on an envelope. The actual email address is what matters. Let's check if the sender's real address matches who they claim to be. Legitimate companies never use free email domains like @gmail.com for official communications."

### Step 2: Inspect Links Without Clicking
1. Hover your mouse cursor over any link or button in the email (do not click)
2. Look at the bottom-left corner of your browser or email client — the actual URL destination will appear
3. Check if the URL matches where you expect to go:
   - A legitimate company link should go to that company's official domain
   - A bank link should go to the official bank website
4. Look for these common phishing URL tricks:
   - Mismatched text and destination: Text says "Login to your account" but URL points to an unrelated site
   - Lookalike domains: secure-microsoft.com (real is microsoft.com)
   - URL shorteners: bit.ly, tinyurl.com, ow.ly — these hide the true destination
   - Subdomain tricks: microsoft.com.fake-site.com (the real domain is fake-site.com, not microsoft.com)
5. If unsure about a link, do not click it — instead, manually type the company's known website address into your browser

**What to tell the user:** "Links in emails are like doors — the label on the door might say 'Bank Login' but the door could lead somewhere completely different. By hovering your mouse over a link without clicking, you can see the real destination. If the address doesn't match what you expect, don't enter."

### Step 3: Check for Urgency and Fear Tactics
1. Phishing emails commonly create false urgency to pressure you into acting without thinking
2. Look for these pressure phrases:
   - "Your account will be suspended within 24 hours"
   - "Unauthorized login detected — verify your account immediately"
   - "Payment overdue — click here to avoid late fees"
   - "Your password has expired — update now to avoid losing access"
   - "Security breach detected — confirm your identity"
3. Ask yourself: Would this company really contact me this way for this issue?
   - Banks do not ask for your password or PIN via email
   - IT departments do not request your login credentials by email
   - Government agencies do not demand payment via email or gift cards
4. If the email contains a threat or deadline, it is highly likely to be a phishing attempt

**What to tell the user:** "Scammers want you to act fast without thinking. They create fake emergencies — your account will be closed, you'll lose money, you'll miss a delivery. Real companies give you time to respond and never threaten you over email. If the email is pushing you to act immediately, that's a major red flag."

### Step 4: Examine Attachments Carefully
1. Do not open any attachment from an unexpected or suspicious email
2. Check the file extension (the part after the dot):
   - Dangerous extensions: .exe, .bat, .cmd, .scr, .vbs, .js, .ps1, .msi, .jar
   - High-risk document extensions: .docm, .xlsm, .pptm (these contain macros that can run malicious code)
   - Suspicious compressed files: .zip, .rar, .7z (especially if password-protected — this bypasses antivirus scanning)
   - Double extensions: invoice.pdf.exe (the real extension is .exe, but it appears as .pdf)
3. Safe extensions: .pdf (without additional extensions), .docx, .xlsx, .pptx (without macros), .txt, .jpg, .png
4. If you must open an attachment:
   - Save it to your computer without opening
   - Right-click the file > Scan with your antivirus software
   - Wait for the scan result before proceeding
5. When in doubt, contact the sender through a verified channel to confirm they sent the attachment

**What to tell the user:** "Attachments are a common way scammers deliver malware. Even a PDF or Word document can be dangerous if it contains hidden code. Never open an attachment you weren't expecting, even if it looks like it's from someone you know — their account could have been compromised."

### Step 5: Check Email Headers (Advanced)
1. Email headers contain technical details about where the email actually came from
2. In Outlook (Desktop): Double-click the email to open it in a new window > File > Properties > look at "Internet headers"
3. In Gmail: Open the email > three dots (...) > "Show original"
4. In Yahoo Mail: Open the email > three dots (...) > "View raw message"
5. Look for these key fields in the headers:
   - Return-Path: Should match the sender's domain — if different, the email is spoofed
   - Received: Trace the path — the earliest "Received" entry shows the actual origin server
   - Authentication-Results: Look for "spf=pass" or "spf=fail" — a fail indicates spoofing
   - DKIM-Signature: Missing or invalid DKIM suggests the email is not from the claimed domain
6. If the headers show the email originated from an unexpected server or country, it is likely phishing

**What to tell the user:** "Every email carries hidden technical information in its headers — like a passport stamp showing where it really came from. Even if the email looks legitimate on the surface, the headers can reveal that it actually originated from a server in another country. This is the definitive way to spot spoofed emails."

### Step 6: Report the Phishing Email
1. If your organization has a reporting tool (Phish Alert Button, Report Message button):
   - Select the suspicious email
   - Click the reporting button in the email toolbar
   - The email is automatically sent to the security team and removed from your inbox
2. Using Outlook (Microsoft 365): Select the email > "Report Message" in the ribbon > "Phishing"
3. Using Gmail: Open the email > three dots (...) > "Report phishing"
4. Using Yahoo Mail: Open the email > three dots (...) > "Report a Phishing Scam"
5. If no reporting tool is available:
   - Forward the email as an attachment to your IT security team or helpdesk
   - In Outlook: Double-click email > three dots (...) > "Forward as Attachment"
   - Subject line: "SUSPECTED PHISHING: [original subject]"
6. After reporting, delete the email from your inbox and deleted items folder

**What to tell the user:** "Reporting phishing emails is one of the most helpful things you can do for your organization's security. When you report a phishing email, the security team can block that sender across the entire company, protecting everyone else from the same scam. Please always report — never just delete."

### Step 7: What to Do If You Already Clicked or Entered Credentials
1. If you clicked a link but did not enter any information:
   - Close the browser tab immediately
   - Run a full antivirus scan on your computer
   - Report the email as phishing (Step 6)
   - Monitor your accounts for unusual activity for the next 48 hours
2. If you entered your password on a phishing site:
   - Change your password immediately from a different, known-safe device
   - Go to the legitimate website by typing the URL yourself (not using the email link)
   - Change your password to a new, unique password never used before
   - If you reused that password on other accounts, change those as well
   - Report the incident to your IT security team immediately — do not delay
   - Enable Multi-Factor Authentication (MFA) on your account if not already enabled
3. If you entered financial information (credit card, banking details):
   - Contact your bank immediately using the official phone number on the back of your card
   - Report the fraud and request a card freeze or replacement
   - Monitor your bank statements for unauthorized transactions

**What to tell the user:** "Don't panic — but act quickly. The faster you change your password and report the incident, the less damage an attacker can do. We'll walk through the steps together. And remember, this happens to thousands of people every day — the important thing is that you caught it and reported it."

---

## Alternative Solutions

If the above steps do not resolve the issue, also try:

- Contacting your organization's security team directly by phone if you are unsure about an email
- Using a free online service like VirusTotal to scan suspicious links or attachments before opening
- Checking the company's official website or social media for any announcements about ongoing phishing campaigns
- Forwarding the suspicious email to the Anti-Phishing Working Group at reportphishing@apwg.org

---

## Prevention Tips

- Think before you click — always hover over links and verify sender addresses before acting
- Enable Multi-Factor Authentication (MFA) on all accounts that support it
- Never reuse passwords across different accounts — use a password manager to generate unique passwords
- Keep your operating system, browser, and antivirus software updated
- If an email seems too good to be true or creates extreme urgency, trust your instincts and verify through another channel

---

## Root Cause

Common reasons phishing emails succeed, in order of likelihood:

- Urgency and fear override the recipient's caution (most common — attackers exploit human psychology)
- Sender email address not carefully verified before acting on the email
- Link destinations not previewed before clicking
- Attachments opened without verifying the sender's identity through a separate channel
- Lack of phishing awareness training and familiarity with common phishing tactics
- Email filtering at the organizational level not catching the phishing attempt
- User fatigue or distraction leading to inattentive email handling

---

## Escalation Decision Matrix

| Condition | Action |
|-----------|--------|
| All 7 steps completed, issue persists | Escalate to Tier 2 Security |
| You clicked a link or opened an attachment from a suspected phishing email | Escalate — requires security investigation |
| You entered your credentials on a suspicious website | Escalate immediately — account compromise likely |
| The phishing email appears to come from a legitimate internal email address | Escalate — possible account compromise of that sender |
| Multiple users in your department report receiving the same phishing email | Escalate — targeted campaign, security team must block |
| The email contains threats, blackmail, or references to sensitive company information | Escalate — potential legal and security issue |
| Email was reported and deleted successfully | Do not escalate — document in ticket |

---

## Related Articles

- [Account Compromised — Immediate Response Checklist](./account-compromised-checklist.md) — If you believe your account was compromised
- [Spot Phishing Emails — Quick Guide](../Tier-0-Self-Service/spot-phishing-quick-guide.md) — Tier 0: Self-service phishing identification
- [Email Header Forensics & Spoofing Investigation](../Tier-2-Technical-Support/email-header-forensics.md) — Tier 2: Advanced email analysis
- [Incident Response — Containment & Forensic Acquisition](../Tier-3-Expert-Engineering/incident-response-containment.md) — Tier 3: Expert security response

> **Note:** If you are looking for the Tier 0 self-service version of this article, see: [Spot Phishing Emails — Quick Guide](../Tier-0-Self-Service/spot-phishing-quick-guide.md) (to be created if not yet present).

---

## FAQ

**Q: What is the difference between spam and phishing?**
**A:** Spam is unwanted advertising — annoying but usually harmless. Phishing is a targeted attempt to steal your credentials, personal information, or money by pretending to be someone you trust. Phishing is malicious; spam is mostly just junk mail.

**Q: Can phishing emails come from people I know?**
**A:** Yes. This is called spear phishing. If a colleague's or friend's email account gets compromised, the attacker can send phishing emails from their real address. These are especially dangerous because they bypass the sender verification check. If the message seems unusual for that person, verify through another channel.

**Q: Is it safe to unsubscribe from phishing emails?**
**A:** No. Clicking "unsubscribe" on a phishing email confirms to the attacker that your email address is active and monitored. This can lead to more phishing attempts. Instead, report the email as phishing and delete it.

---

## Phishing Red Flags Quick Reference

| Red Flag | What to Look For |
|----------|------------------|
| Urgency | "Act now," "24 hours," "Immediate action required" |
| Generic greeting | "Dear Customer," "Dear User" instead of your name |
| Mismatched URL | Hover text shows different destination than displayed |
| Spelling errors | Poor grammar, misspellings, inconsistent formatting |
| Suspicious attachment | .exe, .zip, .docm from unknown sender |
| Request for credentials | No legitimate company asks for your password via email |
| Threat of negative action | "Account will be suspended," "Legal action will be taken" |
| Too good to be true | "You won a prize," "Free money," "Inheritance" |

---

## Was this article helpful?

If this article helped resolve your issue, great. If something was unclear, missing, or did not work, please open a GitHub Issue describing the problem so we can improve it.

Suggest improvements at: https://github.com/EzioLockhart/Tier-1-Support-Knowledge-Base/issues

---

## References

- CompTIA A+ Troubleshooting Methodology: Identify the problem, Establish a theory, Test the theory, Establish a plan of action, Verify functionality, Document findings
- ITIL Incident Management best practices: Prioritize based on impact and urgency; security incidents require immediate escalation
- Microsoft official documentation: Phishing and suspicious behavior in Outlook

---

*Tier: Tier 1 (Help Desk) | Difficulty: L1 (Basic) | Estimated Resolution Time: 5-10 minutes | Required Access Level: User | Severity: P2 (Single User Degraded)*

---

For internal use. Report all suspected phishing to your organization's security team immediately.
