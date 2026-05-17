# MFA Prompt Not Appearing or Code Not Working

- **Category:** MFA & Authentication
- **Tier:** Tier 1 (Help Desk)
- **Version:** 1.0
- **Last Updated:** May 2, 2026
- **Last Reviewed:** May 2, 2026
- **Applies To:** Microsoft Authenticator, Google Authenticator, SMS Codes, Phone Calls, Hardware Tokens, All MFA-Enabled Accounts
- **Difficulty:** L1 (Basic)
- **Estimated Resolution Time:** 10-15 minutes
- **Required Access Level:** User
- **Severity:** P1 (Single User, Critical — Cannot Authenticate)
- **Keywords:** MFA, multi-factor, authentication, prompt, code, authenticator, SMS, verification, not working, expired
- **Prerequisite Knowledge:** Basic smartphone usage, understanding of MFA concept

---

## Symptoms

- MFA prompt does not appear on phone when trying to sign in
- Push notification sent but tapping "Approve" does nothing
- Verification code received but "Incorrect code" error appears
- SMS verification code never arrives on phone
- Phone call verification does not ring or goes to voicemail
- Time-based code from authenticator app is always rejected
- "Authentication failed" or "Verification failed" after entering correct code
- MFA prompt appears but times out before user can respond

---

## Common Error Codes

| Code | Meaning |
|------|---------|
| AADSTS50011 | MFA challenge failed — code expired or incorrect |
| AADSTS50076 | MFA required but user did not complete challenge |
| AADSTS50131 | Conditional Access policy blocked authentication |
| ERROR_TIMEOUT | MFA prompt timed out before user responded |

---

## Symptom-to-Step Mapping

| If You See This | Skip To |
|-----------------|---------|
| Push notification not appearing | Step 1 |
| Code entered but rejected | Step 2 |
| SMS code never arrives | Step 3 |
| Time-based code always wrong | Step 4 |
| MFA prompt timing out | Step 5 |

---

## Triage Questions

Before starting troubleshooting, ask the user:

1. "Are you using the Microsoft Authenticator app, SMS codes, or a phone call for verification?"
2. "Did you recently get a new phone, change your phone number, or reinstall the authenticator app?"
3. "Is your phone connected to the internet right now — either Wi-Fi or cellular data?"
4. "Are you traveling or in a different time zone than usual?"

---

## Quick Checks (30 seconds)

1. Check if your phone has an active internet connection — open a web browser and load any website
2. Open the authenticator app manually — sometimes push notifications are delayed, but the approval may already be waiting in the app
3. Check that your phone's date and time are set to automatic (Settings > Date & time > Set automatically = ON)
4. If using SMS, check that your phone has cellular signal — SMS does not require internet, but does require cell service
5. Try the "I can't use my authenticator app right now" or "Sign in another way" option on the login screen
6. If you need to set up MFA for the first time, see: [Set Up Microsoft Authenticator — Self-Service Guide](../Tier-0-Self-Service/setup-microsoft-authenticator.md)

---

## Step-by-Step Resolution

### Step 1: Check Phone Connectivity and Notifications
1. Push notifications require internet connectivity on your phone
2. Check internet access:
   - Open a web browser on your phone and go to google.com
   - If the page loads, internet is working
   - If not, connect to Wi-Fi or enable cellular data
3. Check notification settings for the authenticator app:
   - iPhone: Settings > Notifications > Microsoft Authenticator (or your authenticator app) > Allow Notifications = ON
   - Android: Settings > Apps > Authenticator > Notifications > Show notifications = ON
4. Check that Do Not Disturb or Focus mode is not blocking notifications
5. Open the authenticator app manually:
   - Microsoft Authenticator: open the app and look for pending approvals
   - Google Authenticator: does not use push — it generates codes
   - Pull down to refresh and check for any waiting approval requests
6. If notification settings were off, turn them on and request a new sign-in to test

**What to tell the user:** "Push notifications are sent over the internet to your phone. If your phone is on airplane mode, has no signal, or notifications are blocked, you won't see the prompt. Let's check your phone's connection and make sure notifications are allowed for the authenticator app."

### Step 2: Verify Time Synchronization (Most Common Fix)
1. Time-based codes (TOTP) depend on your phone's clock being perfectly synchronized
2. If your phone's time is off by even 30 seconds, codes will be rejected
3. Check time settings:
   - iPhone: Settings > General > Date & Time > Set Automatically = ON
   - Android: Settings > System > Date & time > Set time automatically = ON
   - Also ensure "Set time zone automatically" is ON
4. If automatic time was off, toggle it ON, then wait 30 seconds
5. Generate a new code and try again
6. For hardware tokens (key fobs), ensure the device has not been damaged or exposed to magnets
7. This is the number one cause of "code rejected" errors

