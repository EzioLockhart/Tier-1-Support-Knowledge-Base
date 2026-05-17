# Outlook Mobile Not Syncing Emails

- **Category:** Mobile Devices
- **Tier:** Tier 1 (Help Desk)
- **Version:** 1.0
- **Last Updated:** May 2, 2026
- **Last Reviewed:** May 2, 2026
- **Applies To:** Microsoft Outlook for iOS, Microsoft Outlook for Android, All Mobile Devices
- **Difficulty:** L1 (Basic)
- **Estimated Resolution Time:** 10-15 minutes
- **Required Access Level:** User
- **Severity:** P2 (Single User, Degraded — Email Not Syncing on Mobile)
- **Keywords:** Outlook, mobile, sync, iPhone, Android, email, not updating, notifications, account
- **Prerequisite Knowledge:** Basic smartphone navigation, ability to access app settings

---

## Symptoms

- Outlook mobile app not showing new emails
- App displays "Not synced" or "Last updated [hours/days ago]" message
- New emails appear on desktop Outlook but not on mobile
- Sent emails from mobile get stuck and never deliver
- App shows "Cannot connect to server" error
- Notifications for new emails not appearing
- Calendar or contacts not syncing along with email

---

## Common Error Codes

| Code | Meaning |
|------|---------|
| Error 0x80072EE7 | Cannot connect to server — network or server unreachable |
| Error 0x80048821 | Authentication failed — password or account issue |
| Error 0x80072F06 | SSL certificate error — secure connection failed |
| Account Not Synced | Outlook mobile cannot reach the Exchange or Microsoft 365 server |

---

## Symptom-to-Step Mapping

| If You See This | Skip To |
|-----------------|---------|
| No emails syncing at all | Step 1 |
| App shows authentication error | Step 2 |
| Sync works on Wi-Fi but not cellular | Step 3 |
| App is outdated | Step 4 |
| Specific folders not syncing | Step 5 |

---

## Triage Questions

Before starting troubleshooting, ask the user:

1. "When was the last time your Outlook mobile app successfully synced emails?"
2. "Are you connected to Wi-Fi or using cellular data right now?"
3. "Have you recently changed your email password?"
4. "Do other apps on your phone have internet access, like your web browser?"

---

## Quick Checks (30 seconds)

1. Check if the phone has an active internet connection — open a web browser and load any website
2. Check if Airplane Mode is accidentally enabled
3. Force close the Outlook app (swipe it away from recent apps) and reopen it
4. Check if the Outlook app needs an update in the App Store (iOS) or Play Store (Android)
5. Verify other email apps or the phone's built-in mail app can sync the same account
6. If you need help setting up email on your device for the first time, see: [Email Setup on iPhone & Android — Quick Guide](../Tier-0-Self-Service/email-setup-mobile.md)

---

## Step-by-Step Resolution

### Step 1: Check Internet Connection and Refresh Sync
1. Verify the device has internet access:
   - Open a web browser and go to google.com
   - If the page loads, internet is working
   - If not, connect to Wi-Fi or enable cellular data
2. Check if Airplane Mode is off: swipe down from top of screen and verify the airplane icon is not active
3. In the Outlook app, manually refresh:
   - iOS: Pull down from the top of the inbox until you see a spinning wheel
   - Android: Pull down from the top of the inbox
4. Check the sync status at the bottom of the inbox — it should show "Up to date" or a recent sync time
5. If the app shows "Not synced", tap the notification to retry

**What to tell the user:** "First, let's make sure your phone has internet access. Sometimes Outlook shows sync errors simply because the phone lost its connection. Let's check your internet first, then manually refresh the app."

### Step 2: Verify Account and Password
1. If you recently changed your email password, the Outlook app still has the old one saved
2. In Outlook mobile, tap your profile icon (top left) > Settings gear icon
3. Select your email account
4. Look for "Password" or "Re-enter password" option
5. Enter your current password
6. If the app does not prompt for a password, try removing and re-adding the account:
   - Settings > your account > "Delete Account" (this only removes from the app, not deletes your email)
   - Tap "Add Account" and sign in fresh with your current credentials
7. Verify the account uses the correct server settings (usually automatic for Microsoft 365 and Gmail)

