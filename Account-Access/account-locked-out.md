# Account Locked After Multiple Attempts

**Category:** Account & Access
**Last Updated:** April 27, 2026
**Applies To:** Windows Active Directory Domain Accounts, Windows 10/11, Hybrid Azure AD Environments

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

## Quick Checks (30 seconds)

1. Ask the user: "Did you recently change your password?" If yes, the lockout is likely caused by another device or service using the old saved password
2. Ask the user: "Did you log into any new device, application, or service recently?" New devices may have saved the wrong password
3. Ask: "Are you receiving email on your phone?" Mobile devices with saved old passwords are one of the most common lockout sources
4. Check with the user: "Did you update your password in the Wi-Fi settings if your organization uses WPA2-Enterprise?" Corporate Wi-Fi frequently locks accounts
5. Verify the user is connected to the corporate network (VPN or on-site) — domain authentication requires connectivity to a domain controller

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
   - Understanding the lockout policy prevents unnecessary escalation and repeat lockouts.

### Step 2: Unlock the Account in Active Directory Users and Computers (ADUC)

1. Open **Active Directory Users and Computers** (ADUC) on a domain controller or management workstation with RSAT installed
2. Search for the user's account by username or full name
3. Right-click the user account > **"Properties"**
4. Go to the **"Account"** tab
5. Under **"Account options"**, look for the checkbox: **"Unlock the user's account. This account is currently locked out on this Active Directory Domain Controller."**
   - This checkbox only appears when the account is currently locked; if it is grayed out or not visible, the account is not locked
6. Check the box and click **"Apply"** then **"OK"**
7. Inform the user the account is now unlocked
8. If using PowerShell instead of ADUC:

Unlock-ADAccount -Identity "username"

9. Verify unlock succeeded:

Get-ADUser -Identity "username" -Properties LockedOut | Select-Object Name, LockedOut

   - LockedOut should now show "False"

### Step 3: Identify the Source of the Lockout (Event ID 4740)

1. The account will lock again if the root cause (old password stored somewhere) is not identified and fixed
2. On a domain controller, open **Event Viewer** (Win + R > eventvwr.msc)
3. Navigate to: **Windows Logs** > **Security**
4. Click **"Filter Current Log"** on the right pane
5. In the Event ID field, type **4740** and click **OK**
   - Event ID 4740 is generated every time a user account is locked out
6. Find the most recent event for the locked user and open it
7. Key information in the event:
   - **Account Name:** Confirms which account was locked
   - **Caller Computer Name:** The name of the computer or device that triggered the lockout — this is the most important field
   - **Time:** When the lockout occurred
8. If "Caller Computer Name" shows:
   - A workstation name (e.g., DESKTOP-ABC123): The lockout source is that specific computer — check Step 4
   - A server name (e.g., EXCHANGE-SRV01): A service on that server is causing the lockout (e.g., Exchange, SQL, IIS)
   - Blank or "-": The lockout came from a non-Windows device (mobile phone, Mac, Linux, or a web-based service)
   - Multiple different computer names: The user has old passwords saved on several devices
9. Share the Caller Computer Name with the user to help them identify which device has the old password
   - Finding the lockout source prevents the frustrating cycle of unlock-relock calls; without this step, the account will lock again.

### Step 4: Clear Saved Windows Credentials on the User's Computer

1. On the user's primary computer (or the computer identified in Event 4740), open **Credential Manager**:
   - Type "Credential Manager" in the Start menu search
   - Or Control Panel > User Accounts > Credential Manager
2. Click **"Windows Credentials"**
3. Look for any saved credentials related to the user's account or corporate resources:
   - Domain credentials
   - Outlook or Exchange credentials
   - VPN credentials
   - Network share credentials
   - Remote Desktop credentials
4. Click the arrow next to each credential to expand details
5. Click **"Remove"** for all credentials that use the old password
6. Also check **"Generic Credentials"** for any application-specific saved passwords
7. Restart the computer after clearing credentials
8. After restart, the user should log in with their current password
9. When prompted to save credentials again while working (Outlook, VPN, Wi-Fi), the user can save them with the correct password
   - Windows Credential Manager silently stores old passwords and keeps authenticating with them, causing repeated lockouts long after a password change.

### Step 5: Check Mobile Devices and Email Clients

