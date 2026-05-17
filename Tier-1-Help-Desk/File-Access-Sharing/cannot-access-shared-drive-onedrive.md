# Cannot Access Shared Drive or OneDrive Folder

- **Category:** File Access & Sharing
- **Tier:** Tier 1 (Help Desk)
- **Version:** 1.0
- **Last Updated:** May 2, 2026
- **Last Reviewed:** May 2, 2026
- **Applies To:** Windows 10 (22H2), Windows 11 (23H2), OneDrive, SharePoint, Network Shared Drives
- **Difficulty:** L1 (Basic)
- **Estimated Resolution Time:** 10-20 minutes
- **Required Access Level:** User
- **Severity:** P1 (Single User, Critical — Cannot Access Files)
- **Keywords:** shared drive, OneDrive, access denied, permissions, network drive, SharePoint, sync, file sharing
- **Prerequisite Knowledge:** Basic Windows navigation, ability to open File Explorer and check network connections

---

## Symptoms

- Error message: "Access Denied" or "You do not have permission to access this folder"
- Mapped network drive shows red X or "Disconnected" in File Explorer
- OneDrive folder shows "Cannot connect" or files stuck on "Sync pending"
- Previously working shared drive suddenly inaccessible
- "The network path was not found" error when clicking a shared drive
- Files appear in OneDrive online but not in the local OneDrive folder
- "This folder is empty" message despite knowing files exist there

---

## Common Error Codes

| Code | Meaning |
|------|---------|
| 0x80070005 | Access denied — user does not have required permissions |
| 0x80070035 | Network path not found — shared drive or server unreachable |
| 0x80070043 | Network name cannot be found — incorrect path or DNS issue |
| 0x8007016A | Cloud file provider not running — OneDrive sync issue |

---

## Symptom-to-Step Mapping

| If You See This | Skip To |
|-----------------|---------|
| "Access Denied" message | Step 4 |
| Mapped drive shows red X | Step 1 |
| OneDrive files not syncing | Step 2 |
| "Network path not found" error | Step 3 |
| Shared drive works on other computers | Step 5 |

---

## Triage Questions

Before starting troubleshooting, ask the user:

1. "Is this a network shared drive, a OneDrive folder, or a SharePoint site you're trying to access?"
2. "Can other people in your team access this same drive or folder?"
3. "Did this drive ever work for you before, or is this the first time you're trying to access it?"
4. "Have you recently changed your password or been moved to a different department?"

---

## Quick Checks (30 seconds)

1. Check if you have an active internet or network connection — open a browser and load any website
2. Try accessing the shared drive by its full path (e.g., \\server\share) instead of clicking the mapped drive
3. Check OneDrive status in the system tray (cloud icon) — does it show "Up to date" or an error?
4. Restart File Explorer: Ctrl + Shift + Esc > find Windows Explorer > right-click > Restart
5. Verify the shared drive letter is still assigned: open File Explorer > This PC > look for the drive
6. If you need a basic guide to accessing shared files, see: [Access Shared Files & Folders — Quick Guide](../Tier-0-Self-Service/access-shared-files.md)

---

## Step-by-Step Resolution

### Step 1: Reconnect to the Network Drive or OneDrive
1. For mapped network drives:
   - Open File Explorer > This PC
   - Look for the mapped drive with a red X
   - Double-click the drive to force a reconnection attempt
   - If prompted, enter your username in the format DOMAIN\username and your current password
   - Check "Remember my credentials" to save for future use
2. For OneDrive:
   - Click the OneDrive cloud icon in the system tray (bottom-right corner)
   - If OneDrive is paused, click the icon and select "Resume syncing"
   - If OneDrive is not running at all, open Start menu, type "OneDrive", and launch it
   - Sign in with your account if prompted
3. For SharePoint:
   - Open your browser and navigate to your organization's SharePoint site
   - Click "Sync" in the document library toolbar
   - This re-establishes the sync connection with your local OneDrive

**What to tell the user:** "Network drives and OneDrive can lose their connection after a password change or network interruption. Let's try reconnecting manually. For mapped drives, just double-clicking them often forces a fresh connection. For OneDrive, we need to make sure the sync client is actually running."

### Step 2: Sign Out and Sign Back Into OneDrive
1. If OneDrive files are not syncing:
2. Right-click the OneDrive cloud icon in the system tray
3. Click the settings gear > "Settings" > "Account" tab
4. Click "Unlink this PC" (this does not delete your files — they stay in the cloud)
5. OneDrive will prompt you to sign in again
6. Enter your email address and password
7. When prompted for folder location, choose the same location as before
8. OneDrive will re-sync all your files — this can take time depending on how many files you have
9. Check sync status by clicking the cloud icon — it should show "Syncing X files" or "Up to date"