**What to tell the user:** "If you changed your password recently on your computer, your phone is still trying to use the old one. Each failed attempt counts against your account and can lock it. Let's update the password in the app so it matches what you use on your computer."

### Step 3: Check Cellular Data Permissions (If Sync Fails on Cellular)
1. On iPhone:
   - Settings > Cellular (or Mobile Data)
   - Scroll down to find Outlook in the app list
   - Ensure the toggle is ON (green)
2. On Android:
   - Settings > Apps > Outlook > Mobile data & Wi-Fi
   - Ensure "Background data" is enabled
3. Also check if the phone has Data Saver or Low Data Mode enabled, which can block background sync:
   - iPhone: Settings > Cellular > Cellular Data Options > Data Mode > uncheck "Low Data Mode"
   - Android: Settings > Network & internet > Data Saver > ensure Outlook is exempted

**What to tell the user:** "Some phones block apps from using cellular data to save your data plan. Outlook might work great on Wi-Fi but not on cellular because the phone is stopping it. Let's check your cellular data settings and make sure Outlook is allowed to use mobile data."

### Step 4: Update the Outlook App
1. An outdated app can have sync bugs fixed in newer versions
2. iPhone: Open App Store > tap your profile icon > scroll down to find Outlook > tap "Update"
3. Android: Open Play Store > tap your profile icon > Manage apps & device > find Outlook > tap "Update"
4. If no update is available, the app is current
5. After updating, force close and reopen the app
6. Check sync status again

**What to tell the user:** "App developers release updates to fix sync bugs. If your Outlook app is outdated, it might have a known issue that's already been patched. Let's check for updates in your app store."

### Step 5: Check Notification Settings (If Emails Arrive But No Alerts)
1. If emails sync but you do not get notified:
2. iPhone:
   - Settings > Notifications > Outlook
   - Ensure "Allow Notifications" is ON
   - Check alert style is set to Banners or Alerts, not "None"
3. Android:
   - Settings > Apps > Outlook > Notifications
   - Ensure "Show notifications" is ON
   - Check individual notification categories (Mail, Calendar, etc.) are enabled
4. In Outlook app itself:
   - Settings > Notifications
   - Ensure "Mail" notifications are enabled
   - Check your preferred accounts are selected for notifications
5. Also check if Focus/Do Not Disturb mode is silencing notifications

**What to tell the user:** "Your emails are syncing fine, but your phone isn't alerting you. This is usually a notification setting in the phone itself, not in Outlook. Let's check both the app's notification settings and your phone's notification settings."

### Step 6: Clear App Cache and Data (Android) or Reinstall (iOS)
1. For Android:
   - Settings > Apps > Outlook
   - Tap "Storage & cache"
   - Tap "Clear cache" (this does not delete your emails or settings)
   - If still not syncing, tap "Clear storage" (this removes the app data; you will need to sign in again)
2. For iPhone:
   - There is no cache clearing option; instead, delete and reinstall the app
   - Press and hold the Outlook app icon > "Remove App" > "Delete App"
   - Go to App Store, search for Outlook, and reinstall
   - Sign in with your email account again
3. After clearing cache or reinstalling, set up your account again and test sync

**What to tell the user:** "Sometimes the app's temporary files get corrupted and prevent syncing. On Android, we can clear just the cache. On iPhone, we'll do a quick delete and reinstall. Your emails are safe on the server — they'll all sync back once you sign in again."

---

## Alternative Solutions

If the above steps do not resolve the issue, also try:

- Checking if your mailbox is full (log into webmail and check storage quota)
- Removing and re-adding your email account in the Outlook app
- Testing with the phone's built-in mail app — if it also fails, the issue is account-related, not app-related
- Checking with your IT department if mobile access is allowed for your account (some organizations restrict it)

---

## Prevention Tips

- Update your Outlook app password immediately after changing your domain or email password
- Keep the Outlook app updated through your device's app store
- Connect to Wi-Fi periodically to allow larger sync operations
- Regularly check your mailbox storage to avoid hitting the quota
- Enable biometric unlock (Face ID or fingerprint) in Outlook settings for faster access

---

## Root Cause

Common causes of Outlook mobile not syncing, in order of likelihood:

- Phone not connected to the internet or Airplane Mode enabled (most common)
- Password changed on another device but not updated in the app
- Cellular data permission disabled for Outlook
- Outdated Outlook app version with sync bugs
- Corrupted app cache or temporary data
- Notification settings misconfigured on the phone or in the app
- Mailbox storage quota full, preventing new email delivery
- Account permissions or mobile access restricted by IT policy

