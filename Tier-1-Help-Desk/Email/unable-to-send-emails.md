# Unable to Send Emails (Stuck in Outbox)

- **Category:** Email
- **Tier:** Tier 1 (Help Desk)
- **Version:** 1.0
- **Last Updated:** May 2, 2026
- **Last Reviewed:** May 2, 2026
- **Applies To:** Microsoft Outlook 2016, 2019, 2021, Microsoft 365 (Windows & Mac)
- **Difficulty:** L1 (Basic)
- **Estimated Resolution Time:** 10-20 minutes
- **Required Access Level:** User
- **Severity:** P1 (Single User, Critical — Cannot Send Email)
- **Keywords:** Outlook, cannot send, Outbox stuck, email stuck, SMTP, attachment, Work Offline, sending failed
- **Prerequisite Knowledge:** Basic Outlook navigation, ability to check account settings

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

## Common Error Codes

| Code | Meaning |
|------|---------|
| 0x800CCC0F | Connection to outgoing mail server was interrupted |
| 0x800CCC78 | Sender email address rejected by server — possible authentication issue |
| 0x8004210B | Operation timed out waiting for outgoing server response |
| 0x800CCC6F | SMTP protocol error — outgoing mail server rejected the message |

---

## Symptom-to-Step Mapping

| If You See This | Skip To |
|-----------------|---------|
| Work Offline is highlighted in ribbon | Step 1 |
| Only one specific email is stuck | Step 2 |
| Email has large attachments | Step 4 |
| Recipient name is underlined in red | Step 5 |
| "Test Account Settings" shows SMTP failure | Step 6 |

---

## Triage Questions

Before starting troubleshooting, ask the user:

1. "Are all outgoing emails stuck, or just one specific email?"
2. "Does the stuck email have any attachments? If yes, roughly how large are they?"
3. "Did you recently change your email password?"
4. "Can you receive emails from others without any problem?"

---

## Quick Checks (30 seconds)

1. Check if Work Offline mode is enabled — go to the Send/Receive tab and look for the "Work Offline" button; if highlighted, click it to disable
2. Verify internet connectivity by opening a browser and loading any website
3. Look at the Outbox folder — is there one specific email stuck, or are all outgoing emails failing?
4. Check the size of the stuck email — hover over it to see if it has a large attachment (over 10-25 MB)
5. Try sending a quick test email to yourself (your own email address) to isolate whether the issue affects all outgoing mail or just one message
6. If you can send emails but cannot receive new ones, see: [Outlook Not Receiving New Emails](./outlook-not-receiving-emails.md)

---

## Step-by-Step Resolution

### Step 1: Disable Work Offline Mode and Force Send/Receive
1. In Outlook, go to the Send/Receive tab on the ribbon
2. Look for the "Work Offline" button — if it is highlighted or appears pressed, click it to disable offline mode
3. Wait 30 seconds for Outlook to reconnect
4. Click "Send/Receive All Folders" or press F9 to force a manual send/receive
5. Check the Outbox — if the email disappears, it has been sent successfully

**What to tell the user:** "Outlook has a Work Offline mode that stops all email traffic, both incoming and outgoing. Sometimes it gets turned on accidentally. We're checking that first because it's the simplest fix — one click and your email may start flowing again."

### Step 2: Open and Resend the Stuck Email
1. Navigate to the Outbox folder in the left folder pane (under the email account)
2. If the Outbox folder shows a number in brackets (e.g., Outbox [3]), emails are stuck there
3. Open the stuck email by double-clicking it
4. Once open, click the "Send" button in the email window to attempt sending again
5. If the email still does not send, proceed to Step 3

**What to tell the user:** "Sometimes an email gets stuck during a brief network interruption. Opening it and clicking Send again forces Outlook to try again with a fresh connection. Let's see if this simple retry works before diving deeper."

