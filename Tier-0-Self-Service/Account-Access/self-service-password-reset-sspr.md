# Self-Service Password Reset Guide (SSPR)

- **Category:** Account & Access
- **Tier:** Tier 0 (Self-Service)
- **Version:** 1.0
- **Last Updated:** May 18, 2026
- **Last Reviewed:** May 18, 2026
- **Applies To:** Microsoft 365 Accounts, Azure AD Accounts, Domain Accounts with SSPR Enabled
- **Difficulty:** L0 (Self-Service)
- **Estimated Resolution Time:** 5-10 minutes
- **Required Access Level:** User
- **Severity:** P1 (Single User, Critical — Cannot Log In)
- **Keywords:** password, reset, SSPR, self-service, forgot password, unlock, verification, security
- **Prerequisite Knowledge:** Access to a web browser, access to your registered phone or alternate email

---

## Before You Call the Helpdesk

You can reset your own password without calling IT support. This guide shows you how.

**What you need:**
- Internet access (use your phone's browser if your computer is locked)
- Access to your registered phone (for verification code) or alternate email

---

## Quick Steps

| Situation | Action |
|-----------|--------|
| Forgot your password | Go to Step 1 |
| Password expired | Go to Step 1 |
| Account is locked | Go to Step 4 |
| Want to register for SSPR | Go to Step 5 |
| SSPR not working | Go to Step 6 |

---

## Step 1: Go to the Password Reset Portal

1. Open a web browser on any device (computer, phone, tablet)
2. Go to: **https://passwordreset.microsoftonline.com**
3. You will see: "Get back into your account"

**What to tell yourself:** "I can do this from any device — even my phone. I don't need my work computer."

---

## Step 2: Enter Your Account Information

1. In the "Email or Username" field, type your work email address
   - Example: john.doe@yourcompany.com
2. Complete the CAPTCHA challenge:
   - Type the characters you see in the image
   - If the image is hard to read, click the speaker icon to hear the characters
   - Click "New" to get a different image
3. Click the **"Next"** button

**What to tell yourself:** "Use my full work email address — the same one I use for Outlook and Teams."

---

## Step 3: Verify Your Identity

Choose one of the verification methods you registered previously:

**Option A: Text message to your phone**
1. Select "Text my mobile phone"
2. You will receive a 6-digit code via SMS
3. Enter the code on the screen
4. Click "Next"

**Option B: Phone call**
1. Select "Call my mobile phone"
2. Answer the call when your phone rings
3. Press the # key when instructed
4. The screen will advance automatically

**Option C: Email to alternate address**
1. Select "Email my alternate email"
2. Check your personal email (e.g., Gmail, Yahoo)
3. Find the verification code email
4. Enter the code on the screen
5. Click "Next"

**Option D: Authenticator app**
1. Select "Approve a notification on my authenticator app"
2. Open the Microsoft Authenticator app on your phone
3. Tap "Approve" when the notification appears

**What to tell yourself:** "The code will arrive within 30 seconds. If I don't see it, I'll check my spam folder or try a different method."

---

## Step 4: Set a New Password

1. After verification, you will see: "Choose a new password"
2. Enter a new password that meets these requirements:
   - At least 8 characters (your organization may require more)
   - At least one uppercase letter (A-Z)
   - At least one lowercase letter (a-z)
   - At least one number (0-9)
   - At least one special character (! @ # $ % ^ & *)
   - Cannot be a password you have used before
3. Re-enter the password in the confirmation field
4. Click **"Finish"**

**Password tips:**
- Choose a phrase you can remember: "MyFirstDay@2026!"
- Do not use personal information (birthday, pet name, address)
- Do not reuse passwords from other accounts
- Write it down temporarily if needed — destroy the note after memorizing

---

## Step 5: After Resetting Your Password

1. You will see: "Your password has been reset"
2. Click "Click here to sign in"
3. Log in with your email and new password
4. Update your password everywhere you saved it:
   - Phone email app (Outlook mobile, iPhone Mail, Android Mail)
   - Wi-Fi if your organization uses domain credentials for Wi-Fi
   - VPN client
   - Any saved passwords in web browsers
5. If you use your work account on multiple computers, restart each one before logging in

**IMPORTANT:** If you do not update your password everywhere, those devices will keep trying your old password and may lock your account again.

---

## Step 6: Register for SSPR (First Time Setup)

If you have never registered for SSPR, do it now so you can reset your password later:

1. Go to: **https://aka.ms/ssprsetup**
2. Sign in with your work email and password
3. You will see: "More information required"
4. Click **"Next"**
5. Set up at least two verification methods:
   - **Phone number:** Enter your mobile number for SMS codes
   - **Alternate email:** Enter a personal email address
   - **Authenticator app:** Download Microsoft Authenticator and follow the setup
6. Complete the setup for each method
7. Click **"Finish"**

**Why register now:** If you forget your password later, you can reset it yourself without waiting for IT support.

---

## Step 7: What to Do If SSPR Does Not Work

If you cannot reset your password through SSPR:

1. Try a different verification method if you registered more than one
2. Check that you are entering your full work email address correctly
3. Check your phone has signal (for SMS) or internet (for authenticator app)
4. Check your alternate email's spam folder for the verification code
5. If you never registered for SSPR, you must contact IT support:
   - Call the helpdesk number provided by your organization
   - Be prepared to verify your identity (employee ID, manager name, department)

---

## When to Call the Helpdesk

Contact IT support if:

- You never registered for SSPR and cannot log in
- None of your verification methods work (lost phone, can't access alternate email)
- Your account is locked and SSPR will not unlock it
- You suspect your account has been compromised (strange activity)
- You need your MFA methods reset (new phone, changed phone number)

---

## Prevention Tips

- Register for SSPR now before you forget your password: https://aka.ms/ssprsetup
- Register at least two verification methods in case one is unavailable
- Keep your phone number and alternate email up to date with IT
- Memorize your password or use a password manager
- Do not share your password with anyone — IT will never ask for it

---

## FAQ

**Q: Can I use SSPR from home or on my phone?**
**A:** Yes. SSPR works from any device with internet access. Go to https://passwordreset.microsoftonline.com from any browser.

**Q: How long does the verification code last?**
**A:** SMS and email codes typically expire after 5-10 minutes. If your code expires, request a new one.

**Q: Will SSPR unlock my account if it is locked?**
**A:** Yes. In most organizations, resetting your password through SSPR also unlocks your account automatically.

---

## Was this article helpful?

If this article helped resolve your issue, great. If something was unclear, missing, or did not work, please open a GitHub Issue describing the problem so we can improve it.

Suggest improvements at: https://github.com/EzioLockhart/Complete-IT-Support-Knowledge-Base-Tier-0-to-Tier-3/issues

---

## References

- Microsoft official documentation: Self-Service Password Reset
- ITIL Incident Management best practices: Self-service reduces helpdesk ticket volume

---

*Tier: Tier 0 (Self-Service) | Difficulty: L0 (Self-Service) | Estimated Resolution Time: 5-10 minutes | Required Access Level: User | Severity: P1 (Single User Critical)*

---

For internal use. Share this guide with users before escalating to Tier 1.
