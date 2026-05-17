# File Recovery from Previous Versions & Shadow Copy

- **Category:** Backup & Recovery
- **Tier:** Tier 1 (Help Desk)
- **Version:** 1.0
- **Last Updated:** May 2, 2026
- **Last Reviewed:** May 2, 2026
- **Applies To:** Windows 10 (22H2), Windows 11 (23H2), NTFS Drives with Shadow Copy Enabled
- **Difficulty:** L1 (Basic)
- **Estimated Resolution Time:** 10-15 minutes
- **Required Access Level:** User
- **Severity:** P1 (Single User, Critical — Data Loss Risk)
- **Keywords:** file recovery, restore, previous versions, shadow copy, deleted file, overwritten, backup, VSS
- **Prerequisite Knowledge:** Basic Windows navigation, ability to right-click files and open Properties

---

## Symptoms

- File was accidentally deleted and needs to be recovered
- File was overwritten or changed and the previous version is needed
- Folder contents disappeared or were moved without user action
- "There are no previous versions available" message appears when checking for recoverable files
- File was saved over and the original version is needed urgently
- Recycle Bin has been emptied and the deleted file is no longer there
- Error message: "The shadow copy provider had an error" when trying to restore

---

## Common Error Codes

| Code | Meaning |
|------|---------|
| 0x80042306 | Shadow copy provider is in use — retry after a few minutes |
| 0x8004230F | No shadow copies exist for this volume — protection not enabled |
| Event ID 8193 | Volume Shadow Copy Service error — VSS writer failed |
| 0x80070002 | File not found — the specific previous version may not exist |

---

## Symptom-to-Step Mapping

| If You See This | Skip To |
|-----------------|---------|
| File was just deleted from Recycle Bin | Step 1 |
| File was overwritten and old version needed | Step 2 |
| "No previous versions available" | Step 3 |
| Specific folder contents disappeared | Step 4 |
| Need to recover multiple files from a point in time | Step 5 |

---

## Triage Questions

Before starting troubleshooting, ask the user:

1. "When did you last see or have access to the file you need to recover?"
2. "Was the file deleted, overwritten, or did it just disappear?"
3. "Have you checked the Recycle Bin already?"
4. "Is the file on a network shared drive or your local computer?"

---

## Quick Checks (30 seconds)

1. Check the Recycle Bin first — double-click the Recycle Bin icon on the desktop and search for the file
2. Check File Explorer recent files: open File Explorer > click "Home" > look under "Recent"
3. Check if the file was saved to OneDrive or SharePoint — log into webmail and check those locations
4. Use Windows Search (Win + S) to search for the file name — it may have been moved to a different folder
5. Check if your organization has automatic backups configured — ask your IT department
6. If you need basic guidance on restoring deleted files, see: [Restore Deleted Files — Recycle Bin & OneDrive](../Tier-0-Self-Service/restore-deleted-files.md)

---

## Step-by-Step Resolution

### Step 1: Check and Restore from Recycle Bin
1. The Recycle Bin holds deleted files until it is manually emptied or reaches its size limit
2. Double-click the Recycle Bin icon on your desktop
3. If you do not see the Recycle Bin icon:
   - Right-click on the desktop > Personalize > Themes > Desktop icon settings
   - Check "Recycle Bin" and click OK
4. Search for your file by name in the Recycle Bin search bar
5. Sort by "Date deleted" to find recently removed files
6. Right-click the file > "Restore" — the file returns to its original location
7. If the Recycle Bin has been emptied since the file was deleted, proceed to Step 2

**What to tell the user:** "The Recycle Bin is your first and easiest option. When you delete a file, it goes to the Recycle Bin first — it's not permanently gone. Let's check if your file is still sitting there. Even if you emptied the bin, don't worry — Windows has other recovery methods."

### Step 2: Use the "Restore Previous Versions" Feature
1. Previous Versions uses Windows Shadow Copy to save snapshots of files and folders
2. Navigate to the folder where the file was originally located
3. Right-click the folder (not the file) > "Properties"
4. Go to the "Previous Versions" tab
5. Windows will list available snapshots with dates and times
6. Select a version from before the file was deleted or changed
7. Choose an action:
   - "Open" — view the folder contents without restoring, then copy the specific file you need
   - "Restore" — restore the entire folder to that point in time (this overwrites the current folder contents)
8. If the file you need is inside, click "Open", locate the file, and drag it to your desktop or desired location
9. If you need to restore an individual file instead of a folder:
   - Navigate to the folder > right-click a blank area > "Properties" > "Previous Versions"
   - Or right-click the specific file > "Properties" > "Previous Versions" (if available for individual files)

**What to tell the user:** "Windows automatically takes snapshots of your files at different points in time — like having a time machine for your documents. Even if a file was deleted or changed yesterday, Windows might have saved a copy from before that happened. Let's check if any previous versions are available."