**What to tell the user:** "Authenticator app codes are based on the current time — like a watch that needs to be perfectly synchronized. If your phone's clock is off by even a few seconds, every code you generate will be wrong. This is the most common reason codes are rejected. Let's make sure your phone sets its time automatically."

### Step 3: Troubleshoot SMS Code Delivery
1. SMS codes are sent over cellular networks, not the internet
2. Check if your phone has cellular signal:
   - Look for signal bars at the top of the screen
   - If no signal, move to a location with better reception
3. Check if your phone can receive any SMS messages:
   - Ask someone to send you a test text message
   - If test messages also do not arrive, the issue is with your cellular service
4. Check SMS filtering:
   - Some phones filter unknown senders into a separate folder
   - Check your SMS spam or junk folder
5. Wait 60 seconds — SMS codes can be delayed during network congestion
6. Try the "Call me" option instead of SMS if available:
   - Voice calls often work when SMS does not
   - Answer the call and follow the automated instructions
7. If traveling internationally, SMS delivery may be unreliable — use an authenticator app instead

**What to tell the user:** "SMS codes are sent through your cellular network, not the internet. If you're in an area with poor cell service, roaming internationally, or your carrier is having issues, SMS codes may be delayed or never arrive. Let's check your cellular signal and try a phone call verification instead."

### Step 4: Re-register MFA Methods or Use Backup Codes
1. If you recently changed phones or reinstalled the authenticator app, your MFA registration may have been lost
2. Check if you have backup codes:
   - Backup codes were provided when you first set up MFA
   - Check where you saved them (printed copy, password manager, secure note)
   - Each backup code can be used once
3. If you cannot access any MFA method:
   - Contact your IT helpdesk or administrator
   - They can reset your MFA methods and allow you to re-register
   - You will need to verify your identity before MFA is reset
4. After MFA is reset, re-register your authenticator app:
   - Go to the MFA setup portal (usually aka.ms/mfasetup or mysignins.microsoft.com/security-info)
   - Follow the steps to add the authenticator app
   - Scan the QR code with your authenticator app
   - Test the new registration immediately
5. Always save backup codes when re-registering

**What to tell the user:** "If you got a new phone or reinstalled the app, your MFA registration may not have transferred. The authenticator app stores your registration locally on the device. We may need to reset your MFA methods so you can set it up fresh on your new phone. Do you have your backup codes saved anywhere?"

### Step 5: Check Account Lockout and Conditional Access
1. Too many failed MFA attempts can temporarily lock MFA for your account
2. MFA lockout is typically automatic and lasts 5-15 minutes
3. During lockout, even correct codes will be rejected
4. Wait 10-15 minutes without attempting login, then try again
5. Check if your organization uses Conditional Access policies:
   - Some policies block access from certain locations, devices, or networks
   - If you are traveling, on a new device, or using an unrecognized network, MFA may be blocked
   - The error message usually indicates if Conditional Access is the cause
6. If Conditional Access is suspected:
   - Try signing in from a known location or device
   - Connect to your organization's VPN before attempting MFA
   - Contact IT to check Conditional Access policies affecting your account

**What to tell the user:** "After too many failed MFA attempts, the system may temporarily block further attempts as a security measure. It's like getting locked out after too many wrong PIN entries. Let's wait 10-15 minutes and try again. Also, if you're traveling or on a new device, your organization may be blocking access for security reasons."

### Step 6: Reinstall the Authenticator App
1. If the authenticator app itself is malfunctioning:
2. Do NOT uninstall the app without ensuring you have another MFA method or backup codes — uninstalling deletes all registrations
3. If you have another MFA method or backup codes:
   - Uninstall the authenticator app
   - Restart your phone
   - Reinstall the authenticator app from the official app store
   - Re-register your accounts (Step 4)
4. For Microsoft Authenticator specifically:
   - The app has a built-in recovery feature if you enabled cloud backup
   - Open the app > three dots > "Settings" > "Backup" > check if a backup exists
   - On reinstall, choose "Restore from backup"
5. After reinstall, test with a new sign-in

**What to tell the user:** "The authenticator app itself may have a problem. Reinstalling it can fix app-specific bugs, but it also deletes your registrations. Before we do this, let's make sure you have another way to sign in — backup codes, SMS, or we'll have IT reset your MFA first."

---

## Alternative Solutions

If the above steps do not resolve the issue, also try:

- Using a different MFA method entirely (switch from push to SMS, or from SMS to phone call)
- Signing in from a different device or browser to rule out device-specific issues
- Clearing the browser cache and cookies, then attempting login again
- Using the "Sign in another way" link on the MFA prompt screen to try an alternative method

---

## Prevention Tips

