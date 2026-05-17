# Restore Deleted Files — Recycle Bin & OneDrive

- **Category:** Backup & Recovery
- **Tier:** Tier 0 (Self-Service)
- **Version:** 1.0
- **Last Updated:** May 18, 2026
- **Last Reviewed:** May 18, 2026
- **Applies To:** Windows 10, Windows 11, OneDrive, SharePoint
- **Difficulty:** L0 (Self-Service)
- **Estimated Resolution Time:** 5-10 minutes
- **Required Access Level:** User
- **Severity:** P1 (Single User, Critical — Data Loss Risk)
- **Keywords:** deleted, files, restore, recover, Recycle Bin, OneDrive, undo, previous versions
- **Prerequisite Knowledge:** Basic computer usage, ability to open File Explorer and web browser

---

## Before You Call the Helpdesk

Deleted a file by accident? Do not panic. Files are rarely gone forever. Try these methods in order — the sooner you act, the better your chances of recovery.

---

## Quick Recovery Menu

| Method | Best For | Jump To |
|--------|----------|---------|
| Recycle Bin | Files deleted on your computer | Fix 1 |
| Undo Delete | Immediately after deleting | Fix 2 |
| OneDrive Recycle Bin | Files from OneDrive or synced folders | Fix 3 |
| Previous Versions | Files you saved over or changed | Fix 4 |
| File History | Files backed up automatically | Fix 5 |

---

## Fix 1: Restore from the Recycle Bin

The Recycle Bin holds deleted files until it is emptied. Always check here first.

**Step 1: Open the Recycle Bin**
1. Double-click the **Recycle Bin** icon on your desktop
   - If you do not see it, right-click on the desktop > **"Personalize"** > **"Themes"** > **"Desktop icon settings"** > check **"Recycle Bin"** > **"OK"**
2. The Recycle Bin opens like a regular folder

**Step 2: Find your file**
1. Look through the files and folders
2. Use the **search bar** in the top-right corner to search by file name
3. Click the **"Date deleted"** column header to sort by when items were deleted
4. The most recently deleted items appear at the top

**Step 3: Restore the file**
1. Click on the file you want to recover
2. Right-click the file > **"Restore"**
3. The file returns to its original location
4. Open File Explorer and navigate to where the file was originally saved — it should be there

**If the Recycle Bin is empty:** The bin may have been emptied. Proceed to Fix 3 (OneDrive) or Fix 4 (Previous Versions).

**What to tell yourself:** "The Recycle Bin is like a safety net. When I delete a file, it goes there first. As long as I have not emptied the bin, my file is probably still there."

---

## Fix 2: Undo Delete (Immediately After Deleting)

If you just deleted the file moments ago, you can undo it instantly.

**Method 1: Undo keyboard shortcut**
1. Immediately after deleting, press **Ctrl + Z** on your keyboard
2. The file reappears in its original location
3. This works for most actions, not just deleting

**Method 2: Right-click undo**
1. Go to the folder where the file was located
2. Right-click on an empty space in the folder
3. Select **"Undo Delete"**
4. The file reappears

**Important:** This only works if you have not done anything else since deleting. If you have moved, renamed, or created other files, Undo may not work.

---

## Fix 3: Restore from OneDrive Recycle Bin

If your file was in OneDrive, Desktop, Documents, or Pictures folders, it has its own separate recycle bin.

**Step 1: Go to OneDrive on the web**
1. Open a web browser
2. Go to **onedrive.com** or **office.com**
3. Sign in with your work email and password

**Step 2: Find the OneDrive Recycle Bin**
1. On the left sidebar, click **"Recycle bin"**
2. You will see all files deleted from OneDrive in the last 30 days (or longer if your organization extended it)

**Step 3: Restore your file**
1. Find your file in the list
2. Click the checkbox next to the file
3. Click the **"Restore"** button at the top
4. The file returns to its original OneDrive folder

**Why OneDrive has its own Recycle Bin:** Files synced with OneDrive are stored in the cloud. When you delete a synced file, it goes to both your computer's Recycle Bin AND the OneDrive Recycle Bin. Even if your computer's bin is emptied, the OneDrive copy may still exist.

**What to tell yourself:** "OneDrive keeps deleted files for 30 days. Even if I emptied my computer's Recycle Bin, the file might still be in the OneDrive Recycle Bin online."

---

## Fix 4: Restore Previous Versions of a File

