# Password Reset — Active Directory

**Category:** Account & Access
**Last Updated:** April 27, 2026
**Applies To:** Windows Server Active Directory, Windows 10/11 Domain-Joined Workstations, Hybrid Azure AD Environments

---

## Symptoms

- User cannot log into their domain-joined computer
- Error message: "The password is incorrect" or "The user name or password is incorrect"
- User has forgotten their password or suspects account has been compromised
- Account is locked due to too many failed login attempts
- User is prompted to change password but cannot remember current password
- Helpdesk receives call or ticket requesting a password reset
- User cannot access network resources, shared drives, or email due to authentication failure

---

## Quick Checks (30 seconds)

1. Verify the caller's identity before proceeding — this is critical for security. Ask for employee ID, full name, department, and manager name
2. Confirm the username is correct — ask the user to verify the exact username they are using (e.g., DOMAIN\username or username@domain.com)
3. Check if Caps Lock is on — this is a common cause of "incorrect password" errors
4. Ask if the user recently changed their password on another device — the old device may still have the old password cached
5. Check if the user is connected to the corporate network (VPN or on-site) — domain password changes require connection to the domain controller

---

## Step-by-Step Resolution

### Step 1: Verify User Identity (Mandatory Security Step)

1. Ask the user to provide identifying information:
   - Full legal name as it appears in the system
   - Employee ID or badge number
   - Department and manager name
   - Office location or contact number on file
2. Compare the information provided against the user's record in Active Directory:
   - Open **Active Directory Users and Computers** (ADUC)
   - Search for the user by name or username
   - Open the user's properties and verify the details match
3. If the user cannot provide matching information, do not proceed — escalate to your supervisor or follow your organization's identity verification policy
4. If this is a remote user calling in, follow your organization's verification process (e.g., callback to registered phone number, manager confirmation, security questions)
5. Document the verification in the ticket before proceeding
   - Identity verification is the most critical step; resetting a password without proper verification is a major security risk that can lead to unauthorized access.

### Step 2: Reset Password in Active Directory Users and Computers

1. On a domain controller or a management workstation with RSAT (Remote Server Administration Tools) installed, open **Active Directory Users and Computers**
   - If you do not have ADUC installed: Open Server Manager > Add roles and features > Features > Remote Server Administration Tools > Role Administration Tools > AD DS and AD LDS Tools > Active Directory module for Windows PowerShell
2. In the ADUC console, navigate to the user's Organizational Unit (OU)
   - Common locations: "Users" container, or department-specific OUs like "Sales", "Marketing", "IT"
3. Find and right-click the user account
4. Select **"Reset Password"**
5. In the Reset Password dialog:
   - Enter a **new temporary password** that meets the organization's password policy requirements:
     - Minimum length (typically 8-12 characters)
     - Complexity (uppercase, lowercase, number, and special character — e.g., Welcome123!)
     - Must not be one of the user's previous passwords (AD tracks password history)
     - Avoid common words, the company name, or the user's name
   - Confirm the password by entering it again
   - Check the box: **"User must change password at next logon"** — this forces the user to create their own password
   - Do NOT uncheck this box unless specifically instructed by policy
6. Click **"OK"** to apply the password reset
7. If the account is also locked, check the box **"Unlock the user's account"** — the account lockout checkbox appears on the same dialog
   - If you use PowerShell instead, the equivalent command is:
   - Set-ADAccountPassword -Identity "username" -Reset -NewPassword (ConvertTo-SecureString -AsPlainText "TempPass123!" -Force)
   - Unlock-ADAccount -Identity "username"
   - Set-ADUser -Identity "username" -ChangePasswordAtLogon $true

### Step 3: Verify Password Policy Compliance

1. The temporary password MUST comply with the domain password policy. To check the policy:
   - Open **Group Policy Management Console** (GPMC)
   - Or in PowerShell: Get-ADDefaultDomainPasswordPolicy
2. Standard password policy requirements typically include:
   - Minimum password length (usually 8-14 characters)
   - Password must meet complexity requirements (three of four: uppercase, lowercase, number, symbol)
   - Password history enforced (cannot reuse last 5-24 passwords)
   - Minimum password age (usually 1 day — prevents users from cycling through passwords to reuse a favorite)
3. If the temporary password you set does not meet the policy, the reset will fail with an error
4. Note: Do not set a password that expires immediately (some configurations check minimum password age on reset)
   - Understanding password policy prevents "reset failed" errors and callback complaints.

### Step 4: Communicate the Temporary Password Securely to the User

1. Provide the temporary password to the user through a secure method:
   - In person: Have the user type it themselves on their device while you watch
   - Over the phone: Read the password clearly, using phonetic alphabet for ambiguous characters (e.g., "A as in Alpha, 0 as in Zero, l as in Lima, I as in India")
   - Via SMS or secure messaging app if your organization has one
   - Never send passwords via email unless encrypted and permitted by policy
2. Instruct the user clearly:
   - "Your temporary password is: [password]. It is case-sensitive."
   - "When you log in, you will be prompted to change it immediately."
   - "Choose a new password that you have never used before with this account."
   - "Your new password must be at least X characters long and include uppercase, lowercase, a number, and a symbol."
