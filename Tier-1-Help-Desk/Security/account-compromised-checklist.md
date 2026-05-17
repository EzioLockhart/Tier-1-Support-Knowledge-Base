# Account Compromised — Immediate Response Checklist

- **Category:** Security
- **Tier:** Tier 1 (Help Desk)
- **Version:** 1.0
- **Last Updated:** May 2, 2026
- **Last Reviewed:** May 2, 2026
- **Applies To:** All Account Types (Domain, Email, Cloud Services, VPN, Third-Party Applications)
- **Difficulty:** L2 (Intermediate)
- **Estimated Resolution Time:** 30-60 minutes (immediate actions); ongoing monitoring for 30 days
- **Required Access Level:** User
- **Severity:** P1 (Single User, Critical — Account Security Compromised)
- **Keywords:** account compromised, hacked, unauthorized access, password change, MFA, malware scan, incident response, security
- **Prerequisite Knowledge:** Basic account management, ability to change passwords and run antivirus scans

---

## Symptoms

- You cannot log into your account despite entering what you believe is the correct password
- You receive unexpected Multi-Factor Authentication (MFA) prompts on your phone that you did not initiate
- Colleagues or contacts report receiving strange emails or messages from your account that you did not send
- Files in your cloud storage or shared drives have been modified, deleted, or encrypted without your knowledge
- Account recovery email or phone number has been changed without your knowledge
- Login activity shows locations, devices, or times you do not recognize
- New email rules have been created to forward, delete, or hide your incoming emails

---

## Common Error Codes

| Code | Meaning |
|------|---------|
| Event ID 4625 | Failed logon attempt — may indicate attacker trying passwords |
| Event ID 4672 | Special privileges assigned to new logon — possible privilege escalation |
| Event ID 4724 | Password reset attempt — check if this was authorized |
| 0x8007052E | Logon failure: unknown user name or bad password — repeated attempts indicate compromise |

---

## Symptom-to-Step Mapping

| If You See This | Skip To |
|-----------------|---------|
| You can still log into your account | Step 1 |
| MFA methods have been changed | Step 2 |
| Strange emails being sent from your account | Step 4 |
| Files modified or encrypted | Step 6 |
| You're completely locked out | Escalate immediately |

---

## Triage Questions

Before starting troubleshooting, ask the user:

1. "Can you still log into your account right now, or are you locked out?"
2. "What made you suspect your account has been compromised — strange emails, login alerts, or something else?"
3. "Have you clicked any suspicious links or entered your password on an unfamiliar website recently?"
4. "Do you have Multi-Factor Authentication enabled on this account?"

---

## Quick Checks (30 seconds)

1. Can you still log into your account? If yes, proceed immediately to Step 1 — every minute counts
2. Check your account's recent login activity if accessible (look for unfamiliar locations or devices)
3. Look for any email rules or filters you did not create
4. Check if your email signature, auto-reply, or display name has been modified without your consent
5. Ask a colleague if they received any unusual emails or messages from you in the past 24 hours
6. For help identifying phishing emails before they compromise an account, see: [How to Identify and Report a Phishing Email](./phishing-email-identification.md)

---

## Step-by-Step Resolution

### Step 1: Change Your Password Immediately
1. Change your password from a known-safe device (not the potentially compromised computer)
2. Use a strong, unique password:
   - At least 12 characters
   - Combination of uppercase, lowercase, numbers, and symbols
   - Not used on any other account
   - Not based on personal information (birthday, pet name, address, family names)
3. Do not use the compromised password ever again on any account
4. For work or organization accounts:
   - Contact your IT Service Desk to reset your password if you cannot do it yourself
   - Ensure "User must change password at next logon" is enabled if applicable
5. For personal email accounts (Gmail, Yahoo, Outlook.com):
   - Use the "Forgot password" recovery flow if locked out
   - Gmail: accounts.google.com/signin/recovery
   - Yahoo: login.yahoo.com/forgot
   - Outlook.com: account.live.com/password/reset

