# Account & Access Troubleshooting Guides

| Article | Description |
|---------|-------------|
| [Password Reset — Active Directory](./password-reset-ad.md) | AD password reset, identity verification, force password change, SSPR |
| [Account Locked After Multiple Attempts](./account-locked-out.md) | Account lockout source identification, Event ID 4740, saved credentials |

---

## Active Directory PowerShell Commands Quick Reference

| Command | Description |
|---------|-------------|
| `Set-ADAccountPassword -Identity "username" -Reset -NewPassword (ConvertTo-SecureString -AsPlainText "TempPass123!" -Force)` | Reset user password |
| `Set-ADUser -Identity "username" -ChangePasswordAtLogon $true` | Force password change at next logon |
| `Unlock-ADAccount -Identity "username"` | Unlock a locked account |
| `Get-ADUser -Identity "username" -Properties LockedOut` | Check if account is locked |
| `Search-ADAccount -LockedOut` | List all currently locked accounts |
| `Get-ADDefaultDomainPasswordPolicy` | View domain password policy |
| `Get-ADUser -Identity "username" -Properties PasswordLastSet, PasswordExpired, PasswordNeverExpires` | Check password status |
