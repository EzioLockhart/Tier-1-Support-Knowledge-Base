# Password Reset — Active Directory

- **Category:** Account & Access
- **Tier:** Tier 1 (Help Desk)
- **Version:** 1.0
- **Last Updated:** May 2, 2026
- **Last Reviewed:** May 2, 2026
- **Applies To:** Windows Server Active Directory, Windows 10 (22H2), Windows 11 (23H2) Domain-Joined Workstations, Hybrid Azure AD Environments
- **Difficulty:** L2 (Intermediate)
- **Estimated Resolution Time:** 5-10 minutes
- **Required Access Level:** Administrator
- **Severity:** P1 (Single User, Critical — Cannot Log In)
- **Keywords:** Active Directory, password reset, ADUC, unlock account, temporary password, identity verification, SSPR, domain
- **Prerequisite Knowledge:** Active Directory Users and Computers (ADUC), basic PowerShell knowledge, understanding of password policies

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

## Common Error Codes

| Code | Meaning |
|------|---------|
| 0x80070056 | Password policy violation — new password does not meet complexity requirements |
| 0x8007052D | Password history conflict — new password was used previously |
| 0x8007052F | Account restrictions preventing password change at this time |
| Event ID 4724 | Password reset attempt recorded in security log (success or failure) |

---

## Symptom-to-Step Mapping

| If You See This | Skip To |
|-----------------|---------|
| User cannot verify their identity | Step 1 |
| Password reset option is grayed out | Step 2 (PowerShell) or escalate |
| Account is also locked out | Step 5 |
| User changed password but still cannot log in | Step 6 |
| User wants to reset without calling helpdesk | Step 7 |

---

## Triage Questions

Before starting troubleshooting, ask the user:

1. "Can you tell me your full name, employee ID, department, and manager's name so I can verify your identity?"
2. "Are you getting a specific error message when you try to log in, like 'account locked' or just 'incorrect password'?"
3. "Did you recently change your password on any other device or application?"
4. "Are you connected to the corporate network, either in the office or through VPN?"

---

## Quick Checks (30 seconds)

1. Verify the caller's identity before proceeding — this is critical for security. Ask for employee ID, full name, department, and manager name
2. Confirm the username is correct — ask the user to verify the exact username they are using (e.g., DOMAIN\username or username@domain.com)
3. Check if Caps Lock is on — this is a common cause of "incorrect password" errors
4. Ask if the user recently changed their password on another device — the old device may still have the old password cached
5. Check if the user is connected to the corporate network (VPN or on-site) — domain password changes require connection to a domain controller
6. If the account is locked rather than just needing a password change, see: [Account Locked After Multiple Attempts](./account-locked-out.md)

---

## Step-by-Step Resolution

### Step 1: Verify User Identity (Mandatory Security Step)
1. Ask the user to provide identifying information:
   - Full legal name as it appears in the system
   - Employee ID or badge number
   - Department and manager name
   - Office location or contact number on file
2. Compare the information provided against the user's record in Active Directory:
   - Open Active Directory Users and Computers (ADUC)
   - Search for the user by name or username
   - Open the user's properties and verify the details match
3. If the user cannot provide matching information, do not proceed — escalate to your supervisor
4. If this is a remote user calling in, follow your organization's verification process (e.g., callback to registered phone number, manager confirmation, security questions)
5. Document the verification in the ticket before proceeding

**What to tell the user:** "For security purposes, I need to verify your identity before I can reset your password. I'll ask you a few questions to confirm who you are. This protects your account from unauthorized access."

### Step 2: Reset Password in Active Directory Users and Computers
1. On a domain controller or management workstation with RSAT installed, open Active Directory Users and Computers
   - If you do not have ADUC: Open Server Manager > Add roles and features > Features > Remote Server Administration Tools > Role Administration Tools > AD DS and AD LDS Tools > Active Directory module for Windows PowerShell
2. In the ADUC console, navigate to the user's Organizational Unit (OU)
   - Common locations: "Users" container, or department-specific OUs like "Sales", "Marketing", "IT"
3. Find and right-click the user account
4. Select "Reset Password"
5. In the Reset Password dialog:
   - Enter a new temporary password that meets the organization's password policy requirements:
     - Minimum length (typically 8-12 characters)
     - Complexity (uppercase, lowercase, number, and special character — e.g., Welcome123!)
     - Must not be one of the user's previous passwords
     - Avoid common words, the company name, or the user's name
   - Confirm the password by entering it again
   - Check the box: "User must change password at next logon"
   - Do NOT uncheck this box unless specifically instructed by policy
