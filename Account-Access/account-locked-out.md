# Account Locked After Multiple Attempts

- **Category:** Account & Access
- **Tier:** Tier 1 (Help Desk)
- **Version:** 1.0
- **Last Updated:** May 2, 2026
- **Last Reviewed:** May 2, 2026
- **Applies To:** Windows Active Directory Domain Accounts, Windows 10 (22H2), Windows 11 (23H2), Hybrid Azure AD Environments
- **Difficulty:** L2 (Intermediate)
- **Estimated Resolution Time:** 10-20 minutes
- **Required Access Level:** Administrator
- **Severity:** P1 (Single User, Critical — Cannot Log In)
- **Keywords:** account locked, lockout, Active Directory, Event ID 4740, Credential Manager, unlock, password, devices
- **Prerequisite Knowledge:** Active Directory Users and Computers (ADUC), Event Viewer navigation, basic PowerShell

---

## Symptoms

- User receives error: "The referenced account is currently locked out and may not be logged on to"
- Error message at Windows login screen: "Your account has been locked. Contact your support person to unlock it."
- User is unable to log in despite entering what they believe is the correct password
- Account was working fine earlier but suddenly locked without the user intentionally attempting multiple failed logins
- User receives email notification (if configured) that their account has been locked
- Account locks repeatedly within minutes or hours after being unlocked by IT support
- VPN, Wi-Fi (WPA2-Enterprise), or email on mobile device stops working due to account lockout

---

## Common Error Codes

| Code | Meaning |
|------|---------|
| Event ID 4740 | A user account was locked out — recorded on the domain controller |
| Event ID 4625 | An account failed to log on — check for multiple recent events |
| 0x8007052E | Logon failure: unknown user name or bad password |
| 0x8007052F | Account locked out due to too many invalid logon attempts |

---

## Symptom-to-Step Mapping

| If You See This | Skip To |
|-----------------|---------|
| Account locks every few minutes | Step 3 |
| Event ID 4740 shows Caller Computer Name | Step 4 |
| User recently changed their password | Step 5 |
| User has corporate email on phone | Step 5 |
| Account locks at specific times of day | Step 7 |

---

## Triage Questions

Before starting troubleshooting, ask the user:

1. "Did you recently change your password? If yes, that's likely the cause — other devices still have the old password."
2. "Do you have corporate email set up on your phone or tablet?"
3. "Are you logged into any other computers, or do you have mapped network drives?"
4. "Did you save your password in any applications, VPN clients, or Wi-Fi settings?"

---

## Quick Checks (30 seconds)

1. Check if the user recently changed their password — this is the most common cause of repeated lockouts
2. Ask if the user has corporate email on a mobile device (phone or tablet)
3. Check if the user is connected to corporate Wi-Fi using domain credentials (WPA2-Enterprise)
4. Verify the user is connected to the corporate network (VPN or on-site) — domain authentication requires connectivity to a domain controller
5. If the user also needs their password reset, see: [Password Reset — Active Directory](./password-reset-ad.md)

---

## Step-by-Step Resolution

### Step 1: Wait for the Account Lockout Duration (If Applicable)
1. Many organizations configure an account lockout policy with an automatic unlock duration
2. Common policy settings:
   - Account lockout threshold: 3-5 invalid attempts
   - Account lockout duration: 15-30 minutes (automatic unlock) or 0 (never auto-unlock, requires manual IT unlock)
3. Ask the user how long the account has been locked:
   - If less than the lockout duration, ask them to wait and the account will unlock automatically
   - If the lockout duration is set to 0 or the user cannot wait, proceed to manual unlock in Step 2
4. While waiting, advise the user:
   - Do not continue attempting to log in — each failed attempt resets the lockout timer
   - Close all applications that may be using the old password (Outlook, VPN, Wi-Fi, mapped drives)
   - Restart the computer before attempting login after the lockout period