**What to tell the user:** "Sometimes OneDrive loses its authentication token — it's like having an expired key card. We're going to sign out and sign back in. Your files are safe in the cloud the entire time. They'll re-sync back to your computer once you sign in again."

### Step 3: Verify Network Connectivity to the File Server
1. If you receive "Network path not found" errors:
2. Open Command Prompt and ping the server by name:
   ping fileserver
   - Replace "fileserver" with your organization's file server name
   - If ping fails, the server may be unreachable from your network
3. Try pinging the server by IP address instead:
   ping 192.168.1.50
   - If ping by IP works but by name fails, the problem is DNS
4. Check if you are connected to VPN if accessing from home:
   - Shared drives typically require VPN connection to the corporate network
   - Connect to VPN and try the drive again
5. If on-site, check that you are connected to the corporate network, not a guest Wi-Fi

**What to tell the user:** "Your computer can't find the server where the files live. This is like trying to call someone with an old phone number. If you're working from home, make sure your VPN is connected. If you're in the office, check you're on the corporate Wi-Fi, not the guest network."

### Step 4: Check Folder and Share Permissions
1. If you receive "Access Denied", your account may lack the necessary permissions
2. For network shared drives:
   - Right-click the shared drive in File Explorer > "Properties"
   - Go to the "Security" tab
   - Look for your username or groups you belong to in the list
   - Check the permissions listed below (Read, Write, Modify, Full Control)
   - If you do not see your name or have insufficient permissions, contact the drive owner or IT
3. For OneDrive or SharePoint:
   - Open the folder in your browser (OneDrive.com or your SharePoint site)
   - Click "Share" or "Manage access"
   - Verify your account is listed with the appropriate permissions (Can view, Can edit, Owner)
4. If permissions appear correct but access is still denied:
   - Your permission may have been revoked recently
   - You may need to be added to a security group that has access
   - A folder-level permission may be overriding the share-level permission

**What to tell the user:** "Access to shared folders is controlled by permissions — like having a key to a specific room. If your key was revoked or you changed departments, you might have lost access. Let's check what permissions you currently have on this folder."

### Step 5: Re-map the Network Drive
1. If a mapped drive consistently shows disconnected or red X:
2. Disconnect the existing mapped drive:
   - Open Command Prompt and type: net use X: /delete
   - Replace "X:" with the drive letter (e.g., net use Z: /delete)
3. Remap the drive with fresh credentials:
   - Open File Explorer > This PC
   - Click "..." (three dots) > "Map network drive"
   - Select a drive letter (e.g., Z:)
   - Enter the full path: \\server\share
   - Check "Connect using different credentials"
   - Click "Finish"
   - Enter your username in DOMAIN\username format and current password
   - Check "Remember my credentials"
4. Test access by opening the newly mapped drive

**What to tell the user:** "The mapped drive connection may have become corrupted — especially after a password change. We're going to delete the old shortcut and create a fresh one with your current credentials. This is like getting a new, working key card instead of trying to fix the old broken one."

### Step 6: Clear File Explorer History and Credential Manager
1. Old saved credentials can cause persistent access denied errors
2. Open Credential Manager:
   - Type "Credential Manager" in the Start menu search
   - Or Control Panel > User Accounts > Credential Manager
3. Click "Windows Credentials"
4. Look for any saved credentials related to the file server, OneDrive, or SharePoint:
   - Entries may show the server name (e.g., \\fileserver) or domain
5. Click the arrow next to each matching credential > "Remove"
6. Also clear File Explorer history:
   - Open File Explorer > click "..." (three dots) > "Options"
   - In the "General" tab, under "Privacy", click "Clear" next to File Explorer history
7. Restart the computer and try accessing the shared drive again
8. When prompted, enter your current username and password

**What to tell the user:** "Windows saves network passwords in a hidden vault. If your password changed, those saved copies keep trying the old password and failing. We're going to clear them out so Windows asks you for your current password instead."

---

## Alternative Solutions

If the above steps do not resolve the issue, also try:

- Accessing the shared drive from a different computer to determine if the issue is account-related or computer-related
- Using the IP address instead of the server name (e.g., \\192.168.1.50\share instead of \\fileserver\share)
- Checking if your account is locked out, which can prevent access to network resources
- For OneDrive: resetting OneDrive entirely by running the command: %localappdata%\Microsoft\OneDrive\onedrive.exe /reset

---