If you saved over a file or made changes you want to undo, Windows may have saved a previous copy.

**Step 1: Find the file or folder**
1. Open File Explorer
2. Navigate to the folder where your file was (or the file itself if you overwrote it)

**Step 2: Check for previous versions**
1. Right-click the **folder** (not the file) > **"Properties"**
2. Go to the **"Previous Versions"** tab
3. If available, you will see a list of folder snapshots with dates and times
4. Select a version from **before** the file was deleted or changed

**Step 3: Restore or copy**
- Click **"Open"** to view the folder contents without restoring — then copy the specific file you need
- Click **"Restore"** to restore the entire folder to that point in time (this replaces the current version)

**If no previous versions appear:** This feature may not be turned on. Skip to Fix 5.

**What to tell yourself:** "Windows sometimes takes automatic snapshots of my files. If I saved over an important document, I might be able to get the old version back."

---

## Fix 5: Check File History Backup

File History is a Windows backup feature that saves copies of your files to an external drive or network location.

**Step 1: Check if File History is running**
1. Click Start, type **"File History"**, and open it
2. If File History is on, you will see a "Restore personal files" option

**Step 2: Restore files**
1. Click **"Restore personal files"**
2. Browse through the timeline using the arrows at the bottom
3. Find the version of your file or folder from before it was deleted
4. Select the file > click the green **"Restore"** button
5. The file returns to its original location

**If File History is off:** This feature requires setup before the file was lost. If it was never turned on, this option is not available.

---

## What to Do If Nothing Works

If you tried all methods and cannot recover your file:

1. **Check your email:** Search your sent items — you may have emailed the file to yourself or a colleague
2. **Check recent files:** Open the application you used to create the file (Word, Excel, etc.) > File > Open > Recent
3. **Check temporary files:** Open File Explorer and type **%temp%** in the address bar — some applications save temporary copies
4. **Contact IT support:** They may have server-side backups for network drives

---

## Prevention Tips

- Save important files to OneDrive, Desktop, or Documents folders — these are protected by OneDrive's Recycle Bin
- Do not empty your Recycle Bin immediately — give yourself time to realize if you deleted something important
- Enable File History: Settings > Update & Security > Backup > Add a drive
- Before making major changes to a document, save a copy with a different name (e.g., "Report_v2.docx")
- Use Ctrl + Z immediately after any accidental deletion

---

## FAQ

**Q: How long do deleted files stay in the Recycle Bin?**
**A:** Files stay in the computer's Recycle Bin until you manually empty it or the bin reaches its size limit. OneDrive Recycle Bin keeps files for 30 days by default (your organization may have extended this).

**Q: Can I recover a file I deleted months ago?**
**A:** Probably not from the Recycle Bin. If the file was in OneDrive and it has been less than 30 days, try the OneDrive Recycle Bin. If File History was enabled with a backup drive, you may be able to recover older versions.

**Q: What is the difference between Recycle Bin and Previous Versions?**
**A:** Recycle Bin stores files you intentionally deleted. Previous Versions are automatic snapshots Windows takes of your files at different points in time — you can recover older versions even if the file was never deleted, just changed.

---

## Recovery Methods Quick Reference

| Method | What It Recovers | How Long Files Stay |
|--------|------------------|:-------------------:|
| Ctrl + Z | Last action undone | Immediate only |
| Recycle Bin | Deleted files | Until emptied |
| OneDrive Recycle Bin | Deleted synced files | 30 days (or more) |
| Previous Versions | Older versions of files | Days to weeks |
| File History | Backed up files | Months to years |

---

## Was this article helpful?

If this article helped resolve your issue, great. If something was unclear, missing, or did not work, please open a GitHub Issue describing the problem so we can improve it.

Suggest improvements at: https://github.com/EzioLockhart/Complete-IT-Support-Knowledge-Base-Tier-0-to-Tier-3/issues

---

## References

- Microsoft official documentation: Restore deleted files in Windows
- Microsoft OneDrive documentation: Restore deleted files or folders
- ITIL Incident Management best practices: Self-service reduces helpdesk ticket volume

---

*Tier: Tier 0 (Self-Service) | Difficulty: L0 (Self-Service) | Estimated Resolution Time: 5-10 minutes | Required Access Level: User | Severity: P1 (Single User Critical)*

---

For internal use. Share this guide with users before escalating to Tier 1.