### Step 3: Delete and Recreate the Stuck Email
1. If opening and resending fails, drag the stuck email from the Outbox to the Drafts folder
2. If dragging does not work: open the email, go to File > Save As, save it as an Outlook Message Format (.msg) file, then delete the stuck email from Outbox
3. Open the Drafts folder and double-click the email to open it
4. Review the email content and recipient addresses carefully:
   - Check for any typos in recipient email addresses
   - Verify there are no extra spaces or invalid characters
   - Check that distribution lists or groups are valid and not too large
5. Click "Send" to try again

**What to tell the user:** "The email itself might have a small corruption that's causing it to fail every time. We're going to delete the stuck version and recreate it fresh. You won't lose any of your email content — we'll save it to Drafts first."

### Step 4: Check Attachment Size and File Types
1. Many email servers have attachment size limits — typically 10-25 MB for business accounts
2. Open the stuck email and check the total attachment size
3. If the total size exceeds your organization's limit:
   - Remove the attachments from the email
   - Use OneDrive, SharePoint, Google Drive, or another file-sharing service instead
   - Insert the sharing link in the email body
4. Also check for blocked file types — some organizations block .exe, .bat, .zip, or other file types for security
5. Compress large files into a .zip file to reduce size (if .zip files are allowed)
6. Test by sending the email without attachments — if it sends successfully, the attachment was the issue

**What to tell the user:** "Email servers have size limits, and your attachment might be too large. Think of it like trying to mail a package that exceeds the weight limit. We'll use a file-sharing link instead, which is actually a better way to share large files anyway."

### Step 5: Verify Recipient Email Addresses and Distribution Lists
1. Open the stuck email from the Outbox
2. Carefully review each recipient email address:
   - Check for common typos (e.g., @gnail.com instead of @gmail.com, @comapny.com instead of @company.com)
   - Remove any double dots, spaces, or invalid characters
3. If sending to a distribution list or group:
   - Try sending to individual recipients instead to isolate if a specific address is causing the failure
   - Check if the distribution list has external recipient restrictions
4. Try sending the email to one person at a time to identify problematic addresses

**What to tell the user:** "A single invalid or blocked recipient address can prevent the entire email from sending, even if everyone else's address is correct. We're going to check each address carefully and test by sending to one person at a time."

### Step 6: Check Account Settings and Outgoing Server (SMTP)
1. Go to File > Account Settings > Account Settings
2. Select your email account and click "Repair" or "Change"
3. Verify the outgoing mail server (SMTP) settings:
   - Server address is correct (e.g., smtp.office365.com, smtp.gmail.com)
   - Port number is correct (usually 587 for authenticated SMTP)
   - Encryption method (TLS/SSL) matches what the email provider requires
4. Ensure the option "My outgoing server (SMTP) requires authentication" is checked
5. Ensure "Use same settings as my incoming mail server" is selected
6. Click "Test Account Settings" to verify both incoming and outgoing servers work

**What to tell the user:** "The outgoing mail server is like the post office that delivers your email. If the address or settings are wrong, your email can't leave your Outbox. We're going to verify all the server settings are correct."

### Step 7: Clear the Outbox to Resolve Corruption
1. If multiple emails are stuck in Outbox, the Outbox folder itself may be corrupted
2. Drag all emails from the Outbox to the Drafts folder (or another folder)
3. If dragging fails, use the "Move to Folder" option (right-click the email > Move > Other Folder > Drafts)
4. Ensure the Outbox is completely empty — Outlook will not send any emails if even one corrupted message is stuck
5. Once the Outbox is empty, restart Outlook
6. After restart, go to Drafts, open one email, and try sending it
7. If it sends successfully, repeat for the remaining emails
8. If the Outbox corruption persists, create a new Outlook profile

**What to tell the user:** "If multiple emails are stuck, the Outbox folder itself might have a small corruption that's blocking everything. We're going to empty it completely, which forces Outlook to process sending fresh. This is like clearing a jam in a pipe — once the blockage is removed, everything flows again."

---

## Alternative Solutions

If the above steps do not resolve the issue, also try:

- Sending the email from webmail (outlook.office.com or Gmail.com) as a workaround while troubleshooting continues
- Running Outlook in Safe Mode (outlook.exe /safe) to rule out add-in conflicts
- Temporarily disabling your antivirus email scanning feature, which can intercept outgoing mail
- Reducing the email size by removing formatting or embedded images that increase message size

---

## Prevention Tips

- Use file-sharing links (OneDrive, SharePoint, Google Drive) instead of attaching large files directly
- Double-check recipient email addresses before sending to large groups
- Keep Outlook updated through File > Office Account > Update Options > Update Now
- Avoid closing Outlook or shutting down your computer while emails are actively sending
- Review and clean out your Outbox and Drafts folders periodically

---

## Root Cause

Common causes of emails stuck in Outbox, in order of likelihood:

- Work Offline mode accidentally enabled (most common — one click to fix)
- Email attachment too large, exceeding the organization or email provider size limit
- Invalid or misspelled recipient email address causing the send to fail
- SMTP outgoing server settings incorrect or authentication failing
- Corrupted email item in Outbox blocking all other outgoing messages
- Network interruption during the initial send attempt causing the email to get stuck
- Conflict with antivirus email scanning feature
- Expired or changed password not updated in Outlook account settings

---

## Escalation Decision Matrix

| Condition | Action |
|-----------|--------|
| All 7 steps completed, issue persists | Escalate to Tier 2 |
| Multiple users in the organization cannot send emails | Escalate — likely SMTP server or Exchange issue |
| "Test Account Settings" shows SMTP failure with correct settings | Escalate — server-side issue |
| Outgoing emails blocked by spam filter or mail flow rule | Escalate — requires Exchange Admin Center |
| User's send-as or send-on-behalf permissions need modification | Escalate — requires admin rights |
| User's mailbox has exceeded sending quota or rate limit | Escalate — requires admin to adjust |
| Single user, single email issue resolved by recreating | Do not escalate — document solution |

---

## Related Articles

- [Outlook Not Receiving New Emails](./outlook-not-receiving-emails.md) — If you can send but cannot receive emails
- [Exchange Mail Flow Rules & Message Trace](../Tier-2-Technical-Support/exchange-mail-flow-rules.md) — Tier 2: If your email is being blocked by organizational rules

---

## FAQ

**Q: Why can I receive emails but not send them?**
**A:** Receiving and sending use different servers (IMAP/POP for receiving, SMTP for sending). Your incoming server might be working while your outgoing server has an authentication or configuration problem. Step 6 addresses this directly.

**Q: What is the maximum attachment size I can send?**
**A:** It varies by provider. Microsoft 365 typically allows up to 25 MB. Gmail allows up to 25 MB. Many organizations set lower limits (10 MB). Check with your IT department for your specific limit.

**Q: Will deleting a stuck email from my Outbox send it?**
**A:** No. Deleting an email from the Outbox permanently removes it without sending. Always move it to Drafts first if you want to keep the content, or use the save method described in Step 3.

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
| Open Outlook in Safe Mode | Win + R > outlook.exe /safe |

---

## Was this article helpful?

If this article helped resolve your issue, great. If something was unclear, missing, or did not work, please open a GitHub Issue describing the problem so we can improve it.

Suggest improvements at: https://github.com/EzioLockhart/Tier-1-Support-Knowledge-Base/issues

---

## References

- CompTIA A+ Troubleshooting Methodology: Identify the problem, Establish a theory, Test the theory, Establish a plan of action, Verify functionality, Document findings
- ITIL Incident Management best practices: Prioritize based on impact and urgency
- Microsoft official documentation: Fix Outlook email sending issues

---

*Tier: Tier 1 (Help Desk) | Difficulty: L1 (Basic) | Estimated Resolution Time: 10-20 minutes | Required Access Level: User | Severity: P1 (Single User Critical)*

---

For internal use. Follow your organization's escalation procedures.