**What to tell the user:** "The first and most urgent step is to change your password. This is like changing the locks on your door — it stops the attacker from getting back in. Use a completely new password you've never used anywhere before. Every minute counts, so let's do this right now from a device you trust."

### Step 2: Verify and Update Multi-Factor Authentication (MFA) Settings
1. Check your MFA methods immediately after changing your password
2. For Microsoft accounts: mysignins.microsoft.com/security-info
3. For Google accounts: myaccount.google.com/security > 2-Step Verification
4. For other services: Look for "Security settings" or "Two-factor authentication" in account settings
5. Verify all registered MFA methods are devices you own and recognize
6. Remove any unfamiliar phone numbers, email addresses, or authenticator app entries
7. Re-register your MFA methods if any were removed by the attacker
8. If you use SMS-based MFA, consider switching to an authenticator app (Microsoft Authenticator, Google Authenticator, Authy) — SMS is more vulnerable to interception
9. Enable MFA on your account if it was not already enabled before the compromise

**What to tell the user:** "MFA is your strongest protection. Even if an attacker has your password, they can't get in without access to your phone. But we need to check that the attacker hasn't added their own phone number or authentication app to your account. Let's review every MFA method registered."

### Step 3: Force Sign-Out of All Active Sessions
1. Sign out the attacker from all active sessions immediately
2. Microsoft accounts: Go to account.microsoft.com/security > "Sign out everywhere"
3. Google accounts: Go to myaccount.google.com/security > Your devices > Review all signed-in devices > "Sign out of all devices"
4. Social media and other services:
   - Facebook: Settings > Security and Login > Where You're Logged In
   - Twitter/X: Settings > Security and Account Access > Apps and Sessions
   - LinkedIn: Settings > Sign in & Security > Where you're signed in
5. Most platforms have a "Sign out of all sessions" or "Log out everywhere" option in security settings
6. After signing out everywhere, log back in only on your trusted devices with the new password

**What to tell the user:** "Changing your password is great, but the attacker might already be logged in. Their active session could stay connected even after a password change. We need to force every device, everywhere, to sign out. The attacker will then need the new password — which only you have — to get back in."

### Step 4: Check and Remove Malicious Rules, Filters, and Forwarding
1. Attackers commonly create hidden email rules to maintain access or hide their activity
2. Check your email settings for:
   - Auto-forwarding rules (emails forwarded to unknown addresses)
   - Inbox rules that move, delete, or hide specific emails
   - Filter rules that mark certain emails as read automatically
3. In Gmail:
   - Settings (gear icon) > See all settings > Forwarding and POP/IMAP > check forwarding addresses
   - Settings > See all settings > Filters and Blocked Addresses > review all
4. In Outlook / Microsoft 365:
   - Settings (gear icon) > Mail > Rules > review and remove any rules you did not create
   - Settings > Mail > Forwarding > disable forwarding unless you have a specific need
5. In Yahoo Mail:
   - Settings > More Settings > Filters
   - Settings > More Settings > Mailboxes > Email forwarding
6. Also check for hidden folders or labels the attacker may have created

**What to tell the user:** "Attackers often create hidden rules that forward your emails to them or hide their activity. Even after changing your password, they could still be reading your incoming emails through forwarding. We need to check every rule and filter in your email settings."

### Step 5: Run a Full Malware and Antivirus Scan
1. The attacker may have installed malware to capture your new password or maintain access
2. Run a full scan with your built-in antivirus software:
   - Windows: Settings > Privacy & Security > Windows Security > Virus & threat protection > Scan options > Full scan
   - Mac: Built-in XProtect runs automatically; additionally download Malwarebytes for Mac
3. Run an offline scan for deeper threats:
   - Windows: Same Scan options menu > Microsoft Defender Offline scan (restarts the computer)
