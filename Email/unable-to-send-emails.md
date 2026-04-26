# Unable to Send Emails (Stuck in Outbox)

**Category:** Email
**Last Updated:** April 27, 2026
**Applies To:** Microsoft Outlook 2016, 2019, 2021, Microsoft 365 (Windows & Mac)

---

## Symptoms

- Email sent by user gets stuck in the Outbox folder and never sends
- Multiple emails accumulating in Outbox with none being delivered
- Send/Receive progress bar appears briefly but Outbox remains full
- Recipients confirm they never received the email
- No bounce-back or delivery failure notification received by sender
- Other incoming emails continue to arrive normally
- Outlook status bar shows "Connected" but sending still fails

---

## Quick Checks (30 seconds)

1. Check if Work Offline mode is enabled — go to the Send/Receive tab and look for the "Work Offline" button; if highlighted, click it to disable
2. Verify internet connectivity by opening a browser and loading any website
3. Look at the Outbox folder — is there one specific email stuck, or are all outgoing emails failing?
4. Check the size of the stuck email — hover over it to see if it has a large attachment (over 10-25 MB)
5. Try sending a quick test email to yourself (your own email address) to isolate whether the issue affects all outgoing mail or just one message

---

## Step-by-Step Resolution

### Step 1: Disable Work Offline Mode and Force Send/Receive

1. In Outlook, go to the **Send/Receive** tab on the ribbon
2. Look for the **"Work Offline"** button — if it is highlighted or appears pressed, click it to disable offline mode
3. Wait 30 seconds for Outlook to reconnect
4. Click **"Send/Receive All Folders"** or press **F9** to force a manual send/receive
5. Check the Outbox — if the email disappears, it has been sent successfully
6. If Work Offline was not enabled, proceed to the next step
   - Work Offline mode is the most common and simplest cause of emails stuck in Outbox; users often enable it accidentally or it activates after a network interruption.

### Step 2: Open and Resend the Stuck Email

1. Navigate to the **Outbox** folder in the left folder pane (under the email account, not the "Outbox" under "Archive" or a PST file)
2. If the Outbox folder shows a number in brackets (e.g., Outbox [3]), emails are stuck there
3. Open the stuck email by double-clicking it
4. Once open, click the **"Send"** button in the email window to attempt sending again
5. If the email still does not send, proceed to Step 3 to delete and recreate it
   - Sometimes an email becomes "stale" in the Outbox because Outlook attempted to send it during a temporary network drop; reopening and clicking Send forces a fresh send attempt.

### Step 3: Delete and Recreate the Stuck Email

1. If opening and resending fails, drag the stuck email from the Outbox to the **Drafts** folder
2. If dragging does not work: open the email, go to **File > Save As**, save it as an Outlook Message Format (.msg) file, then delete the stuck email from Outbox
3. Open the Drafts folder and double-click the email to open it
4. Review the email content and recipient addresses carefully:
   - Check for any typos in recipient email addresses
   - Verify there are no extra spaces or invalid characters
   - Check that distribution lists or groups are valid and not too large
5. Click **"Send"** to try again
6. If the email still gets stuck, the problem may be the attachment — see Step 4
   - Corrupted or oversized emails can get permanently stuck; recreating the email often resolves this.

### Step 4: Check Attachment Size and File Types

1. Many email servers have attachment size limits — typically 10-25 MB for business accounts
2. Open the stuck email and check the total attachment size:
   - Look at the attachments listed in the email header
   - In the email compose window, attachments show their file sizes
3. If the total size exceeds your organization's limit:
   - Remove the attachments from the email
   - Use OneDrive, SharePoint, Google Drive, or another file-sharing service instead
   - Insert the sharing link in the email body
4. Also check for blocked file types — some organizations block .exe, .bat, .zip, or other file types for security
5. Compress large files into a .zip file to reduce size (if .zip files are allowed)
6. Test by sending the email without attachments — if it sends successfully, the attachment was the issue
   - Attachment size limits are the second most common cause of Outbox stuck emails; users may not realize their attachment exceeds the limit.

### Step 5: Verify Recipient Email Addresses and Distribution Lists

