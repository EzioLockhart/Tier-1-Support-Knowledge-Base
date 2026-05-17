# Access Shared Files & Folders — Quick Guide

- **Category:** File Access & Sharing
- **Tier:** Tier 0 (Self-Service)
- **Version:** 1.0
- **Last Updated:** May 18, 2026
- **Last Reviewed:** May 18, 2026
- **Applies To:** Windows 10, Windows 11, OneDrive, SharePoint, Network Shared Drives
- **Difficulty:** L0 (Self-Service)
- **Estimated Resolution Time:** 5-10 minutes
- **Required Access Level:** User
- **Severity:** P2 (Single User, Degraded — Cannot Access Files)
- **Keywords:** shared drive, OneDrive, SharePoint, access, files, folders, network drive, permission
- **Prerequisite Knowledge:** Basic computer usage, ability to open File Explorer and web browser

---

## Before You Start

**Which type of shared files are you trying to access?**

| If You Need To | Go To |
|----------------|-------|
| Access a network shared drive (S: drive, Z: drive, etc.) | Fix 1 |
| Open a OneDrive folder someone shared with you | Fix 2 |
| Access a SharePoint team site | Fix 3 |
| Request access to something you cannot open | Fix 4 |
| Sync shared folders to your computer | Fix 5 |

---

## Fix 1: Access a Network Shared Drive

Network shared drives appear as drive letters in File Explorer (like S: or Z:).

1. Open **File Explorer** (the folder icon on your taskbar)
2. Look at the left sidebar under "This PC"
3. You should see your shared drives listed with drive letters
4. If a drive has a **red X**, it is disconnected:
   - Double-click the drive to try to reconnect
   - If prompted, enter your username and password
5. If the drive is missing entirely:
   - You may need to map it — contact IT support for the exact path

**Common drive letters and their typical uses:**
- S: drive — Shared department folder
- Z: drive — Personal network folder
- Other letters vary by organization

**What to tell yourself:** "If I see a red X on the drive, I just need to double-click it. If it asks for my password, I use my work login."

---

## Fix 2: Open a OneDrive Folder Someone Shared With You

When someone shares a OneDrive folder with you, you usually receive an email with a link.

**Method A: Open in your web browser**
1. Open the email that says someone shared a folder with you
2. Click the **"Open"** or **"View folder"** button in the email
3. Your web browser will open and show the shared folder
4. You can view, download, and upload files from here

**Method B: Add to your own OneDrive**
1. Click the shared link to open the folder in your browser
2. Look for a button that says **"Add shortcut to My files"** or **"Add to my OneDrive"**
3. Click it — the folder will appear in your own OneDrive
4. You can now access it from File Explorer under your OneDrive folder

**If the link says "Access Denied":**
- The sharing link may have expired
- Your permission may have been removed
- Contact the person who shared it and ask them to reshare

---

## Fix 3: Access a SharePoint Team Site

SharePoint sites are websites where teams store shared documents.

1. Open your web browser
2. Go to your organization's SharePoint homepage (usually office.com or your company's intranet)
3. Sign in with your work email and password
4. Look for the SharePoint site name — you can search at the top
5. Click on the site to open it
6. On the left side, click **"Documents"** to see the shared files
7. You can view and edit files directly in the browser

**To sync SharePoint files to your computer:**
1. Open the SharePoint document library in your browser
2. Look for a **"Sync"** button in the toolbar
3. Click **"Sync"**
4. Follow the prompts — the files will appear in File Explorer under your organization name

---

## Fix 4: Request Access to Files You Cannot Open

If you click a file or folder and see "Access Denied" or "You need permission":

1. Look for a **"Request Access"** button or link on the error page
2. Click it
3. You may be asked to write a short message explaining why you need access
4. The file owner will receive your request and can grant you access
5. You will receive an email when access is granted

**If there is no "Request Access" button:**
- Ask your manager or the person who shared the file to grant you access
- Contact IT support if you are unsure who the owner is

---

## Fix 5: Sync Shared Folders to Your Computer

Syncing means the files appear in File Explorer like regular folders, even when you are offline.

**For OneDrive shared folders:**
1. Open the shared folder in your browser
2. Click **"Add shortcut to My files"**
3. The folder appears in your OneDrive
4. If OneDrive sync is running on your computer, the folder will sync automatically

**For SharePoint libraries:**
1. Open the SharePoint document library in your browser
2. Click the **"Sync"** button
3. Click **"Sync now"** when prompted
4. The files will appear in File Explorer under your organization name

**Check if OneDrive sync is running:**
1. Look for a blue cloud icon in the system tray (bottom-right corner, near the clock)
2. If you see it, OneDrive is running
3. If you do not see it, open Start menu, type "OneDrive", and launch it

---

## When to Call the Helpdesk

Contact IT support if:

- You cannot see a shared drive that you used to have access to
- "Access Denied" persists after requesting access
- You cannot find a SharePoint site that your team uses
- The Sync button is missing or not working
- You need access to a new shared drive or folder for your role

---

## FAQ

**Q: What is the difference between OneDrive and SharePoint?**
**A:** OneDrive is your personal work storage (like your My Documents in the cloud). SharePoint is for team files — shared document libraries that multiple people access. They look similar but serve different purposes.

**Q: Can I access shared files from home without VPN?**
**A:** Yes, if they are on OneDrive or SharePoint. These are cloud-based and accessible from any web browser. Network shared drives (S: drive, Z: drive) usually require VPN to access from home.

**Q: Why do I see "Access Denied" on a file my colleague can open?**
**A:** Permissions are set per person or group. Your colleague may be in a security group that has access while you are not. Contact the file owner or IT to be added.

---

## Was this article helpful?

If this article helped resolve your issue, great. If something was unclear, missing, or did not work, please open a GitHub Issue describing the problem so we can improve it.

Suggest improvements at: https://github.com/EzioLockhart/Complete-IT-Support-Knowledge-Base-Tier-0-to-Tier-3/issues

---

## References

- Microsoft official documentation: OneDrive and SharePoint sharing
- ITIL Incident Management best practices: Self-service reduces helpdesk ticket volume

---

*Tier: Tier 0 (Self-Service) | Difficulty: L0 (Self-Service) | Estimated Resolution Time: 5-10 minutes | Required Access Level: User | Severity: P2 (Single User Degraded)*

---

For internal use. Share this guide with users before escalating to Tier 1.