**What to tell the user:** "Your account will unlock automatically if we wait. But if you keep trying to log in with the wrong password, it resets the timer. Let's stop all attempts, close anything that might be using your old password, and wait. If your organization doesn't have an automatic unlock, I'll unlock it manually now."

### Step 2: Unlock the Account in Active Directory
1. Open Active Directory Users and Computers (ADUC) on a domain controller or management workstation with RSAT installed
2. Search for the user's account by username or full name
3. Right-click the user account > "Properties"
4. Go to the "Account" tab
5. Under "Account options", look for the checkbox: "Unlock the user's account. This account is currently locked out on this Active Directory Domain Controller."
   - This checkbox only appears when the account is currently locked
6. Check the box and click "Apply" then "OK"
7. Inform the user the account is now unlocked
8. If using PowerShell:
   Unlock-ADAccount -Identity "username"
9. Verify unlock succeeded:
   Get-ADUser -Identity "username" -Properties LockedOut | Select-Object Name, LockedOut
   - LockedOut should now show "False"

**What to tell the user:** "Your account is now unlocked. But before you try to log in, we need to find what's causing the lockouts — otherwise it will just lock again in a few minutes."

### Step 3: Identify the Source of the Lockout (Event ID 4740)
1. The account will lock again if the root cause is not identified and fixed
2. On a domain controller, open Event Viewer: Win + R > eventvwr.msc
3. Navigate to: Windows Logs > Security
4. Click "Filter Current Log" on the right pane
5. In the Event ID field, type 4740 and click OK
   - Event ID 4740 is generated every time a user account is locked out
6. Find the most recent event for the locked user and open it
7. Key information in the event:
   - Account Name: Confirms which account was locked
   - Caller Computer Name: The name of the computer or device that triggered the lockout — this is the most important field
   - Time: When the lockout occurred
8. If "Caller Computer Name" shows:
   - A workstation name (e.g., DESKTOP-ABC123): The lockout source is that specific computer — check Step 4
   - A server name (e.g., EXCHANGE-SRV01): A service on that server is causing the lockout
   - Blank or "-": The lockout came from a non-Windows device (mobile phone, Mac, Linux, or web-based service)
   - Multiple different computer names: The user has old passwords saved on several devices
9. Share the Caller Computer Name with the user

**What to tell the user:** "I found the source of the lockout. Your account is being locked by [Caller Computer Name]. This is likely a device or application that's still using your old password. Let's track it down and fix it."

### Step 4: Clear Saved Windows Credentials on the User's Computer
1. On the user's primary computer (or the computer identified in Event 4740), open Credential Manager:
   - Type "Credential Manager" in the Start menu search
   - Or Control Panel > User Accounts > Credential Manager
2. Click "Windows Credentials"
3. Look for any saved credentials related to the user's account or corporate resources:
   - Domain credentials
   - Outlook or Exchange credentials
   - VPN credentials
   - Network share credentials
   - Remote Desktop credentials
4. Click the arrow next to each credential to expand details
5. Click "Remove" for all credentials that use the old password
6. Also check "Generic Credentials" for any application-specific saved passwords
7. Restart the computer after clearing credentials
8. After restart, the user should log in with their current password

**What to tell the user:** "Windows saves passwords in a hidden vault called Credential Manager. When you change your password, those saved copies don't update — they keep trying the old one. We're going to clear them all out so only your current password is used."

### Step 5: Check Mobile Devices and Email Clients
1. Mobile devices are one of the most common causes of repeated account lockouts
2. Ask the user to check all devices that access corporate email:
   - Smartphone (iPhone or Android) — native mail app, Outlook mobile, or other email apps
   - Tablet (iPad, Android tablet)
   - Personal laptop or home desktop that may have Outlook configured
3. On each device, update the password:
   - iPhone/iPad Mail app: Settings > Mail > Accounts > Select account > Account > re-enter password
   - Outlook mobile: App will typically prompt for new password automatically when it fails to sync
   - Android: Settings > Accounts > select corporate account > re-enter password