### Step 3: Check If Shadow Copy (System Protection) Is Enabled
1. If "No previous versions available" appears, System Protection may not be turned on
2. Check if System Protection is enabled:
   - Press Win + R, type sysdm.cpl, press Enter
   - Go to the "System Protection" tab
   - Under "Protection Settings", find your C: drive
   - The "Protection" column should show "On" — if it shows "Off", shadow copies are not being created
3. If System Protection is Off for the drive where your file was stored:
   - Unfortunately, Previous Versions cannot recover files from before protection was enabled
   - You can turn it on now to protect against future data loss:
     - Select the drive > "Configure" > "Turn on system protection"
     - Set "Max Usage" to at least 5-10% of the drive
     - Click "Apply" then "OK"
4. If System Protection is On but no versions appear:
   - Shadow copies may have been deleted when the disk ran low on space
   - Try restarting the computer and checking again — sometimes the list needs a refresh
   - Proceed to Step 4 for alternative recovery options

**What to tell the user:** "Windows has a feature called System Protection that automatically saves file snapshots. If it was turned off on your computer before the file was lost, the snapshot feature wasn't running and can't help us. But we can turn it on now to prevent this from happening again. Let's check its status and try other recovery methods."

### Step 4: Recover from OneDrive or SharePoint (If Applicable)
1. If the missing file was in a OneDrive or SharePoint folder, it has its own version history
2. For OneDrive:
   - Go to onedrive.com or office.com and sign in
   - Navigate to the folder where your file was located
   - Look in the "Recycle Bin" on the left sidebar — OneDrive keeps deleted files for 30 days
   - If the file was overwritten, right-click the file > "Version history"
   - Find the version you need and click "Restore" or download it
3. For SharePoint:
   - Go to your SharePoint site document library
   - Find the file > click the three dots (...) > "Version history"
   - Select the version you need and restore it
4. If the file was deleted from a synced folder:
   - Check the OneDrive recycle bin online — it often has files that the local Recycle Bin does not
   - Deleted files from synced folders are available online for 30 days (or longer if your organization extended it)

**What to tell the user:** "If your file was stored in OneDrive or SharePoint — even if it was synced to your computer — the cloud version keeps its own separate backup. OneDrive keeps deleted files for 30 days and stores every saved version of a document. This is actually more powerful than Windows' built-in recovery. Let's check online."

### Step 5: Use Command Prompt to List Available Shadow Copies
1. Sometimes the graphical interface does not list all available shadow copies
2. Open Command Prompt as Administrator: Win + X > Terminal (Admin)
3. List all shadow copies on the system:
   vssadmin list shadows
4. This shows every shadow copy with creation time and the volume it belongs to
5. Identify the shadow copy from the time period you need
6. To access a specific shadow copy, create a symbolic link:
   mklink /d C:\ShadowCopy \\?\GLOBALROOT\Device\HarddiskVolumeShadowCopy1\
   - Replace "HarddiskVolumeShadowCopy1" with the exact shadow copy ID from the list
   - This creates a folder at C:\ShadowCopy that you can browse like a normal folder
7. Navigate to C:\ShadowCopy in File Explorer and find your file
8. Copy the file to your desktop or desired location
9. After recovering, delete the symbolic link: rmdir C:\ShadowCopy

**What to tell the user:** "Even when the graphical interface shows no previous versions, the command line can sometimes access shadow copies that are hidden from view. This is a more technical method, but it can recover files that appear to be completely gone."

### Step 6: Check File History Backup (If Configured)
1. File History is a separate Windows backup feature that continuously backs up files to an external drive or network location
2. Check if File History is enabled:
   - Settings > Update & Security > Backup (Windows 10)
   - Settings > Accounts > Windows backup (Windows 11)
3. If File History was set up before the file was lost:
   - Open Control Panel > File History
   - Click "Restore personal files"
   - Browse through the backup timeline to find your file
   - Select the file and click the green "Restore" button
4. File History keeps multiple versions of files over time
5. If File History was never configured, this option is not available

**What to tell the user:** "File History is like an automatic time machine that saves copies of your files to an external drive. If you or your IT department set this up before the file was lost, we have another way to recover your file. Let's check if it's configured on your computer."

---

## Alternative Solutions

If the above steps do not resolve the issue, also try:

- Using third-party file recovery software like Recuva (free) to scan the drive for deleted files
- Checking if your IT department performs regular backups of network drives or local machines
- Searching your email attachments — you may have emailed the file to yourself or a colleague
- Checking temporary files: open File Explorer and type %temp% in the address bar — some applications save temporary copies

---

## Prevention Tips

- Enable System Protection on all drives: Control Panel > System > System Protection > Configure > Turn on
- Save important files to OneDrive or SharePoint folders — they have built-in version history and deleted file retention
- Set up File History to an external drive or network location for automatic backups
- Create manual copies of critical files before making major changes — takes seconds, saves hours
- Do not store important files only on your desktop or Downloads folder — these locations are most likely to be accidentally deleted

---