4. Run a second-opinion scanner:
   - Malwarebytes Free: malwarebytes.com — download, install, and run a full scan
   - Emsisoft Emergency Kit: emsisoft.com — free portable scanner
5. If malware is detected:
   - Follow the removal prompts provided by the antivirus software
   - Restart the computer after removal
   - Run a second full scan to confirm the system is clean
6. If malware cannot be removed, the computer may need to be wiped and the operating system reinstalled

**What to tell the user:** "If you clicked a link or opened an attachment from the attacker, your computer could be infected with malware that records everything you type — including your new password. We need to run a deep scan to make sure your computer is clean. This is critical because changing your password won't help if the attacker can see you type the new one."

### Step 6: Notify Your IT Security Team or Service Provider
1. Report the compromise to your organization's security team or the service provider immediately
2. Provide these details:
   - What symptoms you noticed and when they started
   - Whether you clicked any suspicious links or entered credentials somewhere
   - Whether you still have access to the account or are locked out
   - Any unusual files, emails, or activity you observed
   - All steps you have already taken (password change, MFA update, sign-out, scans)
3. The security team will:
   - Investigate the scope of the compromise
   - Check if the attacker accessed sensitive data or other connected systems
   - Block the attacker's access at the organizational level
   - Initiate formal incident response procedures if required
4. Cooperate fully with the investigation — the security team may need access to your computer or account

**What to tell the user:** "You've done everything right so far. Now we need to notify the security team so they can protect the rest of the organization. They'll check if the attacker tried to move beyond your account, access sensitive data, or target other people. Reporting quickly protects everyone, not just you."

### Step 7: Monitor and Recover Post-Incident
1. After the immediate response, continue monitoring for at least 30 days:
   - Check login activity daily for unfamiliar locations, devices, or times
   - Review sent items and deleted items for messages the attacker may have sent
   - Check all connected applications and third-party integrations
2. Review and update security on linked accounts:
   - If you used the compromised password on other services, change those passwords immediately
   - Each account should have a unique password
   - Enable MFA on all accounts that support it
3. Check for data exfiltration:
   - Review cloud storage, email, and shared drives for signs the attacker downloaded or accessed files
   - Report any suspected data loss to the security team immediately
4. Learn from the incident:
   - Identify how the compromise likely occurred (phishing, weak password, no MFA, reused password, malware)
   - Address the root cause to prevent recurrence
   - Consider using a password manager to generate and store strong, unique passwords
5. Keep records of the incident timeline and all communications with IT

**What to tell the user:** "The danger isn't over just because you've secured your account. Attackers sometimes wait weeks before using stolen information. We need to stay vigilant — check your login activity regularly, watch for unusual behavior, and make sure this doesn't happen again by fixing the root cause."

---

## Alternative Solutions

If the above steps do not resolve the issue, also try:

- Checking haveibeenpwned.com to see if your email address was part of a known data breach
- Reviewing connected apps and third-party integrations that have access to your account
- Placing a fraud alert on your credit report if financial information was exposed
- Contacting law enforcement if you experienced financial loss or identity theft

---

## Prevention Tips

- Enable Multi-Factor Authentication on every account that supports it
- Use a password manager to generate and store unique, strong passwords for each service
- Never reuse passwords across different accounts — one breach compromises all
- Be skeptical of unsolicited emails, especially those creating urgency or requesting credentials
- Regularly review your account's recent login activity and connected applications

---

## Root Cause

Common ways accounts become compromised, in order of likelihood:

- Phishing email successfully tricked user into entering credentials on a fake login page (most common)
- Password reused across multiple services and one of those services suffered a data breach
- Weak password easily guessed or cracked by automated brute force attacks
- Multi-Factor Authentication (MFA) not enabled, allowing access with just a password
- Malware or keylogger on the computer captured the password as it was typed
- Credentials exposed in a third-party data breach and sold or published online
- Social engineering attack where an attacker impersonated a trusted entity and obtained the password

---

## Escalation Decision Matrix