---

## Escalation Decision Matrix

| Condition | Action |
|-----------|--------|
| All 6 steps completed, issue persists | Escalate to Tier 2 |
| Issue affects multiple users in the organization | Escalate — likely server-side or tenant-wide issue |
| User cannot authenticate even with correct password | Escalate — possible account lock or MFA issue |
| Built-in mail app also fails to sync the same account | Escalate — account or server configuration issue |
| App reinstalled and issue returns within days | Escalate — possible device or profile conflict |
| Mobile device management (MDM) policy suspected as blocker | Escalate — MDM team needed |
| Cache clearing or reinstall resolves the issue | Do not escalate — document solution |

---

## Related Articles

- [Email Setup on iPhone & Android — Quick Guide](../Tier-0-Self-Service/email-setup-mobile.md) — Tier 0: Self-service mobile email setup
- [Mobile Device Management (MDM) Enrollment Issues](../Tier-2-Technical-Support/mdm-enrollment-issues.md) — Tier 2: Advanced mobile device diagnostics
- [Mobile Connectivity — APN & Certificate Diagnostics](../Tier-3-Expert-Engineering/mobile-connectivity-apn.md) — Tier 3: Expert mobile connectivity analysis

> **Note:** The following related articles are planned for future creation within their respective tier folders:
> - [Email Setup on iPhone & Android — Quick Guide](../Tier-0-Self-Service/email-setup-mobile.md)
> - [Mobile Device Management (MDM) Enrollment Issues](../Tier-2-Technical-Support/mdm-enrollment-issues.md)
> - [Mobile Connectivity — APN & Certificate Diagnostics](../Tier-3-Expert-Engineering/mobile-connectivity-apn.md)

---

## FAQ

**Q: Why do my emails sync on Wi-Fi but not on cellular data?**
**A:** Your phone likely has cellular data disabled for Outlook. Check Settings > Cellular (iPhone) or Settings > Apps > Outlook > Mobile data (Android) and ensure data access is enabled. Also check Data Saver mode is not blocking background sync.

**Q: Will deleting the Outlook app from my phone delete my emails?**
**A:** No. Your emails, calendar, and contacts are stored on the server (Microsoft 365, Exchange, Gmail). Deleting the app only removes the local copy. When you reinstall and sign in, everything syncs back.

**Q: Why do I get notifications on my computer but not my phone?**
**A:** Outlook mobile notifications are separate from desktop notifications. Check your phone's notification settings for the Outlook app, and also check Focus/Do Not Disturb mode. If your phone is set to silent, you may not see alerts even though emails are syncing.

---

## Quick Reference: Outlook Mobile Settings Locations

| Setting | iPhone Path | Android Path |
|---------|-------------|--------------|
| Cellular Data | Settings > Cellular > Outlook | Settings > Apps > Outlook > Mobile data |
| Notifications | Settings > Notifications > Outlook | Settings > Apps > Outlook > Notifications |
| App Update | App Store > Profile > Updates | Play Store > Profile > Manage apps |
| Clear Cache | (Not available — reinstall) | Settings > Apps > Outlook > Storage > Clear cache |
| Account Settings | Outlook > Profile > Settings gear > Account | Outlook > Profile > Settings gear > Account |

---

## Was this article helpful?

If this article helped resolve your issue, great. If something was unclear, missing, or did not work, please open a GitHub Issue describing the problem so we can improve it.

Suggest improvements at: https://github.com/EzioLockhart/Complete-IT-Support-Knowledge-Base-Tier-0-to-Tier-3/issues

---

## References

- CompTIA A+ Troubleshooting Methodology: Identify the problem, Establish a theory, Test the theory, Establish a plan of action, Verify functionality, Document findings
- ITIL Incident Management best practices: Prioritize based on impact and urgency
- Microsoft official documentation: Troubleshoot Outlook mobile sync issues

---

*Tier: Tier 1 (Help Desk) | Difficulty: L1 (Basic) | Estimated Resolution Time: 10-15 minutes | Required Access Level: User | Severity: P2 (Single User Degraded)*

---

For internal use. Follow your organization's mobile device and email policies.