## Root Cause

Common causes of file loss or need for recovery, in order of likelihood:

- Accidental deletion and Recycle Bin already emptied (most common)
- File overwritten with new content and old version needed
- Files or folders moved to an unknown location by user or application
- System Protection (Shadow Copy) never enabled on the drive
- Disk space running low causing Windows to delete older shadow copies
- Application error or crash causing unsaved work to be lost
- Malware or ransomware encrypting or deleting files

---

## Escalation Decision Matrix

| Condition | Action |
|-----------|--------|
| All 6 steps completed, file not recovered | Escalate to Tier 2 |
| File is on a network shared drive with server-side backups | Escalate — server admin can restore from backup |
| Shadow copies exist but cannot be accessed (permission errors) | Escalate — requires administrator access |
| File is business-critical and all recovery methods have failed | Escalate urgently — possible professional data recovery needed |
| System Protection is disabled by Group Policy | Escalate — requires policy change |
| Drive corruption preventing shadow copy access | Escalate — possible disk failure |
| File successfully recovered from Previous Versions or OneDrive | Do not escalate — document solution |

---

## Related Articles

- [Restore Deleted Files — Recycle Bin & OneDrive](../Tier-0-Self-Service/restore-deleted-files.md) — Tier 0: Self-service file recovery
- [Windows Backup Failure & VSS Writer Diagnostics](../Tier-2-Technical-Support/windows-backup-vss-writer.md) — Tier 2: Advanced backup diagnostics
- [Disaster Recovery — Bare-Metal Restore & System State](../Tier-3-Expert-Engineering/disaster-recovery-bare-metal.md) — Tier 3: Expert recovery procedures

> **Note:** The following related articles are planned for future creation within their respective tier folders:
> - [Restore Deleted Files — Recycle Bin & OneDrive](../Tier-0-Self-Service/restore-deleted-files.md)
> - [Windows Backup Failure & VSS Writer Diagnostics](../Tier-2-Technical-Support/windows-backup-vss-writer.md)
> - [Disaster Recovery — Bare-Metal Restore & System State](../Tier-3-Expert-Engineering/disaster-recovery-bare-metal.md)

---

## FAQ

**Q: How far back can Previous Versions recover files?**
**A:** It depends on how much disk space is allocated to System Protection. Typically, Windows keeps shadow copies for a few days to a few weeks. If the allocated space fills up, older snapshots are deleted. Increasing the Max Usage in System Protection settings keeps versions longer.

**Q: What is the difference between Previous Versions and File History?**
**A:** Previous Versions (Shadow Copy) takes snapshots of entire drives at points in time — it's automatic and built into Windows. File History is a separate backup feature that continuously backs up files to an external drive — it must be manually configured. Both can recover files, but File History keeps more versions over a longer period.

**Q: Can I recover a file that was never saved?**
**A:** In most cases, no. If you created a new document and closed it without saving, the temporary file is usually deleted. Some applications (Word, Excel) have auto-recovery features that may have saved a temporary copy. Check File > Info > Manage Document > Recover Unsaved Documents in those applications.

---

## Recovery Methods Quick Reference

| Method | What It Recovers | How Far Back |
|--------|------------------|:------------:|
| Recycle Bin | Recently deleted files | Until bin is emptied |
| Previous Versions | Deleted or overwritten files | Days to weeks |
| OneDrive Recycle Bin | Deleted synced files | 30 days (or more) |
| OneDrive Version History | Overwritten files | Every saved version |
| File History | Backed up files | Months to years |
| Command Line (vssadmin) | Shadow copies | Same as Previous Versions |

---

## Commands Quick Reference

| Command | Purpose |
|---------|---------|
| sysdm.cpl | Open System Properties (System Protection tab) |
| vssadmin list shadows | List all available shadow copies |
| mklink /d C:\ShadowCopy \\?\GLOBALROOT\Device\HarddiskVolumeShadowCopy1\ | Create accessible link to a shadow copy |
| rmdir C:\ShadowCopy | Remove shadow copy link after recovery |

---

## Was this article helpful?

If this article helped resolve your issue, great. If something was unclear, missing, or did not work, please open a GitHub Issue describing the problem so we can improve it.

Suggest improvements at: https://github.com/EzioLockhart/Complete-IT-Support-Knowledge-Base-Tier-0-to-Tier-3/issues

---

## References

- CompTIA A+ Troubleshooting Methodology: Identify the problem, Establish a theory, Test the theory, Establish a plan of action, Verify functionality, Document findings
- ITIL Incident Management best practices: Prioritize based on impact and urgency; data loss is a critical incident
- Microsoft official documentation: Restore files from Previous Versions and Shadow Copy

---

*Tier: Tier 1 (Help Desk) | Difficulty: L1 (Basic) | Estimated Resolution Time: 10-15 minutes | Required Access Level: User | Severity: P1 (Single User Critical)*

---

For internal use. Follow your organization's data recovery and backup policies.