4. If the user recently changed their password, the old one is still stored on these devices
5. After updating the password on all devices, monitor for at least 1 hour

**What to tell the user:** "Your phone or tablet is likely the culprit. It keeps trying to sync email with your old password, and each attempt counts as a failed login. After enough tries, your account locks. Update the password on every device that has your work email."

### Step 6: Check Mapped Network Drives and Persistent Connections
1. Mapped network drives configured with stored credentials use the old password
2. On the user's computer:
   - Open File Explorer and look at "This PC" for mapped drives
   - Disconnect all mapped drives: right-click each > "Disconnect"
3. After the account is unlocked and the user logs in with the correct password:
   - Remap the network drives
   - When entering credentials, ensure the user enters their new password
   - Check "Remember my credentials" only if desired
4. Also check for any persistent network connections using old password:
   - Open Command Prompt and type: net use
   - This lists all active network connections
   - Delete old connections: net use * /delete
5. Remap drives and connections after login

**What to tell the user:** "Mapped network drives that remember your old password will keep trying to reconnect in the background. Each attempt is a failed login. We need to disconnect them and reconnect using your new password."

### Step 7: Check Scheduled Tasks and Services Running Under User Account
1. Some users configure scheduled tasks or services to run under their domain account
2. If the password was changed, these tasks continue using the old password and cause lockouts
3. Check for scheduled tasks:
   - Open Task Scheduler: Win + R > taskschd.msc
   - Browse through the Task Scheduler Library
   - Look for any tasks configured to run under the user's domain account
   - Check the "Last Run Result" — errors like 0x8007052E (logon failure) indicate old password
4. Update the password for each task:
   - Right-click the task > Properties
   - Under "Security options", click "Change User or Group"
   - Re-enter the user account and password
5. Check Services running under the user account:
   - Open Services: Win + R > services.msc
   - Look at the "Log On As" column
   - If any service uses the user's domain account, update the password
6. Restart the computer after making changes

**What to tell the user:** "Do you have any automated tasks that run under your account, like scheduled backups or scripts? These store your password separately and don't update when you change it. Let's check and update them."

---

## Alternative Solutions

If the above steps do not resolve the issue, also try:

- Using the Microsoft Account Lockout and Management Tools (LockoutStatus.exe, ALTools) for advanced lockout analysis
- Enabling Netlogon debug logging on the user's computer to trace authentication attempts
- Checking for stored passwords in web browsers (Chrome, Edge, Firefox saved passwords)
- Having the user sign out of all Microsoft 365 sessions and sign back in fresh

---

## Prevention Tips

- Update your password on all devices (phone, tablet, home computer) immediately after changing it
- Use a password manager to avoid saving passwords in browsers and Credential Manager manually
- Regularly review and clean out Windows Credential Manager
- Avoid configuring scheduled tasks or services to run under your personal domain account
- Register for Self-Service Password Reset (SSPR) so you can reset your own password without calling the helpdesk

---

## Root Cause

Common causes of account lockouts, in order of likelihood:

- Mobile device (phone or tablet) with old saved password attempting to sync email — most common
- Windows Credential Manager storing old domain or application passwords
- User changed domain password but did not update it on all devices and applications
- Mapped network drives using stored credentials with the old password
- VPN client with saved old password attempting to reconnect automatically
- Corporate Wi-Fi (WPA2-Enterprise) using old password to authenticate
- Scheduled tasks or Windows services configured to run under the user's domain account
- Another user or automated system attempting to access the user's account with incorrect credentials

---

## Escalation Decision Matrix