- Register at least two MFA methods (e.g., authenticator app AND phone number) for redundancy
- Save your backup codes in a secure location — a password manager, printed copy, or encrypted note
- Enable cloud backup in Microsoft Authenticator (app settings > Backup) before changing phones
- Keep your phone's date and time set to automatic to prevent code synchronization issues
- Before traveling internationally, ensure you have a reliable MFA method that does not depend on SMS

---

## Root Cause

Common causes of MFA failures, in order of likelihood:

- Phone's date and time not set to automatic — time-based codes are out of sync (most common)
- Phone not connected to the internet — push notifications cannot be delivered
- Notification permissions disabled for the authenticator app
- MFA registration lost after phone change, app reinstall, or device reset
- Too many failed attempts causing temporary MFA lockout
- SMS codes delayed or blocked by cellular network issues
- Conditional Access policy blocking authentication from unrecognized location or device
- Authenticator app outdated or corrupted

---

## Escalation Decision Matrix

| Condition | Action |
|-----------|--------|
| All 6 steps completed, issue persists | Escalate to Tier 2 |
| User cannot access any MFA method and has no backup codes | Escalate — MFA reset required by administrator |
| MFA reset required for account | Escalate — requires identity verification and admin action |
| Multiple users in the organization report same MFA issue | Escalate — possible tenant-wide MFA service issue |
| Conditional Access policy blocking legitimate access | Escalate — policy review required |
| User's phone was lost or stolen | Escalate — security incident, revoke sessions immediately |
| Time sync and app reinstall resolve the issue | Do not escalate — document solution |

---

## Related Articles

- [Set Up Microsoft Authenticator — Self-Service Guide](../Tier-0-Self-Service/setup-microsoft-authenticator.md) — Tier 0: Self-service MFA setup
- [Conditional Access Policy Troubleshooting](../Tier-2-Technical-Support/conditional-access-policy.md) — Tier 2: Advanced Conditional Access diagnostics
- [Federation Trust & ADFS Claim Rule Diagnostics](../Tier-3-Expert-Engineering/federation-trust-adfs.md) — Tier 3: Expert identity federation

> **Note:** The following related articles are planned for future creation within their respective tier folders:
> - [Set Up Microsoft Authenticator — Self-Service Guide](../Tier-0-Self-Service/setup-microsoft-authenticator.md)
> - [Conditional Access Policy Troubleshooting](../Tier-2-Technical-Support/conditional-access-policy.md)
> - [Federation Trust & ADFS Claim Rule Diagnostics](../Tier-3-Expert-Engineering/federation-trust-adfs.md)

---

## FAQ

**Q: Why does my authenticator code work on one account but not another?**
**A:** Each account has its own secret key and time synchronization. If codes work for one account but fail for another, the failing account may have its registration out of sync. Re-register the problematic account. Also check if the failing account uses a different MFA policy.

**Q: Can I use the same authenticator app on multiple phones?**
**A:** Most authenticator apps do not sync across devices automatically. Microsoft Authenticator supports cloud backup (iOS and Android), which can restore your accounts on a new device. Google Authenticator does not support backup — you must re-register all accounts if you change phones.

**Q: What is the difference between a verification code and a push notification?**
**A:** A verification code (6-digit number) is generated by the authenticator app and you type it into the login screen. A push notification pops up on your phone and you tap "Approve" or "Deny". Push is faster and more secure, but requires internet. Codes work without internet but must be time-synchronized.

---

## MFA Methods Quick Reference

| Method | Requires Internet | Requires Cell Signal | Reliable When Traveling |
|--------|:----------------:|:--------------------:|:-----------------------:|
| App Push Notification | Yes | No | Yes (on Wi-Fi) |
| App Verification Code | No (after setup) | No | Yes |
| SMS Code | No | Yes | Unreliable |
| Phone Call | No | Yes | Yes (if roaming) |
| Hardware Token | No | No | Yes |
| Backup Codes | No | No | Yes |

---

## Was this article helpful?

If this article helped resolve your issue, great. If something was unclear, missing, or did not work, please open a GitHub Issue describing the problem so we can improve it.

Suggest improvements at: https://github.com/EzioLockhart/Complete-IT-Support-Knowledge-Base-Tier-0-to-Tier-3/issues

---

## References

- CompTIA A+ Troubleshooting Methodology: Identify the problem, Establish a theory, Test the theory, Establish a plan of action, Verify functionality, Document findings
- ITIL Incident Management best practices: Prioritize based on impact and urgency; MFA failures prevent all access
- Microsoft official documentation: Troubleshoot multi-factor authentication issues
- Microsoft Authenticator App: Backup and recovery

---

*Tier: Tier 1 (Help Desk) | Difficulty: L1 (Basic) | Estimated Resolution Time: 10-15 minutes | Required Access Level: User | Severity: P1 (Single User Critical)*

---

For internal use. Follow your organization's identity and access management policies.
