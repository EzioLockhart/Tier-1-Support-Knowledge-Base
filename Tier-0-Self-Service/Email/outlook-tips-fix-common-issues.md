# Outlook Tips — Fix Common Email Issues Yourself

- **Category:** Email
- **Tier:** Tier 0 (Self-Service)
- **Version:** 1.0
- **Last Updated:** May 18, 2026
- **Last Reviewed:** May 18, 2026
- **Applies To:** Microsoft Outlook 2016, 2019, 2021, Microsoft 365 (Windows & Mac)
- **Difficulty:** L0 (Self-Service)
- **Estimated Resolution Time:** 5-10 minutes
- **Required Access Level:** User
- **Severity:** P2 (Single User, Degraded — Email Issues)
- **Keywords:** Outlook, email, fix, tips, self-service, send, receive, offline, password, sync
- **Prerequisite Knowledge:** Basic Outlook usage, ability to open and navigate email

---

## Before You Call the Helpdesk

Try these quick fixes first. Most Outlook issues can be solved in under 5 minutes without calling IT support.

---

## Quick Fix Menu

| Problem | Jump To |
|---------|---------|
| Not receiving new emails | Fix 1 |
| Cannot send emails | Fix 2 |
| Outlook says "Working Offline" | Fix 3 |
| Outlook keeps asking for password | Fix 4 |
| Emails going to Junk folder | Fix 5 |
| Outlook running very slow | Fix 6 |

---

## Fix 1: Not Receiving New Emails

1. Check if you are in Work Offline mode:
   - Look at the bottom-left corner of Outlook
   - If it says "Working Offline" or "Disconnected", go to Fix 3
2. Check your Focused Inbox:
   - Look for "Focused" and "Other" tabs at the top of your inbox
   - Click the "Other" tab — new emails from unknown senders may be there
3. Check your Junk Email folder:
   - Look in the left folder list for "Junk Email"
   - If you find legitimate emails there, right-click them and select "Not Junk"
4. Try a manual Send/Receive:
   - Click the "Send/Receive" tab at the top
   - Click "Send/Receive All Folders"
   - Or press F9 on your keyboard

**If still not working:** Ask a colleague to send you a test email. If it arrives, the issue is resolved. If not, check your internet connection and try again.

---

## Fix 2: Cannot Send Emails

1. Check if your email is stuck in the Outbox:
   - Look in the left folder list for "Outbox"
   - If there are emails stuck there, open each one and click "Send" again
2. Check attachment size:
   - Most organizations limit attachments to 10-25 MB
   - If your attachment is too large, use OneDrive or SharePoint link instead
3. Check recipient email addresses:
   - Look for typos in the email addresses (e.g., @gnail.com instead of @gmail.com)
   - Remove any spaces or extra characters
4. Make sure you are not in Work Offline mode (see Fix 3)

**If still not working:** Try sending a test email to yourself. If you receive it, your outgoing mail is working. If it also gets stuck, try restarting Outlook.

---

## Fix 3: Outlook Says "Working Offline"

1. Click the "Send/Receive" tab at the top of Outlook
2. Look for the "Work Offline" button
3. If it is highlighted or looks pressed, click it once to turn it off
4. Wait 30 seconds for Outlook to reconnect
5. The status bar at the bottom should now say "Connected"

**Why this happens:** This button can be clicked accidentally, or Outlook may switch to offline mode after a network interruption. It is the most common cause of email problems.

---

## Fix 4: Outlook Keeps Asking for Password

1. When the password prompt appears, carefully type your current password
2. Check the box that says "Remember my credentials" before clicking OK
3. If the prompt keeps returning:
   - Close Outlook completely
   - Open the Start menu and type "Credential Manager"
   - Click "Windows Credentials"
   - Look for any entries with "Outlook" or your email address
   - Click the arrow next to each one and select "Remove"
   - Restart Outlook and enter your password when prompted

**Why this happens:** Windows saves old passwords, and after you change your password, the saved copy keeps trying the old one. Clearing saved credentials forces Outlook to use your new password.

---

## Fix 5: Emails Going to Junk Folder

1. Click the "Junk Email" folder in the left folder list
2. If you find a legitimate email there:
   - Right-click the email
   - Select "Junk" → "Not Junk"
   - Check the box "Always trust email from this sender" if prompted
3. To prevent future emails from the same sender going to Junk:
   - Right-click any email from that sender
   - Select "Junk" → "Never Block Sender"

**Why this happens:** Outlook's spam filter sometimes mistakenly identifies legitimate emails as junk. Marking them as "Not Junk" trains the filter to be more accurate.

---

## Fix 6: Outlook Running Very Slow

1. Close Outlook completely
2. Check for updates:
   - Reopen Outlook
   - Go to File → Office Account → Update Options → Update Now
3. Clear your Deleted Items folder:
   - Right-click "Deleted Items" in the left folder list
   - Select "Empty Folder"
4. Reduce mailbox size:
   - Delete old emails with large attachments
   - Sort your inbox by size to find the largest emails
5. Disable add-ins:
   - Go to File → Options → Add-ins
   - At the bottom, select "COM Add-ins" and click "Go"
   - Uncheck any add-ins you do not need
   - Click OK

**Why this happens:** A large mailbox, outdated software, or too many add-ins can slow Outlook down significantly.

---

## When to Call the Helpdesk

Contact IT support if:

- You tried all the relevant fixes above and the issue persists
- You cannot access your email at all — even through webmail
- You suspect your account has been compromised (strange emails being sent from your account)
- You need your password reset
- Multiple colleagues report the same issue (may be a server problem)

---

## Prevention Tips

- Restart Outlook at least once a week — do not leave it running for weeks
- Empty your Deleted Items folder monthly
- Keep Outlook updated through File → Office Account → Update Options
- Do not click "Work Offline" unless you intentionally need offline access
- Before attaching large files, use OneDrive or SharePoint links instead

---

## Was this article helpful?

If this article helped resolve your issue, great. If something was unclear, missing, or did not work, please open a GitHub Issue describing the problem so we can improve it.

Suggest improvements at: https://github.com/EzioLockhart/Complete-IT-Support-Knowledge-Base-Tier-0-to-Tier-3/issues

---

## References

- Microsoft official documentation: Fix Outlook issues
- ITIL Incident Management best practices: Self-service reduces helpdesk ticket volume

---

*Tier: Tier 0 (Self-Service) | Difficulty: L0 (Self-Service) | Estimated Resolution Time: 5-10 minutes | Required Access Level: User | Severity: P2 (Single User Degraded)*

---

For internal use. Share this guide with users before escalating to Tier 1.