6. Click "OK" to apply the password reset
7. If the account is also locked, check the box "Unlock the user's account" on the same dialog
8. PowerShell alternative:
   Set-ADAccountPassword -Identity "username" -Reset -NewPassword (ConvertTo-SecureString -AsPlainText "TempPass123!" -Force)
   Unlock-ADAccount -Identity "username"
   Set-ADUser -Identity "username" -ChangePasswordAtLogon $true

**What to tell the user:** "I've reset your password. I'll now give you a temporary password. When you log in, you'll be prompted to change it immediately to something only you know."

### Step 3: Verify Password Policy Compliance
1. The temporary password must comply with the domain password policy
2. Check the policy if needed:
   - Open Group Policy Management Console (GPMC)
   - Or in PowerShell: Get-ADDefaultDomainPasswordPolicy
3. Standard password policy requirements typically include:
   - Minimum password length (usually 8-14 characters)
   - Password must meet complexity requirements (three of four: uppercase, lowercase, number, symbol)
   - Password history enforced (cannot reuse last 5-24 passwords)
   - Minimum password age (usually 1 day — prevents users from cycling through passwords)
4. If the temporary password does not meet the policy, the reset will fail with an error
5. Note: Do not set a password that expires immediately

**What to tell the user:** "Your new password must follow our organization's rules: at least 8 characters, with uppercase, lowercase, a number, and a symbol. It also can't be a password you've used before."

### Step 4: Communicate the Temporary Password Securely
1. Provide the temporary password to the user through a secure method:
   - In person: Have the user type it themselves on their device while you watch
   - Over the phone: Read the password clearly, using phonetic alphabet for ambiguous characters (e.g., "A as in Alpha, 0 as in Zero, l as in Lima, I as in India")
   - Via SMS or secure messaging app if your organization has one
   - Never send passwords via email unless encrypted and permitted by policy
2. Instruct the user clearly:
   - "Your temporary password is: [password]. It is case-sensitive."
   - "When you log in, you will be prompted to change it immediately."
   - "Choose a new password that you have never used before with this account."
3. Remind the user to update the password on all devices:
   - Email on mobile phone (Outlook app or native mail app)
   - Wi-Fi network password if using WPA2-Enterprise with domain credentials
   - Any saved passwords in web browsers or password managers
   - Shared drives or mapped network drives that use domain authentication
   - VPN client if they connect remotely

**What to tell the user:** "After you change your password, remember to update it everywhere — your phone email, any saved passwords, and your VPN. Old saved passwords will keep trying your old password and may lock your account again."

### Step 5: Unlock Account if Also Locked Out
1. Often a password reset request is accompanied by an account lockout
2. Check if the account is locked:
   - In ADUC, open the user's properties and look at the "Account" tab
   - If "Unlock account" is available as a checkbox, the account is currently locked
3. To unlock: Check the "Unlock the user's account" checkbox > Apply > OK
4. Inform the user their account is now unlocked and they should wait 1-2 minutes before attempting to log in
5. If the account locks again immediately after unlock:
   - A device or service is using the old password
   - Check the security event log for Event ID 4740 (Account Locked Out)
   - Look at the "Caller Computer Name" field to identify the source
6. For detailed lockout source identification, see: [Account Locked After Multiple Attempts](./account-locked-out.md)

**What to tell the user:** "Your account was also locked, which happens after too many failed attempts. I've unlocked it. Wait about 2 minutes before trying to log in, and make sure to update your password on your phone and other devices right away."

### Step 6: Verify Successful Login and Password Change
1. Ask the user to restart their computer before logging in (this clears cached credentials)
2. The user should log in with the temporary password at the Windows login screen
3. Windows will display: "The user's password must be changed before signing in"
4. The user enters the temporary password again (current password field)
5. Then enters their new password twice (new password and confirm password)
6. After successful password change, the user should reach their desktop
7. Test access to key resources:
   - Can the user open Outlook and send/receive email?
   - Can the user access mapped network drives or SharePoint?
   - Can the user connect to VPN if remote?
8. If any resource prompts for password again, the user should enter their new password
9. Document in the ticket that the reset was successful

**What to tell the user:** "Once you're logged in with your new password, test everything — email, shared drives, VPN. If anything asks for a password, use your new one. Let me know if anything doesn't work, and I'll stay on the line until you're fully back up."

### Step 7: Educate User on Self-Service Password Reset (SSPR)
1. Inform the user about self-service options to avoid future helpdesk calls:
   - Microsoft 365 / Azure AD SSPR: Users can reset their own password at https://passwordreset.microsoftonline.com
   - Security questions or alternate email/phone: Encourage users to register at https://aka.ms/ssprsetup
2. Walk the user through registering for SSPR if time permits:
   - Go to https://aka.ms/ssprsetup
   - Sign in with domain credentials
   - Register at least two authentication methods (mobile phone, alternate email, security questions)
