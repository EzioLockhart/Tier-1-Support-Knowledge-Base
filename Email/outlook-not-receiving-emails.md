# Outlook Not Receiving New Emails

**Category:** Email
**Last Updated:** April 26, 2026
**Applies To:** Microsoft Outlook 2016, 2019, 2021, Microsoft 365 (Windows & Mac)

---

## Symptoms

- New emails not appearing in inbox despite being visible on webmail or mobile
- Send/Receive shows no errors but inbox remains unchanged
- Last email received was hours or days ago
- Colleagues confirm they sent emails that never arrived
- Outlook status bar shows "Connected" or "Updating Inbox" indefinitely
- If you can receive emails but cannot send them, see: [Unable to Send Emails (Stuck in Outbox)](./unable-to-send-emails.md)

---

## Quick Checks (30 seconds)

1. Check if emails appear in webmail (outlook.office.com or Gmail.com) — if yes, problem is local to Outlook
2. Verify internet connection by opening a browser and loading any website
3. Check the Outlook status bar (bottom-left) — does it say "Connected", "Disconnected", or "Working Offline"?
4. Look at the Send/Receive progress indicator in the status bar (bottom of Outlook window) — is it stuck or showing errors?
5. Check if the inbox filter is active (e.g., "Unread" or "This Week" showing instead of "All")
6. Switch between "Focused" and "Other" inbox tabs if using Focused Inbox — new emails may be landing in the Other tab

---

## Step-by-Step Resolution

### Step 1: Disable and Re-enable Work Offline Mode

1. In Outlook, go to the **Send/Receive** tab on the ribbon
2. Look for the **"Work Offline"** button — if it is highlighted or pressed, click it to disable offline mode
3. Wait 30 seconds for Outlook to reconnect and sync
4. Click **"Send/Receive All Folders"** (also on the Send/Receive tab) or press **F9** to force a manual sync
   - This is the most common cause of not receiving emails; users often enable it accidentally by clicking the button or losing network connection temporarily.

### Step 2: Check Inbox Filters and View Settings

1. In your inbox, look at the top of the message list for any active filter (e.g., "Unread", "This Week", "Flagged")
2. Click the filter text and select **"All"** to clear all filters
3. Go to the **View** tab > **"View Settings"** > **"Filter"**
4. Click **"Clear All"** then **OK** to remove all filters
5. If using Focused Inbox, click the **"Other"** tab — new emails from unknown senders may appear there instead of "Focused"
6. Check if hidden emails now appear
   - Filters and Focused Inbox can hide new emails from view, making it appear as though nothing is arriving.

### Step 3: Check Junk Email Folder and Rules

1. In the left folder pane, click **"Junk Email"** (or "Spam" depending on account type)
2. Look for any legitimate emails that were incorrectly filtered
3. If you find one, right-click it > **"Junk"** > **"Not Junk"** to train the filter and move it to inbox
4. Check the **"Mark as not junk"** box in the dialog that appears to add sender to Safe Senders list
5. Go to **File** > **"Manage Rules & Alerts"**
6. Review all active rules — look for rules that **move**, **delete**, **forward**, or **redirect** incoming emails
7. Temporarily uncheck suspicious rules, click **Apply**, and test by sending yourself an email from another account
   - An incorrectly configured rule is a common reason emails seem to "disappear" after arrival.

### Step 4: Check Account Settings and Server Connection

1. Go to **File** > **"Account Settings"** > **"Account Settings"**
2. Select your email account and click **"Repair"** (Outlook 365/2019+) or **"Change"** (Outlook 2016)
3. Verify the incoming mail server settings are correct (confirm with IT or email provider documentation)
4. Click **"Test Account Settings"** and check for any errors in the results window
5. If using Gmail, ensure **IMAP is enabled** in Gmail settings (Gmail > Settings gear icon > See all settings > Forwarding and POP/IMAP > Enable IMAP > Save Changes)
6. Restart Outlook after any changes
   - Incorrect server settings or disabled IMAP will prevent Outlook from downloading new emails.

### Step 5: Check Mailbox Storage Quota

1. Log into your email account via webmail (outlook.office.com, Gmail.com, etc.)
2. Check your mailbox storage usage — usually visible at the bottom of the folder pane or in Settings > Storage
3. If your mailbox is full or near full (e.g., 49.5 GB out of 50 GB for Microsoft 365):
   - Delete or archive old emails, especially those with large attachments
   - Empty the "Deleted Items" and "Junk Email" folders
   - In Outlook, go to File > Tools > **"Mailbox Cleanup"** to find large items
4. After freeing space, wait 10-15 minutes for new emails to start flowing again
   - A full mailbox is a frequently overlooked cause; the server rejects new emails when storage is exhausted.

### Step 6: Clear Outlook Cache and Rebuild OST File

1. Close Outlook completely (verify no Outlook.exe in Task Manager > Processes)
2. Open **Control Panel** > **Mail (Microsoft Outlook)**
3. Click **"Email Accounts"** > select your account > **"Repair"**
4. Wait for the repair process to complete, then test Outlook
5. If repair does not help, close Outlook again and navigate to:

%LocalAppData%\Microsoft\Outlook

6. Find the **.ost** file for your account (named after your email address, e.g., username@domain.com.ost)
7. Rename the file to add ".old" at the end (e.g., username@domain.com.ost.old)
8. Restart Outlook — a new OST file will be created and all emails will re-sync from the server
   - This can take several minutes for large mailboxes; do not interrupt the process.
   - This resolves issues caused by a corrupted local cache file.

### Step 7: Create a New Outlook Profile (Last Resort)

1. Close Outlook completely
2. Open **Control Panel** > **Mail (Microsoft Outlook)**
3. Click **"Show Profiles"**
4. Click **"Add"** and create a new profile with your email account details
5. Name it something like "Outlook-New" to distinguish from the old profile
6. Under "When starting Microsoft Outlook, use this profile", select **"Always use this profile"** and choose the new one
7. Open Outlook — it will download all emails fresh from the server
8. If emails now arrive normally, the old profile was corrupted; you can delete it after confirming all data is accessible
   - This is a clean slate fix that resolves persistent profile-level corruption.

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

## Escalation Criteria

Escalate to Tier 2 / Exchange Team if:

- Multiple users in the organization report the same issue (indicates server-side or tenant-wide problem)
- "Test Account Settings" fails after verifying all credentials and server details are correct
- The issue persists after creating a brand new Outlook profile
- OST file repeatedly becomes corrupted within days of being rebuilt
- User reports missing emails that do not appear in webmail either — possible data loss, escalate urgently
- Mailbox quota cannot be increased without admin access
- Admin credentials are needed to check Exchange Admin Center or Microsoft 365 Admin Center

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

---

For internal use. Follow your organization's escalation procedures.
