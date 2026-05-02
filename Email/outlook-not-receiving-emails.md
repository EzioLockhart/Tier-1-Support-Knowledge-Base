# Outlook Not Receiving New Emails

- **Category:** Email
- **Tier:** Tier 1 (Help Desk)
- **Version:** 1.0
- **Last Updated:** May 2, 2026
- **Last Reviewed:** May 2, 2026
- **Applies To:** Microsoft Outlook 2016, 2019, 2021, Microsoft 365 (Windows & Mac)
- **Difficulty:** L1 (Basic)
- **Estimated Resolution Time:** 10-20 minutes
- **Required Access Level:** User
- **Severity:** P1 (Single User, Critical — Cannot Receive Email)
- **Keywords:** Outlook, not receiving, inbox empty, sync, Work Offline, OST, profile, Focused Inbox, rules
- **Prerequisite Knowledge:** Basic Outlook navigation, ability to open Settings and check account details

---

## Symptoms

- New emails not appearing in inbox despite being visible on webmail or mobile
- Send/Receive shows no errors but inbox remains unchanged
- Last email received was hours or days ago
- Colleagues confirm they sent emails that never arrived
- Outlook status bar shows "Connected" or "Updating Inbox" indefinitely

---

## Common Error Codes

| Code | Meaning |
|------|---------|
| 0x8004010F | Outlook data file cannot be accessed — OST file corruption |
| 0x800CCC0F | Connection to server was interrupted — sync failure |
| 0x80040119 | Unknown error during send/receive operation |
| 0x80040600 | Mailbox storage quota exceeded — server rejected email |

---

## Symptom-to-Step Mapping

| If You See This | Skip To |
|-----------------|---------|
| Status bar shows "Working Offline" | Step 1 |
| Inbox shows "Filtered" or "Unread" only | Step 2 |
| Emails appear in webmail but not Outlook | Step 4 |
| Mailbox is nearly full | Step 5 |
| Outlook crashes or freezes during sync | Step 6 |

---

## Triage Questions

Before starting troubleshooting, ask the user:

1. "Can you see new emails when you log into webmail through a browser?"
2. "Does the bottom-left corner of Outlook say 'Connected', 'Disconnected', or 'Working Offline'?"
3. "Are you using Focused Inbox? Have you checked the 'Other' tab?"
4. "Do you know roughly how full your mailbox is, or have you received any storage warning messages?"

---

## Quick Checks (30 seconds)

1. Check if emails appear in webmail (outlook.office.com or Gmail.com) — if yes, problem is local to Outlook
2. Verify internet connection by opening a browser and loading any website
3. Check the Outlook status bar (bottom-left) — does it say "Connected", "Disconnected", or "Working Offline"?
4. Look at the Send/Receive progress indicator in the status bar — is it stuck or showing errors?
5. Check if the inbox filter is active (e.g., "Unread" or "This Week" showing instead of "All")
6. Switch between "Focused" and "Other" inbox tabs if using Focused Inbox — new emails may be landing in the Other tab
7. If you can send emails but cannot receive new ones, see: [Unable to Send Emails (Stuck in Outbox)](./unable-to-send-emails.md)

---

## Step-by-Step Resolution

### Step 1: Disable and Re-enable Work Offline Mode
1. In Outlook, go to the Send/Receive tab on the ribbon
2. Look for the "Work Offline" button — if it is highlighted or pressed, click it to disable offline mode
3. Wait 30 seconds for Outlook to reconnect and sync
4. Click "Send/Receive All Folders" or press F9 to force a manual sync

**What to tell the user:** "Outlook has a Work Offline mode that stops all email traffic. Sometimes it gets turned on accidentally or after a network interruption. We're going to check if it's enabled and turn it off. This is the most common cause of not receiving emails."

### Step 2: Check Inbox Filters and View Settings
1. In your inbox, look at the top of the message list for any active filter (e.g., "Unread", "This Week", "Flagged")
2. Click the filter text and select "All" to clear all filters
3. Go to the View tab > "View Settings" > "Filter"
4. Click "Clear All" then OK to remove all filters
5. If using Focused Inbox, click the "Other" tab — new emails from unknown senders may appear there instead of "Focused"
6. Check if hidden emails now appear