## Prevention Tips

- Use "Remember my credentials" sparingly — saved passwords become outdated when you change your password
- Bookmark important SharePoint sites in your browser as a backup access method
- Sync only the OneDrive folders you need rather than the entire document library
- Restart your computer at least weekly to refresh network connections
- Note the full network path (\\server\share) of important drives in a safe place

---

## Root Cause

Common causes of shared drive or OneDrive access issues, in order of likelihood:

- Network connection lost or VPN disconnected (most common for remote users)
- Password changed recently but saved credentials not updated
- OneDrive sync client paused, not running, or signed out
- DNS issue preventing server name resolution
- User permissions revoked or changed due to role or department change
- Corrupted mapped drive connection or credential manager entry
- File server or SharePoint site temporarily unavailable

---

## Escalation Decision Matrix

| Condition | Action |
|-----------|--------|
| All 6 steps completed, issue persists | Escalate to Tier 2 |
| Multiple users cannot access the same shared drive | Escalate — likely server or permission group issue |
| User needs permissions changed or added to a security group | Escalate — requires admin access |
| File server unreachable even by IP address | Escalate — server may be down |
| OneDrive sync issues persist after reset | Escalate — possible account or tenant issue |
| User's account is locked or disabled | Escalate — requires account administration |
| Drive re-mapping resolves the issue | Do not escalate — document solution |

---

## Related Articles

- [Access Shared Files & Folders — Quick Guide](../Tier-0-Self-Service/access-shared-files.md) — Tier 0: Self-service guide for accessing shared files
- [NTFS Permission Inheritance & Effective Access Analysis](../Tier-2-Technical-Support/ntfs-permission-inheritance.md) — Tier 2: Advanced permission diagnostics
- [DFS Namespace & Replication Diagnostics](../Tier-3-Expert-Engineering/dfs-namespace-replication.md) — Tier 3: Expert file system analysis

> **Note:** The following related articles are planned for future creation within their respective tier folders:
> - [Access Shared Files & Folders — Quick Guide](../Tier-0-Self-Service/access-shared-files.md)
> - [NTFS Permission Inheritance & Effective Access Analysis](../Tier-2-Technical-Support/ntfs-permission-inheritance.md)
> - [DFS Namespace & Replication Diagnostics](../Tier-3-Expert-Engineering/dfs-namespace-replication.md)

---

## FAQ

**Q: Why does my mapped drive disconnect every time I restart my computer?**
**A:** This usually happens when saved credentials are corrupted or the network is not fully available during startup. Try re-mapping the drive with "Reconnect at sign-in" unchecked, or use a logon script that maps the drive after the network is ready.

**Q: What is the difference between OneDrive and SharePoint?**
**A:** OneDrive is your personal work storage — like your My Documents in the cloud. SharePoint is for team files — shared document libraries that multiple people access. They both sync through the OneDrive sync client, which is why the troubleshooting steps overlap.

**Q: Can I access my shared drives without a VPN?**
**A:** It depends on your organization's setup. Traditional on-premises file servers require VPN. SharePoint and OneDrive are cloud-based and do not require VPN — you can access them from any browser at office.com. Check with your IT department about which type you have.

---

## Commands Quick Reference

| Command | Purpose |
|---------|---------|
| net use | List all mapped network drives and their status |
| net use X: /delete | Disconnect a mapped drive (replace X: with drive letter) |
| net use X: \\server\share | Map a new network drive |
| ping fileserver | Test connectivity to file server by name |
| ping 192.168.1.50 | Test connectivity to file server by IP address |
| %localappdata%\Microsoft\OneDrive\onedrive.exe /reset | Reset OneDrive sync client |

---

## Was this article helpful?

If this article helped resolve your issue, great. If something was unclear, missing, or did not work, please open a GitHub Issue describing the problem so we can improve it.

Suggest improvements at: https://github.com/EzioLockhart/Complete-IT-Support-Knowledge-Base-Tier-0-to-Tier-3/issues

---

## References

- CompTIA A+ Troubleshooting Methodology: Identify the problem, Establish a theory, Test the theory, Establish a plan of action, Verify functionality, Document findings
- ITIL Incident Management best practices: Prioritize based on impact and urgency; file access issues affect productivity
- Microsoft official documentation: Troubleshoot mapped network drives and OneDrive sync issues

---

*Tier: Tier 1 (Help Desk) | Difficulty: L1 (Basic) | Estimated Resolution Time: 10-20 minutes | Required Access Level: User | Severity: P1 (Single User Critical)*

---

For internal use. Follow your organization's file access and data security policies.