3. Remind users:
   - Do not share passwords with anyone, including IT staff
   - Create unique passwords not used for personal accounts
   - Consider using a password manager approved by the organization
   - Report any suspicion of account compromise immediately

**What to tell the user:** "You can reset your own password next time without calling us. Let me show you how to set that up now — it takes about 2 minutes and saves you from being locked out in the future."

---

## Alternative Solutions

If the above steps do not resolve the issue, also try:

- Using PowerShell if ADUC is not available: Set-ADAccountPassword and Unlock-ADAccount commands
- Checking if the user account is disabled in ADUC — re-enable if needed
- Verifying the domain controller is reachable from your management workstation
- For hybrid Azure AD environments, forcing a delta sync: Start-ADSyncSyncCycle -PolicyType Delta

---

## Prevention Tips

- Register for Self-Service Password Reset (SSPR) so you can reset your own password without calling the helpdesk
- Use a password manager to store complex, unique passwords for each system
- Update your password on all devices (phone, tablet, home computer) immediately after changing it
- Never share your password with anyone, including IT staff who should never ask for it
- Log out of shared computers completely — do not save your password in browsers on shared devices

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

## Escalation Decision Matrix

| Condition | Action |
|-----------|--------|
| Password reset option grayed out or returns an error | Escalate — possible permission issue |
| Account is a privileged account (Domain Admin, Enterprise Admin) | Escalate — requires additional authorization |
| User's account appears to be disabled, deleted, or missing | Escalate — requires identity team investigation |
| Password reset succeeds but user still cannot authenticate | Escalate — possible Kerberos or replication issue |
| Account keeps locking out repeatedly within minutes | Escalate — see Account Locked article or Tier 2 |
| User reports suspicious activity indicating account compromise | Escalate — follow security incident response |
| Domain controller is unreachable from your workstation | Escalate — network or infrastructure issue |

---

## Related Articles

- [Account Locked After Multiple Attempts](./account-locked-out.md) — If the account is locked and you need to find the source
- [Self-Service Password Reset Guide (SSPR)](../Tier-0-Self-Service/sspr-guide.md) — For users who want to reset without calling the helpdesk
- [Kerberos Authentication Failures & Token Analysis](../Tier-2-Technical-Support/kerberos-auth-failures.md) — Tier 2: Advanced authentication diagnostics

---

## FAQ

**Q: Why must the user change the password at next logon?**
**A:** This ensures that only the user knows their password. Even though you reset it, you know the temporary password. Forcing a change at logon means the user creates a new password that only they know, maintaining security.

**Q: What if the user is remote and cannot contact a domain controller?**
**A:** The user must have line-of-sight to a domain controller to change their password. If remote, they need to connect via VPN first, or use Azure AD SSPR if your organization has hybrid identity configured.

**Q: How long should a temporary password be valid?**
**A:** Ideally, the user should log in and change it immediately. If they cannot log in right away, the temporary password should expire in 24 hours. Check your organization's policy.

---

## PowerShell Commands Quick Reference

| Command | Description |
|---------|-------------|
| Set-ADAccountPassword -Identity "username" -Reset -NewPassword (ConvertTo-SecureString -AsPlainText "TempPass123!" -Force) | Reset user password |
| Set-ADUser -Identity "username" -ChangePasswordAtLogon $true | Force password change at next logon |
| Unlock-ADAccount -Identity "username" | Unlock a locked account |
| Get-ADUser -Identity "username" -Properties LockedOut | Check if account is locked |
| Get-ADDefaultDomainPasswordPolicy | View domain password policy |
| Search-ADAccount -LockedOut | List all currently locked accounts |
| Get-ADUser -Identity "username" -Properties PasswordLastSet, PasswordExpired, PasswordNeverExpires | Check password status |

---

## Was this article helpful?

If this article helped resolve your issue, great. If something was unclear, missing, or did not work, please open a GitHub Issue describing the problem so we can improve it.

Suggest improvements at: https://github.com/EzioLockhart/Tier-1-Support-Knowledge-Base/issues

---

## References

- CompTIA A+ Troubleshooting Methodology: Identify the problem, Establish a theory, Test the theory, Establish a plan of action, Verify functionality, Document findings
- ITIL Incident Management best practices: Prioritize based on impact and urgency; Identity verification is a critical security control
- Microsoft official documentation: Reset a password in Active Directory

---

*Tier: Tier 1 (Help Desk) | Difficulty: L2 (Intermediate) | Estimated Resolution Time: 5-10 minutes | Required Access Level: Administrator | Severity: P1 (Single User Critical)*

---

For internal use. Follow your organization's identity verification and password reset policies.