1. Open the stuck email from the Outbox
2. Carefully review each recipient email address:
   - Check for common typos (e.g., @gnail.com instead of @gmail.com, @comapny.com instead of @company.com)
   - Remove any double dots, spaces, or invalid characters
   - Verify the domain exists by checking with the recipient or looking up the company domain
3. If sending to a distribution list or group:
   - Try sending to individual recipients instead to isolate if a specific address is causing the failure
   - Check if the distribution list has external recipient restrictions
4. Try sending the email to one person at a time to identify problematic addresses
   - A single invalid or blocked recipient address can prevent the entire email from sending, even if all other recipients are valid.

### Step 6: Check Account Settings and Outgoing Server (SMTP)

1. Go to **File > Account Settings > Account Settings**
2. Select your email account and click **"Repair"** or **"Change"**
3. Verify the outgoing mail server (SMTP) settings:
   - Server address is correct (e.g., smtp.office365.com, smtp.gmail.com)
   - Port number is correct (usually 587 for authenticated SMTP)
   - Encryption method (TLS/SSL) matches what the email provider requires
4. Ensure the option **"My outgoing server (SMTP) requires authentication"** is checked
5. Ensure **"Use same settings as my incoming mail server"** is selected
6. Click **"Test Account Settings"** to verify both incoming and outgoing servers work
7. If the test fails on SMTP, note the error message and check with your email provider or IT team for correct settings
   - Incorrect SMTP server settings will allow receiving emails but prevent sending any outgoing emails.

### Step 7: Reduce the Outbox to Resolve Corruption (Last Resort)

1. If multiple emails are stuck in Outbox, the Outbox folder itself may be corrupted
2. Drag all emails from the Outbox to the Drafts folder (or another folder)
3. If dragging fails, use the "Move to Folder" option (right-click the email > Move > Other Folder > Drafts)
4. Ensure the Outbox is completely empty — Outlook will not send any emails if even one corrupted message is stuck
5. Once the Outbox is empty, restart Outlook
6. After restart, go to Drafts, open one email, and try sending it
7. If it sends successfully, repeat for the remaining emails
8. If the Outbox corruption persists and emails continue to get stuck, create a new Outlook profile:
   - Close Outlook > Control Panel > Mail (Microsoft Outlook) > Show Profiles > Add
   - Add your email account to the new profile
   - Set the new profile as default and restart Outlook
   - An empty Outbox forces Outlook to process sending fresh; corrupted items in Outbox can block all outgoing mail.

---

## Root Cause

Common causes of emails stuck in Outbox, in order of likelihood:

- Work Offline mode accidentally enabled (most common — one click to fix)
- Email attachment too large, exceeding the organization or email provider size limit
- Invalid or misspelled recipient email address causing the send to fail
- SMTP outgoing server settings incorrect or authentication failing
- Corrupted email item in Outbox blocking all other outgoing messages
- Network interruption during the initial send attempt causing the email to get "stuck"
- Conflict with antivirus email scanning feature (some antivirus software scans outgoing emails and can interfere)

---

## Escalation Criteria

Escalate to Tier 2 / Exchange or Email Team if:

- Multiple users in the organization cannot send emails (indicates SMTP server or Exchange issue)
- "Test Account Settings" shows SMTP failure with correct server settings
- Outgoing emails are blocked by a spam filter or mail flow rule that requires Exchange Admin Center access
- User's send-as or send-on-behalf permissions need to be modified
- The user's mailbox has exceeded its sending quota or rate limit
- SMTP relay or connector configuration needs to be changed in Microsoft 365 or Exchange
- The user account requires a mail flow trace to determine why emails are not delivering

---

## Commands and Shortcuts Quick Reference

| Action | How To Access |
|--------|---------------|
| Force Send/Receive | Send/Receive tab > Send/Receive All Folders, or press F9 |
| Toggle Work Offline | Send/Receive tab > Work Offline button |
| Account Settings | File > Account Settings > Account Settings |
| Test Account Settings | File > Account Settings > Select account > Repair > Test Settings |
| Open Outbox folder | Left folder pane > Outbox (under email account) |
| Move email to Drafts | Drag email to Drafts, or right-click > Move > Other Folder |
| Create new Outlook profile | Control Panel > Mail (Microsoft Outlook) > Show Profiles > Add |

---

For internal use. Follow your organization's email and acceptable use policies.