**What to tell the user:** "Outlook can filter your inbox to show only certain types of emails, like unread messages or emails from this week. We're going to make sure no filters are hiding your new emails. Also, if you use Focused Inbox, new senders often land in the Other tab."

### Step 3: Check Junk Email Folder and Rules
1. In the left folder pane, click "Junk Email" (or "Spam" depending on account type)
2. Look for any legitimate emails that were incorrectly filtered
3. If you find one, right-click it > "Junk" > "Not Junk" to train the filter and move it to inbox
4. Go to File > "Manage Rules & Alerts"
5. Review all active rules — look for rules that move, delete, forward, or redirect incoming emails
6. Temporarily uncheck suspicious rules, click Apply, and test by sending yourself an email from another account

**What to tell the user:** "Sometimes legitimate emails get caught by the spam filter, or an email rule you created in the past is now moving new emails to an unexpected folder. We're going to check both places."

### Step 4: Check Account Settings and Server Connection
1. Go to File > "Account Settings" > "Account Settings"
2. Select your email account and click "Repair" (Outlook 365/2019+) or "Change" (Outlook 2016)
3. Verify the incoming mail server settings are correct
4. Click "Test Account Settings" and check for any errors in the results window
5. If using Gmail, ensure IMAP is enabled in Gmail settings: Gmail > Settings gear icon > See all settings > Forwarding and POP/IMAP > Enable IMAP > Save Changes
6. Restart Outlook after any changes

**What to tell the user:** "We're going to verify that Outlook can actually reach your email server. The repair tool checks the connection and fixes common configuration problems automatically."

### Step 5: Check Mailbox Storage Quota
1. Log into your email account via webmail (outlook.office.com, Gmail.com, etc.)
2. Check your mailbox storage usage — usually visible at the bottom of the folder pane or in Settings > Storage
3. If your mailbox is full or near full (e.g., 49.5 GB out of 50 GB for Microsoft 365):
   - Delete or archive old emails, especially those with large attachments
   - Empty the "Deleted Items" and "Junk Email" folders
   - In Outlook, go to File > Tools > "Mailbox Cleanup" to find large items
4. After freeing space, wait 10-15 minutes for new emails to start flowing again

**What to tell the user:** "Your mailbox has a size limit, and when it's full, the email server rejects new messages. Think of it like a full physical mailbox — the postal worker can't put anything new in. We need to free up space by removing old emails and emptying the trash."

### Step 6: Clear Outlook Cache and Rebuild OST File
1. Close Outlook completely (verify no Outlook.exe in Task Manager > Processes)
2. Open Control Panel > Mail (Microsoft Outlook)
3. Click "Email Accounts" > select your account > "Repair"
4. Wait for the repair process to complete, then test Outlook
5. If repair does not help, close Outlook again and navigate to: %LocalAppData%\Microsoft\Outlook
6. Find the .ost file for your account (named after your email address)
7. Rename the file to add ".old" at the end (e.g., username@domain.com.ost.old)
8. Restart Outlook — a new OST file will be created and all emails will re-sync from the server

**What to tell the user:** "Outlook keeps a local copy of your mailbox called an OST file. Sometimes this file gets corrupted, which stops new emails from appearing. We're going to rename the old file and let Outlook create a fresh copy. This can take several minutes for large mailboxes, but your emails are safe on the server."

### Step 7: Create a New Outlook Profile
1. Close Outlook completely
2. Open Control Panel > Mail (Microsoft Outlook)
3. Click "Show Profiles"
4. Click "Add" and create a new profile with your email account details
5. Name it something like "Outlook-New" to distinguish from the old profile
6. Under "When starting Microsoft Outlook, use this profile", select "Always use this profile" and choose the new one
7. Open Outlook — it will download all emails fresh from the server
8. If emails now arrive normally, the old profile was corrupted

**What to tell the user:** "Your Outlook profile stores all your email account configurations. Sometimes a profile gets corrupted at a deep level that repairs can't fix. We're creating a brand new profile, which is like giving Outlook a fresh start. Your emails are safe — they'll all download again from the server."

---

## Alternative Solutions

If the above steps do not resolve the issue, also try:

- Running Outlook in Safe Mode (outlook.exe /safe) to rule out add-in conflicts
- Disabling antivirus email scanning temporarily to test if it's blocking incoming mail
- Checking with your email administrator if there are mail flow rules blocking specific senders
- Using Outlook on the web (OWA) as a workaround while the desktop issue is investigated

