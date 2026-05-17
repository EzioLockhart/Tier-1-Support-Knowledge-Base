# Set Up Microsoft Authenticator — Self-Service Guide

- **Category:** MFA & Authentication
- **Tier:** Tier 0 (Self-Service)
- **Version:** 1.0
- **Last Updated:** May 18, 2026
- **Last Reviewed:** May 18, 2026
- **Applies To:** Microsoft Authenticator for iOS, Microsoft Authenticator for Android
- **Difficulty:** L0 (Self-Service)
- **Estimated Resolution Time:** 5-10 minutes
- **Required Access Level:** User
- **Severity:** P1 (Single User, Critical — MFA Setup Required)
- **Keywords:** Microsoft Authenticator, MFA, setup, QR code, two-factor, authentication, app, install
- **Prerequisite Knowledge:** Ability to download apps on your smartphone, access to a computer for QR code scanning

---

## Before You Start

**What you need:**
- Your smartphone (iPhone or Android)
- A computer to display the QR code
- Your work email and password ready
- About 10 minutes of time

**What this does:** The Microsoft Authenticator app adds an extra layer of security to your account. After setup, you will approve sign-ins from your phone instead of typing codes.

---

## Quick Steps

| Step | Action |
|------|--------|
| 1 | Download the app on your phone |
| 2 | Start MFA setup on your computer |
| 3 | Scan the QR code with your phone |
| 4 | Approve a test notification |
| 5 | Enable cloud backup |
| 6 | Test your setup |

---

## Step 1: Download the Microsoft Authenticator App

**On iPhone:**
1. Open the **App Store**
2. Search for "Microsoft Authenticator"
3. Look for the app with the Microsoft logo (a lock icon)
4. Tap **"Get"** and wait for it to download
5. Open the app

**On Android:**
1. Open the **Google Play Store**
2. Search for "Microsoft Authenticator"
3. Look for the app published by "Microsoft Corporation"
4. Tap **"Install"** and wait for it to download
5. Open the app

**What to tell yourself:** "The app is free and takes less than a minute to download. I'll look for the official Microsoft logo to make sure I'm getting the right one."

---

## Step 2: Start MFA Setup on Your Computer

1. On your computer, open a web browser
2. Go to: **https://aka.ms/mfasetup**
3. Sign in with your work email and password
4. You will see: "More information required"
5. Click **"Next"**
6. You will see options for setting up MFA
7. Select **"Mobile app"** from the list
8. Choose **"Receive notifications for verification"**
9. Click **"Set up"**

**What to tell yourself:** "I need to be on a computer for this part because my phone will scan a QR code from the screen."

---

## Step 3: Scan the QR Code with Your Phone

1. On your computer screen, you will see a **QR code** (a square pattern of black and white dots)
2. On your phone, in the Microsoft Authenticator app:
   - Tap the **"+"** (plus sign) in the top-right corner
   - If this is your first time, tap **"Add account"**
3. Select **"Work or school account"**
4. Select **"Scan QR code"**
5. Point your phone's camera at the QR code on your computer screen
   - Hold the phone steady about 15-20 cm from the screen
   - The app will beep or vibrate when it scans successfully
6. If the camera cannot scan:
   - Tap "Enter code manually" on your phone
   - On the computer, click "Can't scan image?"
   - A code and URL will appear — type these into your phone

**What to tell yourself:** "I'll hold my phone steady and make sure the whole QR code fits in the square on my screen. It scans in less than a second."

---

## Step 4: Approve the Test Notification

1. After scanning, your phone will show your work account added
2. Microsoft will send a test notification to your phone
3. On your phone, you will see: "Approve sign-in?"
4. Tap **"Approve"**
5. On your computer, you will see: "Notification approved"
6. Click **"Next"**
7. Click **"Done"**

**What to tell yourself:** "This test proves everything is working. The real approval will look exactly the same when I sign in to my work account."

---

## Step 5: Enable Cloud Backup (Important)

Cloud backup saves your MFA setup so you can restore it if you get a new phone.

1. Open the Microsoft Authenticator app on your phone
2. Tap the **three dots (...)** in the top-right corner
3. Select **"Settings"**
4. Under "Backup", make sure **"Cloud backup"** is turned ON
   - iPhone: It will use your iCloud account
   - Android: It will use your Google account
5. Verify your backup account when prompted

**Why this matters:** If you lose your phone or get a new one, cloud backup lets you restore all your MFA accounts without setting them up again. Without backup, you will need IT to reset your MFA.

---

## Step 6: Test Your Setup

1. Sign out of your work account on your computer
2. Sign back in with your email and password
3. After entering your password, a notification should appear on your phone
4. Tap **"Approve"** on your phone
5. You should be signed in on your computer

**If it works:** You are all set. Future sign-ins will use this same approval process.

**If it does not work:** Go back to https://aka.ms/mfasetup and verify your account is set up with "Mobile app" selected. Try removing and re-adding the account in the authenticator app.

---

## What to Expect Going Forward

| When | What Happens |
|------|-------------|
| Signing into Outlook on a new computer | You will get a notification on your phone to approve |
| Signing into Teams on the web | You will get a notification on your phone to approve |
| Changing your password | You may need to approve with the authenticator app |
| Every 90 days (varies) | You may be asked to re-verify with MFA |

---

## When to Call the Helpdesk

Contact IT support if:

- You cannot scan the QR code and manual entry also fails
- The test notification never arrives on your phone
- You got a new phone and cloud backup was not enabled
- You accidentally deleted the Microsoft Authenticator app
- You are locked out and cannot access your account

---

## Prevention Tips

- Enable cloud backup in the authenticator app right after setup
- Keep the authenticator app updated through your phone's app store
- Do not delete the app even if you do not use it daily
- If you get a new phone, restore from cloud backup before wiping the old phone
- Register a backup MFA method (SMS or alternate email) at https://aka.ms/mfasetup

---

## FAQ

**Q: Do I need internet on my phone for this to work?**
**A:** Yes, for push notifications. However, the app can also generate codes offline. If you have no internet, select "I can't use my Microsoft Authenticator app right now" on the sign-in screen and choose a different method.

**Q: What if I get a new phone?**
**A:** If you enabled cloud backup, install the app on your new phone, select "Restore from backup", and all your accounts will be restored. If you did not enable backup, you must contact IT to reset your MFA.

**Q: Will this drain my phone battery?**
**A:** No. The app uses minimal battery. It only activates when you receive a sign-in notification.

---

## Was this article helpful?

If this article helped resolve your issue, great. If something was unclear, missing, or did not work, please open a GitHub Issue describing the problem so we can improve it.

Suggest improvements at: https://github.com/EzioLockhart/Complete-IT-Support-Knowledge-Base-Tier-0-to-Tier-3/issues

---

## References

- Microsoft official documentation: Set up Microsoft Authenticator
- ITIL Incident Management best practices: Self-service MFA setup reduces helpdesk ticket volume

---

*Tier: Tier 0 (Self-Service) | Difficulty: L0 (Self-Service) | Estimated Resolution Time: 5-10 minutes | Required Access Level: User | Severity: P1 (Single User Critical)*

---

For internal use. Share this guide with users before escalating to Tier 1.