3. Remind the user to update the password on all devices and applications:
   - Email on mobile phone (Outlook app or native mail app)
   - Wi-Fi network password if using WPA2-Enterprise with domain credentials
   - Any saved passwords in web browsers or password managers
   - Shared drives or mapped network drives that use domain authentication
   - VPN client if they connect remotely
   - Stored credentials will keep trying the old password and may lock the account again.

### Step 5: Unlock Account if Also Locked Out

1. Often a password reset request is accompanied by an account lockout. Check if the account is locked:
   - In ADUC, open the user's properties and look at the **"Account"** tab
   - Under "Account options", if "Unlock account" is available as a checkbox, the account is currently locked
2. To unlock:
   - Check the **"Unlock the user's account"** checkbox (appears grayed out if account is not locked)
   - Click **Apply** or **OK**
3. Alternatively, fully unlock from the reset dialog: when resetting the password, the "Unlock the user's account" option is available in the same dialog
4. Inform the user that their account is now unlocked and they should wait 1-2 minutes before attempting to log in
5. If the account locks again immediately after unlock:
   - A device or service is using the old password and repeatedly trying to authenticate
   - The user has a saved credential, mapped drive, or mobile device with the old password
   - Check the security event log on the domain controller for the source of the failed logins:
     - Event ID 4740: Account Locked Out
     - Look at the "Caller Computer Name" field to identify which machine is causing the lockout
     - For detailed lockout source identification, see: [Account Locked After Multiple Attempts](./account-locked-out.md)

### Step 6: Verify Successful Login and Password Change

1. Ask the user to restart their computer before logging in (this clears cached credentials)
2. The user should log in with the temporary password at the Windows login screen
3. Windows will immediately display: "The user's password must be changed before signing in"
4. The user enters the temporary password again (current password field)
5. Then enters their new password twice (new password and confirm password)
6. After successful password change, the user should reach their desktop
7. Test access to key resources:
   - Can the user open Outlook and send/receive email?
   - Can the user access mapped network drives or SharePoint?
   - Can the user connect to VPN if remote?
8. If any resource prompts for password again, the user should enter their new password and check "Remember my credentials"
9. Document in the ticket that the reset was successful and what temporary password was provided (for audit trail if required by policy)
   - A verification step prevents a second callback when the user discovers they still cannot access email or VPN.

### Step 7: Educate User on Self-Service Password Reset (SSPR) for Future

1. Inform the user about self-service options to avoid future helpdesk calls:
   - **Microsoft 365 / Azure AD SSPR:** If your organization uses Microsoft 365, users can reset their own password at https://passwordreset.microsoftonline.com
   - **Self-Service Password Reset Portal:** Any internal portal your organization provides
   - **Security questions or alternate email/phone:** Encourage users to register these at https://aka.ms/ssprsetup
2. Walk the user through registering for SSPR if time permits:
   - Go to https://aka.ms/ssprsetup
   - Sign in with domain credentials
   - Register at least two authentication methods (mobile phone, alternate email, security questions)
3. Remind users:
   - Do not share passwords with anyone, including IT staff
   - Create unique passwords not used for personal accounts
   - Consider using a password manager approved by the organization
   - Report any suspicion of account compromise immediately, not just password reset
   - Password resets processed through helpdesk are tracked and audited
   - Self-service password reset reduces downtime, improves security, and empowers users.

---

## Root Cause

Common reasons users request a password reset, in order of frequency:

- User genuinely forgot their password (most common — human memory limitation with complex, frequently changed passwords)
- Password expired per domain policy without user noticing the expiration warning
- Account locked due to multiple failed login attempts (often from a mobile device or saved credential using old password)
- User recently changed password on one device but other devices still using the old cached password
- Caps Lock key unintentionally enabled during login
- Account compromised — user suspects unauthorized access and requests reset as a security measure
- New employee or contractor whose account was not properly communicated during onboarding

---

## Escalation Criteria

Escalate to Tier 2 / Identity and Access Management Team if:

- The password reset option is grayed out or returns an error (possible permission issue — you may not have rights to reset passwords for that OU)
- The account is a privileged account (Domain Admin, Enterprise Admin, Schema Admin, etc.) requiring additional authorization
- The user's account appears to be disabled, deleted, or missing entirely from Active Directory
- Password reset succeeds but the user still cannot authenticate (possible Kerberos or replication issue)
- The account keeps locking out repeatedly within minutes after unlocking and password reset
- The user reports suspicious activity indicating account compromise — follow security incident response procedures
- The domain controller is unreachable from your management workstation
- The user is a VIP or executive requiring expedited handling per organizational policy
- Password reset requires approval through a change management process due to compliance requirements

---

## PowerShell Commands Quick Reference

| Command | Description |
|---------|-------------|
| `Set-ADAccountPassword -Identity "username" -Reset -NewPassword (ConvertTo-SecureString -AsPlainText "TempPass123!" -Force)` | Reset user password |
| `Set-ADUser -Identity "username" -ChangePasswordAtLogon $true` | Force password change at next logon |
| `Unlock-ADAccount -Identity "username"` | Unlock a locked account |
| `Get-ADUser -Identity "username" -Properties LockedOut` | Check if account is locked |
| `Get-ADDefaultDomainPasswordPolicy` | View domain password policy |
| `Search-ADAccount -LockedOut` | List all currently locked accounts |
| `Get-ADUser -Identity "username" -Properties PasswordLastSet, PasswordExpired, PasswordNeverExpires` | Check password status |

---

For internal use. Follow your organization's identity verification and password reset policies.