---

## Prevention Tips

- Empty your Deleted Items and Junk Email folders weekly to prevent mailbox quota issues
- Review your email rules every few months to ensure they are still needed
- Keep Outlook updated through File > Office Account > Update Options > Update Now
- Avoid closing Outlook unexpectedly during send/receive operations
- Monitor your mailbox size regularly — aim to stay below 80% of your quota

---

## Root Cause

Common causes of Outlook not receiving emails, in order of likelihood:

- Work Offline mode enabled (most common — often enabled accidentally via button or network interruption)
- Active inbox filter or Focused Inbox hiding new messages from view
- Misconfigured rules automatically moving or deleting incoming emails
- Junk email filter capturing legitimate emails
- Mailbox storage quota full (server rejects new emails silently)
- Corrupted Outlook profile or OST cache file
- Incorrect account server settings or expired password
- IMAP/POP not enabled on the email provider side (especially Gmail and Yahoo)
- Firewall, VPN, or antivirus software blocking Outlook's connection to the mail server

---

## Escalation Decision Matrix

| Condition | Action |
|-----------|--------|
| All 7 steps completed, issue persists | Escalate to Tier 2 |
| Multiple users in the organization report the same issue | Escalate — likely server-side or tenant-wide problem |
| "Test Account Settings" fails after verifying all credentials | Escalate — Exchange admin may need to check server |
| OST file repeatedly becomes corrupted within days of being rebuilt | Escalate — possible disk or profile corruption at system level |
| User reports missing emails that do not appear in webmail either | Escalate urgently — possible data loss |
| Mailbox quota cannot be increased without admin access | Escalate — requires Exchange Admin Center |
| Issue resolved after new profile | Do not escalate — document solution |

---

## Related Articles

- [Unable to Send Emails (Stuck in Outbox)](./unable-to-send-emails.md) — If you can receive but cannot send emails
- [Self-Service Password Reset Guide (SSPR)](../Tier-0-Self-Service/sspr-guide.md) — If you need to reset your email password

---

## FAQ

**Q: Why do emails appear on my phone but not in Outlook on my computer?**
**A:** Your phone uses a different sync method (usually ActiveSync or IMAP) that connects directly to the email server. If emails appear on your phone, the problem is specifically with Outlook on your computer — not with your email account itself.

**Q: Will rebuilding my OST file delete any emails?**
**A:** No. The OST file is just a local copy. All your emails, folders, calendar items, and contacts are stored on the email server. When you rebuild the OST, Outlook downloads a fresh copy from the server.

**Q: How long should a mailbox sync take after rebuilding the OST?**
**A:** It depends on your mailbox size and internet speed. A 10 GB mailbox on a fast connection can take 30-60 minutes. Outlook is usable during the sync, but some older emails may not appear until the sync completes.

---

## Commands and Shortcuts Quick Reference

| Action | How To Access |
|--------|---------------|
| Force Send/Receive | Send/Receive tab > Send/Receive All Folders, or press F9 |
| Toggle Work Offline | Send/Receive tab > Work Offline button |
| Open Mail control panel | Control Panel > Mail (Microsoft Outlook) |
| Manage Rules & Alerts | File > Manage Rules & Alerts |
| Account repair | File > Account Settings > Select account > Repair |
| Mailbox Cleanup tool | File > Tools > Mailbox Cleanup |
| OST file location | %LocalAppData%\Microsoft\Outlook |
| Open Outlook in Safe Mode | Win + R > outlook.exe /safe |

---

## Was this article helpful?

If this article helped resolve your issue, great. If something was unclear, missing, or did not work, please open a GitHub Issue describing the problem so we can improve it.

Suggest improvements at: https://github.com/EzioLockhart/Tier-1-Support-Knowledge-Base/issues

---

## References

- CompTIA A+ Troubleshooting Methodology: Identify the problem, Establish a theory, Test the theory, Establish a plan of action, Verify functionality, Document findings
- ITIL Incident Management best practices: Prioritize based on impact and urgency
- Microsoft official documentation: Fix Outlook email sync issues

---

*Tier: Tier 1 (Help Desk) | Difficulty: L1 (Basic) | Estimated Resolution Time: 10-20 minutes | Required Access Level: User | Severity: P1 (Single User Critical)*

---

For internal use. Follow your organization's escalation procedures.