| Condition | Action |
|-----------|--------|
| Account lockout source cannot be identified after all checks | Escalate to Tier 2 |
| Account locks immediately after unlock with all known sources cleared | Escalate — possible account compromise |
| Event ID 4740 does not appear on the domain controller | Escalate — possible replication delay or logging issue |
| Account is a privileged account (Domain Admin, Enterprise Admin) | Escalate — requires additional security investigation |
| Multiple user accounts are locking simultaneously | Escalate — possible brute force attack or domain-wide issue |
| Lockout policy settings need to be reviewed or adjusted | Escalate — requires policy change |
| Source identified and fixed, no further lockouts | Do not escalate — document solution |

---

## Related Articles

- [Password Reset — Active Directory](./password-reset-ad.md) — If the user also needs their password reset
- [Self-Service Password Reset Guide (SSPR)](../Tier-0-Self-Service/sspr-guide.md) — For users who want to reset without calling the helpdesk
- [Kerberos Authentication Failures & Token Analysis](../Tier-2-Technical-Support/kerberos-auth-failures.md) — Tier 2: Advanced authentication diagnostics
- [Security Event Log Analysis & SIEM Alert Investigation](../Tier-2-Technical-Support/security-event-log-analysis.md) — Tier 2: Understanding Event ID 4740 in depth

> **Note:** If you are looking for the Account Compromised Immediate Response Checklist, see: [Account Compromised — Immediate Response Checklist](../Security/account-compromised-checklist.md) (to be created if not yet present). If you are looking for Conditional Access Policy Troubleshooting, see the Tier 2 MFA & Authentication category.

---

## FAQ

**Q: Why does my account keep locking even after I changed my password?**
**A:** Changing your password does not automatically update saved copies on other devices. Your phone, tablet, mapped drives, and VPN client all store the old password and keep trying it. You must update each one manually.

**Q: How can I find out which device is locking my account?**
**A:** The Event ID 4740 on the domain controller shows the "Caller Computer Name" — this is the device causing the lockout. If it's blank, the lockout is coming from a non-Windows device like a phone or tablet.

**Q: Will clearing Credential Manager delete my saved website passwords?**
**A:** No. Website passwords saved in your browser are separate from Windows Credential Manager. Clearing Windows Credentials only removes saved Windows and network passwords, not your browser's saved logins.

---

## PowerShell Commands Quick Reference

| Command | Description |
|---------|-------------|
| Unlock-ADAccount -Identity "username" | Unlock a specific user account |
| Get-ADUser -Identity "username" -Properties LockedOut | Check if account is locked |
| Search-ADAccount -LockedOut | List all currently locked accounts in the domain |
| Get-ADUser -Identity "username" -Properties PasswordLastSet, PasswordExpired, LockedOut | View password age and lockout status |
| Get-EventLog -LogName Security -InstanceId 4740 -Newest 10 | View last 10 account lockout events (requires domain controller) |
| Get-ADUser -Identity "username" -Properties * | View all user properties |

---

## Event ID 4740 Key Fields

| Field | What It Tells You |
|-------|-------------------|
| Account Name | Which user account was locked |
| Caller Computer Name | Which computer or device triggered the lockout |
| Time Created | When the lockout occurred |
| Subject: Security ID | Who or what process triggered the lockout |

---

## Was this article helpful?

If this article helped resolve your issue, great. If something was unclear, missing, or did not work, please open a GitHub Issue describing the problem so we can improve it.

Suggest improvements at: https://github.com/EzioLockhart/Tier-1-Support-Knowledge-Base/issues

---

## References

- CompTIA A+ Troubleshooting Methodology: Identify the problem, Establish a theory, Test the theory, Establish a plan of action, Verify functionality, Document findings
- ITIL Incident Management best practices: Prioritize based on impact and urgency; Account lockout affects multiple services
- Microsoft official documentation: Account lockout troubleshooting

---

*Tier: Tier 1 (Help Desk) | Difficulty: L2 (Intermediate) | Estimated Resolution Time: 10-20 minutes | Required Access Level: Administrator | Severity: P1 (Single User Critical)*

---

For internal use. Follow your organization's identity verification, account unlock, and security policies.
