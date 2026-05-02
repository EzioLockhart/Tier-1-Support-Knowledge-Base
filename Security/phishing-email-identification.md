# How to Identify and Report a Phishing Email

**Category:** Security
**Last Updated:** May 2, 2026
**Applies To:** All Email Platforms (Outlook, Gmail, Yahoo, Webmail), All Users

---

## Symptoms

- Email appears to be from a legitimate company (bank, IT department, shipping company, government agency) but feels unusual
- Email creates a sense of urgency: "Your account will be suspended," "Payment required," "Immediate action needed"
- Sender email address looks slightly wrong (e.g., @microsft.com instead of @microsoft.com, @amaz0n.com instead of @amazon.com)
- Email contains links that do not match the displayed text when hovered over
- Unexpected attachment from an unknown or suspicious sender (especially .exe, .zip, .docm, .pdf with unusual name)
- Email requests personal information, login credentials, or payment details
- Email body contains poor grammar, spelling errors, or inconsistent formatting
- You were not expecting this email and it seems out of context

---

## Quick Checks (30 seconds)

1. Check the sender's actual email address (not just the display name) — does the domain match the company exactly?
2. Hover over any links in the email (do not click) — does the preview URL match where you expect to go?
3. Does the email address you by name, or use generic greetings like "Dear Customer" or "Dear User"?
4. Is there an unexpected attachment? Do not open it — verify with the supposed sender through a different channel
5. Were you expecting this email? If not, treat it as suspicious by default

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
   - Legitimate companies will never use a free email domain (@gmail.com, @yahoo.com, @outlook.com) for official communications.

### Step 2: Inspect Links Without Clicking

1. Hover your mouse cursor over any link or button in the email (do not click)
2. Look at the bottom-left corner of your browser or email client — the actual URL destination will appear
3. Check if the URL matches where you expect to go:
   - A legitimate company link should go to that company's official domain
   - A bank link should go to the official bank website
4. Look for these common phishing URL tricks:
   - Mismatched text and destination: Text says "Login to your account" but URL points to an unrelated site
   - Lookalike domains: secure-microsoft.com (real is microsoft.com), login-hsbc.com (real is hsbc.com)
   - URL shorteners: bit.ly, tinyurl.com, ow.ly — these hide the true destination
   - Subdomain tricks: microsoft.com.fake-site.com (the real domain is fake-site.com, not microsoft.com)
5. If unsure about a link, do not click it — instead, manually type the company's known website address into your browser
   - Never click a link in a suspicious email; go directly to the official website by typing the URL yourself.

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
   - Legitimate organizations use official channels and multiple contact attempts before taking negative action; they do not send single emails with immediate deadlines.

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
   - Even legitimate-looking attachments from known contacts can be malicious if the sender's account was compromised.

### Step 5: Check Email Headers (Advanced)

1. Email headers contain technical details about where the email actually came from
2. In Outlook (Desktop):
   - Double-click the email to open it in a new window
   - Go to **File** > **Properties**
   - Look at the "Internet headers" section at the bottom
3. In Gmail:
   - Open the email
   - Click the three dots (...) > **"Show original"**
4. In Yahoo Mail:
   - Open the email
   - Click the three dots (...) > **"View raw message"**
5. Look for these key fields in the headers:
   - **Return-Path:** Should match the sender's domain — if different, the email is spoofed
   - **Received:** Trace the path — the earliest "Received" entry shows the actual origin server
   - **Authentication-Results:** Look for "spf=pass" or "spf=fail" — a fail indicates spoofing
   - **DKIM-Signature:** Missing or invalid DKIM suggests the email is not from the claimed domain
6. If the headers show the email originated from an unexpected server or country, it is likely phishing
   - Header analysis is technical but provides definitive evidence of email spoofing.

### Step 6: Report the Phishing Email

1. If your organization has a reporting tool (Phish Alert Button, Report Message button):
   - Select the suspicious email
   - Click the reporting button in the email toolbar
   - The email is automatically sent to the security team and removed from your inbox
2. Using Outlook (Microsoft 365):
   - Select the email
   - Click **"Report Message"** in the ribbon > **"Phishing"**
3. Using Gmail:
   - Open the email
   - Click the three dots (...) > **"Report phishing"**
4. Using Yahoo Mail:
   - Open the email
   - Click the three dots (...) > **"Report a Phishing Scam"**
5. If no reporting tool is available:
   - Forward the email as an attachment to your IT security team or helpdesk
   - In Outlook: Double-click email > three dots (...) > **"Forward as Attachment"**
   - Subject line: "SUSPECTED PHISHING: [original subject]"
6. After reporting, delete the email from your inbox and deleted items folder
   - Reporting helps security teams block similar phishing attempts across the entire organization.

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
   - File a report with the relevant authorities if funds were lost
   - Quick reporting significantly reduces potential damage from credential compromise.
   - If you believe your account has already been compromised, follow the full response checklist: [Account Compromised — Immediate Response Checklist](./account-compromised-checklist.md)

---

## Root Cause

Common reasons phishing emails succeed, in order of likelihood:

- Urgency and fear override the recipient's caution (most common — attackers exploit human psychology)
- Sender email address not carefully verified before acting on the email
- Link destinations not previewed before clicking
- Attachments opened without verifying the sender's identity through a separate channel
- Lack of phishing awareness and familiarity with common phishing tactics
- Email filtering at the organizational level not catching the phishing attempt
- User fatigue or distraction leading to inattentive email handling

---

## Escalation Criteria

Report to IT Security Team immediately if:

- You clicked a link or opened an attachment from a suspected phishing email
- You entered your credentials on a suspicious website
- The phishing email appears to come from a legitimate internal email address (possible account compromise)
- Multiple users in your department report receiving the same phishing email (targeted campaign)
- The email contains threats, blackmail, or references to sensitive company information
- You are unsure whether an email is legitimate after completing the checks above — always verify with the security team

---

## Quick Reference: Phishing Red Flags

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

For internal use. Report all suspected phishing to your organization's security team immediately.