1. Mobile devices are one of the most common causes of repeated account lockouts
2. Ask the user to check all devices that access corporate email:
   - Smartphone (iPhone or Android) — native mail app, Outlook mobile, or other email apps
   - Tablet (iPad, Android tablet)
   - Personal laptop or home desktop that may have Outlook configured
3. On each device, update the password:
   - **iPhone/iPad Mail app:** Settings > Mail > Accounts > Select account > Account > re-enter password
   - **Outlook mobile:** App will typically prompt for new password automatically when it fails to sync
   - **Android:** Settings > Accounts > select corporate account > re-enter password
4. If the user recently changed their password, the old one is still stored on these devices
5. After updating the password on all devices, monitor for at least 1 hour to ensure no further lockouts occur
   - A single mobile device with an old saved password can lock an account every few minutes as it repeatedly attempts to sync.

### Step 6: Check Mapped Network Drives and Persistent Connections

1. Mapped network drives configured with stored credentials use the old password
2. On the user's computer:
   - Open File Explorer and look at "This PC" for mapped drives
   - Disconnect all mapped drives: right-click each > **"Disconnect"**
3. After the account is unlocked and the user logs in with the correct password:
   - Remap the network drives
   - When entering credentials, ensure the user enters their new password
   - Check "Remember my credentials" only if desired
4. Also check for any persistent network connections that may use the old password:
   - Open Command Prompt and type: net use
   - This lists all active network connections
   - Delete old connections: net use * /delete
5. Remap drives and connections after login
   - Mapped drives with saved old passwords repeatedly authenticate in the background, triggering lockouts that the user does not see or initiate.

### Step 7: Check Scheduled Tasks and Services Running Under User Account

1. Some users configure scheduled tasks or services to run under their domain account
2. If the password was changed, these tasks continue using the old password and cause lockouts
3. Check for scheduled tasks:
   - Open **Task Scheduler** (Win + R > taskschd.msc)
   - Browse through the Task Scheduler Library
   - Look for any tasks configured to run under the user's domain account
   - Check the "Last Run Result" — errors like 0x8007052E (logon failure) indicate old password
4. Update the password for each task:
   - Right-click the task > **Properties**
   - Under "Security options", click **"Change User or Group"**
   - Re-enter the user account and password
5. Check Services running under the user account:
   - Open Services (Win + R > services.msc)
   - Look at the "Log On As" column
   - If any service uses the user's domain account, update the password in the service properties
6. Restart the computer after making changes
   - Automated tasks and services running old credentials trigger lockouts on a schedule, often at specific times of day, which can confuse the user who was not actively logging in at that time.

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
- Another user or automated system attempting to access the user's account with incorrect credentials (less common but possible with shared or service accounts)

---

## Escalation Criteria

Escalate to Tier 2 / Identity and Access Management Team if:

- Account lockout source cannot be identified after checking all common sources on the user's devices
- Account locks immediately after unlock even with all known sources cleared (possible account compromise or attack)
- Event ID 4740 does not appear on the domain controller (possible replication delay or logging not enabled)
- The account is a privileged account (Domain Admin, Enterprise Admin) requiring additional investigation per security policy
- Multiple user accounts are locking simultaneously (possible brute force attack or domain-wide issue)
- Lockout policy settings need to be reviewed or adjusted for the organization
- User suspects their account has been compromised — follow security incident response procedures immediately

---

## PowerShell Commands Quick Reference

| Command | Description |
|---------|-------------|
| `Unlock-ADAccount -Identity "username"` | Unlock a specific user account |
| `Get-ADUser -Identity "username" -Properties LockedOut` | Check if account is locked |
| `Search-ADAccount -LockedOut` | List all currently locked accounts in the domain |
| `Get-ADUser -Identity "username" -Properties PasswordLastSet, PasswordExpired, LockedOut` | View password age and lockout status |
| `Get-EventLog -LogName Security -InstanceId 4740 -Newest 10` | View last 10 account lockout events (requires domain controller) |
| `Get-ADUser -Identity "username" -Properties *` | View all user properties |

---

## Event ID 4740 Key Fields

| Field | What It Tells You |
|-------|-------------------|
| Account Name | Which user account was locked |
| Caller Computer Name | Which computer or device triggered the lockout |
| Time Created | When the lockout occurred |
| Subject: Security ID | Who or what process triggered the lockout |

---

For internal use. Follow your organization's identity verification, account unlock, and security policies.
