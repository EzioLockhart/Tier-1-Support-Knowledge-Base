# Account Compromised — Immediate Response Checklist

**Category:** Security
**Last Updated:** May 2, 2026
**Applies To:** All Account Types (Domain, Email, Cloud Services, VPN, Third-Party Applications)

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

## Quick Checks (30 seconds)

1. Can you still log into your account? If yes, proceed immediately to Step 1 — every minute counts
2. Check your account's recent login activity if accessible (look for unfamiliar locations or devices)
3. Look for any email rules or filters you did not create
4. Check if your email signature, auto-reply, or display name has been modified without your consent
5. Ask a colleague if they received any unusual emails or messages from you in the past 24 hours

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
6. The faster you change the password, the less time an attacker has to do damage.

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
   - MFA is the most effective protection against credential-based attacks; it stops attackers even if they have your password.

### Step 3: Force Sign-Out of All Active Sessions

1. Sign out the attacker from all active sessions immediately
2. Microsoft accounts:
   - Go to account.microsoft.com/security > "Sign out everywhere"
   - Check recent activity at mysignins.microsoft.com
3. Google accounts:
   - Go to myaccount.google.com/security > Your devices
   - Review all signed-in devices and sign out unfamiliar ones
   - Use "Sign out of all devices" option
4. Social media and other services:
   - Most platforms have a "Sign out of all sessions" or "Log out everywhere" option in security settings
   - Facebook: Settings > Security and Login > Where You're Logged In
   - Twitter/X: Settings > Security and Account Access > Apps and Sessions
   - LinkedIn: Settings > Sign in & Security > Where you're signed in
5. After signing out everywhere, log back in only on your trusted devices with the new password
   - Session tokens can remain valid after a password change; forcing sign-out everywhere ensures the attacker loses all access.

### Step 4: Check and Remove Malicious Rules, Filters, and Forwarding

1. Attackers commonly create hidden email rules to maintain access or hide their activity
2. Check your email settings for:
   - Auto-forwarding rules (emails forwarded to unknown addresses)
   - Inbox rules that move, delete, or hide specific emails
   - Filter rules that mark certain emails as read automatically
3. In Gmail:
   - Settings (gear icon) > See all settings > Forwarding and POP/IMAP
   - Check forwarding addresses — remove any you do not recognize
   - Settings > See all settings > Filters and Blocked Addresses — review all
4. In Outlook / Microsoft 365:
   - Settings (gear icon) > Mail > Rules
   - Review and remove any rules you did not create
   - Settings > Mail > Forwarding — disable forwarding unless you have a specific business need
5. In Yahoo Mail:
   - Settings > More Settings > Filters
   - Settings > More Settings > Mailboxes > Email forwarding
6. Also check for:
   - Hidden folders or labels the attacker may have created
   - Changes to your email signature or auto-reply (out-of-office) message
   - New connected applications or third-party integrations granted access to your account
   - Hidden rules and forwarding allow attackers to monitor your email even after a password change.

### Step 5: Run a Full Malware and Antivirus Scan

1. The attacker may have installed malware to capture your new password or maintain access
2. Run a full scan with your built-in antivirus software:
   - Windows: Settings > Privacy & Security > Windows Security > Virus & threat protection > Scan options > Full scan
   - Mac: Built-in XProtect runs automatically; additionally download Malwarebytes for Mac
3. Run an offline scan for deeper threats:
   - Windows: Same Scan options menu > Microsoft Defender Offline scan (restarts the computer)
4. Run a second-opinion scanner for additional confidence:
   - Malwarebytes Free: malwarebytes.com — download, install, and run a full scan
   - Emsisoft Emergency Kit: emsisoft.com — free portable scanner
5. If malware is detected:
   - Follow the removal prompts provided by the antivirus software
   - Restart the computer after removal
   - Run a second full scan to confirm the system is clean
6. If malware cannot be removed, the computer may need to be wiped and the operating system reinstalled
   - Escalate to your IT department if malware removal fails
   - A keystroke logger or remote access trojan can capture your new password immediately; malware must be removed before you proceed.

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
4. Cooperate fully with the investigation — the security team may need:
   - Access to your computer or device for forensic analysis
   - Information about your recent activities and communications
   - A detailed timeline of what happened and when
   - Prompt reporting protects not just your account but the entire organization.

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
5. Keep records:
   - Document the incident timeline for personal reference
   - Save all communications with IT or security teams
   - Note all steps you took and when you took them
   - Post-incident monitoring catches follow-up attacks, which often occur days or weeks after the initial compromise.

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
- For help identifying phishing emails before they compromise an account, see: [How to Identify and Report a Phishing Email](./phishing-email-identification.md)

---

## Escalation Criteria

Report to your security team or service provider immediately if:

- You cannot access your account to change the password (attacker has locked you out)
- Malware scan detects threats that cannot be removed by standard antivirus tools
- The compromised account has access to sensitive data, financial systems, or administrative functions
- Customer information, financial data, or other sensitive information may have been accessed
- The attacker sent messages to clients, partners, or the public from your account
- You suspect the compromise is part of a wider attack affecting multiple accounts or users
- Law enforcement or regulatory reporting may be required due to the nature of the data involved

---

## Quick Reference: Incident Response Timeline

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

For internal use. Report all security incidents to your organization's security team immediately.