| Condition | Action |
|-----------|--------|
| All 7 steps completed, issue persists | Escalate to Tier 2 Security |
| You cannot access your account to change the password | Escalate immediately — attacker has locked you out |
| Malware scan detects threats that cannot be removed | Escalate — requires advanced cleaning or system wipe |
| The compromised account has access to sensitive data or administrative functions | Escalate urgently — potential data breach |
| Customer information, financial data, or other sensitive information may have been accessed | Escalate — regulatory reporting may be required |
| The attacker sent messages to clients, partners, or the public from your account | Escalate — reputational risk |
| Account secured and no further suspicious activity after 30 days | Do not escalate — document as resolved |

---

## Related Articles

- [How to Identify and Report a Phishing Email](./phishing-email-identification.md) — If the compromise started with a phishing email
- [Spot Phishing Emails — Quick Guide](../Tier-0-Self-Service/spot-phishing-quick-guide.md) — Tier 0: Self-service phishing identification
- [Security Event Log Analysis & SIEM Alert Investigation](../Tier-2-Technical-Support/security-event-log-analysis.md) — Tier 2: Advanced security diagnostics
- [Incident Response — Containment & Forensic Acquisition](../Tier-3-Expert-Engineering/incident-response-containment.md) — Tier 3: Expert incident response

> **Note:** If you are looking for the Tier 2 or Tier 3 versions of this article, see: [Security Event Log Analysis](../Tier-2-Technical-Support/security-event-log-analysis.md) and [Incident Response](../Tier-3-Expert-Engineering/incident-response-containment.md) (to be created if not yet present).

---

## FAQ

**Q: I changed my password, but I'm still seeing strange activity. What now?**
**A:** The attacker may have created forwarding rules, added backup email addresses, or installed malware on your device. Go through all the steps again, paying special attention to Step 3 (sign out everywhere) and Step 4 (check rules and forwarding). If activity continues, escalate to your security team immediately.

**Q: Should I pay a ransom if my files have been encrypted?**
**A:** No. Paying encourages further attacks and there is no guarantee your files will be restored. Report the ransomware to your security team and law enforcement. If you have backups, your files can be restored without paying.

**Q: How do I know if this was a targeted attack or a random compromise?**
**A:** If your account was compromised through a mass phishing campaign or a data breach at another service, it was likely opportunistic. If the attacker specifically researched you, used personal information, or targeted your organization, it may be a targeted attack. Your security team can help determine this.

---

## Incident Response Timeline Quick Reference

| Timeframe | Action |
|-----------|--------|
| Immediately (within 5 minutes) | Change password from a safe, trusted device |
| Within 15 minutes | Enable or verify MFA settings; sign out all active sessions |
| Within 30 minutes | Check and remove malicious email rules, filters, and forwarding |
| Within 2 hours | Run a full malware scan on all potentially affected devices |
| Within 4 hours | Notify your IT security team or service provider |
| Within 24 hours | Audit connected applications and linked accounts |
| Ongoing (30 days) | Monitor login activity and account behavior for unusual patterns |

---

## Was this article helpful?

If this article helped resolve your issue, great. If something was unclear, missing, or did not work, please open a GitHub Issue describing the problem so we can improve it.

Suggest improvements at: https://github.com/EzioLockhart/Tier-1-Support-Knowledge-Base/issues

---

## References

- CompTIA A+ Troubleshooting Methodology: Identify the problem, Establish a theory, Test the theory, Establish a plan of action, Verify functionality, Document findings
- ITIL Incident Management best practices: Security incidents require immediate escalation and formal incident response
- Microsoft official documentation: What to do if your account has been compromised

---

*Tier: Tier 1 (Help Desk) | Difficulty: L2 (Intermediate) | Estimated Resolution Time: 30-60 minutes | Required Access Level: User | Severity: P1 (Single User Critical)*

---

For internal use. Report all security incidents to your organization's security team immediately.
