# Windows Update Stuck or Fails to Install

- **Category:** Operating System
- **Tier:** Tier 1 (Help Desk)
- **Version:** 1.0
- **Last Updated:** May 2, 2026
- **Last Reviewed:** May 2, 2026
- **Applies To:** Windows 10 (22H2), Windows 11 (23H2), All Editions (Home, Pro, Enterprise)
- **Difficulty:** L2 (Intermediate)
- **Estimated Resolution Time:** 20-60 minutes
- **Required Access Level:** Power User
- **Severity:** P2 (Single User, Degraded — System Not Updated)
- **Keywords:** Windows Update, stuck, failed, error code, DISM, SFC, SoftwareDistribution, update, KB
- **Prerequisite Knowledge:** Basic Windows navigation, ability to open Command Prompt as Administrator

---

## Symptoms

- Windows Update progress bar stuck at a percentage (e.g., 45%, 93%, 100%) for hours without completing
- Update shows "Downloading" but the percentage does not change for an extended period
- Update fails with an error code (e.g., 0x80070002, 0x80070005, 0x800705B4, 0x80073712, 0x8024402C)
- Computer repeatedly attempts to install the same update and fails each time, then rolls back
- "Updates are underway. Please keep your computer on." message stays on screen for hours
- Computer stuck in a reboot loop during or after an update installation
- "Something went wrong" or "We couldn't complete the updates. Undoing changes." error message appears

---

## Common Error Codes

| Code | Meaning |
|------|---------|
| 0x80070002 | File not found — update files missing or corrupted |
| 0x80070005 | Access denied — permission issue with update components |
| 0x800705B4 | Timeout error — update installation took too long |
| 0x80073712 | Component store corruption — DISM repair needed |
| 0x8024402C | Windows Update server unreachable — network or firewall issue |

---

## Symptom-to-Step Mapping

| If You See This | Skip To |
|-----------------|---------|
| Update stuck at a percentage for hours | Step 1 |
| Specific error code appears | Step 2 |
| Update fails repeatedly with the same code | Step 3 |
| 0x80073712 error | Step 4 |
| Update downloads but never installs | Step 5 |
| Update fails only on this computer | Step 6 |

---

## Triage Questions

Before starting troubleshooting, ask the user:

1. "How long has the update been stuck? Is it still showing progress, or completely frozen?"
2. "What error code do you see, if any? Even a partial code helps."
3. "Is your computer plugged into power? Updates can pause on battery."
4. "How much free disk space do you have on your C: drive?"

---

## Quick Checks (30 seconds)

1. Is the computer plugged into power (laptops)? Updates may pause on battery power to prevent shutdown during installation
2. Is there an active internet connection? Open a browser and test if websites load — updates require internet for downloading
3. How long has the update been stuck? Windows updates can legitimately take 30-60 minutes on older or slower systems
4. Check if the hard drive activity light is blinking — constant activity indicates the update is still working, just slowly
5. Press Ctrl + Alt + Delete — if Task Manager opens, the system is not fully frozen; if nothing happens, the system may be hard-locked
6. If the system is generally slow even when updates are not running, see: [Slow Boot Time and Performance](./slow-boot-performance.md)

---

## Step-by-Step Resolution

### Step 1: Wait and Check for Actual Progress
1. Windows updates, especially major feature updates (e.g., moving from Windows 10 to Windows 11, or annual feature updates), can take 2-4 hours on slower systems
2. Do not force restart during the "Updates are underway" screen unless the system has been completely unresponsive for more than 4 hours
3. If the screen shows a percentage or spinning circle that is still moving (even slowly), the update is still working — wait longer
4. Check for signs of actual activity:
   - Hard drive LED blinking or solidly lit
   - Fan running (CPU working)
   - Caps Lock or Num Lock key toggles the keyboard light
5. If the system has been completely frozen (no disk activity, no keyboard response, no screen change) for more than 2 hours, proceed to hard restart:
   - Press and hold the power button for 10-15 seconds until the computer shuts off
   - Wait 30 seconds, then power on
   - Windows should detect the failed update and attempt recovery
   - If Windows displays "Undoing changes" on restart, let it complete — this is normal recovery behavior

**What to tell the user:** "Major Windows updates can take several hours on some computers. If the progress indicator is still moving — even barely — the update is still working. Forcing a restart during an update can corrupt Windows, so we only do it as a last resort. Let's check for signs that the update is actually still running."

### Step 2: Run Windows Update Troubleshooter
1. Open Settings > System > Troubleshoot > Other troubleshooters
   - On Windows 10: Settings > Update & Security > Troubleshoot > Additional troubleshooters
2. Find "Windows Update" in the list and click "Run"
3. The troubleshooter will automatically:
   - Check for pending restarts
   - Verify update services are running
   - Check for corrupted update files
   - Fix incorrect system settings that block updates
4. Follow any recommended fixes and allow the troubleshooter to apply changes
5. Restart the computer after the troubleshooter completes
6. After restart, go to Settings > Windows Update and click "Check for updates"

**What to tell the user:** "Windows has a built-in repair tool specifically for update problems. It checks all the background services, clears temporary files, and fixes common issues automatically. It's the safest first step — let's run it now."

### Step 3: Reset Windows Update Components (SoftwareDistribution Folder)
1. This is one of the most effective fixes for stuck or failing updates
2. Open Command Prompt as Administrator: Win + X > Terminal (Admin)
3. Stop the Windows Update services by running these commands one by one:
   net stop wuauserv
   net stop cryptSvc
   net stop bits
   net stop msiserver
4. Wait for each command to say the service stopped successfully before proceeding
5. Rename the SoftwareDistribution and Catroot2 folders (these store update cache files):
   ren C:\Windows\SoftwareDistribution SoftwareDistribution.old
   ren C:\Windows\System32\catroot2 Catroot2.old
6. Restart the services you stopped earlier:
   net start wuauserv
   net start cryptSvc
   net start bits
   net start msiserver
7. Close Command Prompt and restart the computer
8. After restart, go to Settings > Windows Update > Check for updates

**What to tell the user:** "Windows stores all update files in a folder called SoftwareDistribution. When these files get corrupted — which happens more often than you'd think — updates fail or get stuck. We're going to stop the update service, rename that folder so Windows creates a fresh one, and restart. Your update history will be cleared, but no personal files are affected."

### Step 4: Run DISM and SFC to Repair System Files
1. Corrupted system files can cause updates to fail repeatedly
2. Open Command Prompt as Administrator: Win + X > Terminal (Admin)
3. First, run the System File Checker (SFC) scan to find and repair corrupted Windows files: sfc /scannow
4. Wait for the scan to complete — this can take 15-45 minutes depending on your system speed
5. SFC will display one of these results when complete:
   - "Windows Resource Protection did not find any integrity violations." — all files are intact, proceed
   - "Windows Resource Protection found corrupt files and successfully repaired them." — issues fixed, restart and test
   - "Windows Resource Protection found corrupt files but was unable to fix some of them." — proceed to DISM below
6. Next, run DISM (Deployment Image Servicing and Management) to repair the Windows system image:
   DISM /Online /Cleanup-Image /RestoreHealth
7. DISM will check the Windows image against Windows Update servers and repair any corruption — this can take 30-90 minutes
8. The progress bar may appear to pause at certain percentages; this is normal — do not cancel it
9. Once DISM completes successfully, run SFC again to ensure all issues are resolved: sfc /scannow
10. Restart the computer and retry Windows Update

**What to tell the user:** "Windows has two powerful repair tools: SFC checks your actual system files, and DISM repairs the master copy those files come from. Think of SFC as fixing individual broken pages in a book, while DISM replaces the damaged master copy the pages are printed from. Together they fix almost any system file corruption."

### Step 5: Free Up Disk Space and Verify Storage
1. Windows updates, especially feature updates, need significant free space to download and install
2. Check available disk space:
   - Open Settings > System > Storage
   - Ensure the system drive (usually C:) has at least 20-30 GB of free space for major updates
   - For monthly cumulative updates, at least 5-10 GB free is recommended
3. Free up space using Windows built-in tools:
   - In Storage settings, click "Temporary files"
   - Select items to remove: Windows Update Cleanup, Delivery Optimization Files, Temporary files, Recycle Bin
   - Click "Remove files"
4. Also run Disk Cleanup as Administrator for more options:
   - Type "Disk Cleanup" in Start menu, right-click it > "Run as administrator"
   - Select the system drive (C:)
   - Check all boxes, especially "Windows Update Cleanup" and "Previous Windows installation(s)"
   - Click "OK" then "Delete Files"
5. Uninstall unused applications from Settings > Apps > Installed apps
6. Move large personal files (videos, photos, documents) to an external drive or cloud storage

**What to tell the user:** "Windows updates need breathing room to download, extract, and install. If your drive is nearly full, updates fail without always telling you that space is the issue. We need at least 20 GB free for major updates. Let's clear out temporary files and old update leftovers."

### Step 6: Install Updates in a Clean Boot State
1. Third-party software and services can interfere with Windows Update
2. Perform a clean boot to start Windows with only Microsoft services:
   - Press Win + R, type msconfig, and press Enter
   - Go to the "Services" tab
   - Check "Hide all Microsoft services" (this is important — do not skip)
   - Click "Disable all" (this disables only non-Microsoft services)
   - Go to the "Startup" tab > click "Open Task Manager"
   - In Task Manager's Startup tab, disable all startup items by right-clicking each > "Disable"
   - Close Task Manager and click "OK" in System Configuration
   - Click "Restart" when prompted
3. After restart, the computer will be in a clean boot state
4. Run Windows Update immediately: Settings > Windows Update > Check for updates
5. After updates complete successfully, re-enable normal startup:
   - Open msconfig again (Win + R > msconfig)
   - On the "General" tab, select "Normal startup"
   - Click "OK" and restart

**What to tell the user:** "Sometimes antivirus software, backup programs, or other third-party applications interfere with Windows Update. We're going to start Windows in a minimal state with only Microsoft services running — a 'clean boot'. This isolates whether something you installed is blocking the update."

### Step 7: Manually Download and Install the Failing Update
1. If a specific update keeps failing, you can download it directly from the Microsoft Update Catalog
2. Identify the failing update's KB number:
   - Go to Settings > Windows Update > Update history
   - Find the update that failed and note its KB number (e.g., KB5034441)
3. Open a browser and go to: https://www.catalog.update.microsoft.com
4. Search for the KB number (e.g., "KB5034441")
5. Find the correct version for your system:
   - Check your Windows version: Settings > System > About > look at "System type" (64-bit or 32-bit)
   - Download the matching version (usually "x64-based systems" for modern computers)
6. Click "Download" and save the .msu file
7. Once downloaded, double-click the .msu file to install it manually
8. Follow the installation wizard and restart when prompted
9. After restart, check Settings > Windows Update to confirm the update installed successfully

**What to tell the user:** "If one specific update keeps failing, we can bypass the automatic update system entirely and install it manually from Microsoft's catalog. This is like ordering a replacement part directly from the factory instead of waiting for the automatic delivery system. Let's find your failing update's KB number and download it directly."

---

## Alternative Solutions

If the above steps do not resolve the issue, also try:

- Running the Windows Update Assistant from Microsoft's website to force major feature updates
- Temporarily disabling antivirus and firewall software during the update installation
- Using the Media Creation Tool to perform an in-place upgrade, which preserves files and apps
- Checking for and removing any pending updates in the queue before retrying

---

## Prevention Tips

- Keep at least 20-30 GB of free space on your system drive at all times
- Restart your computer at least once a week to allow pending updates to complete
- Do not force-shutdown your computer during updates unless it has been completely frozen for hours
- Regularly run Disk Cleanup as Administrator to remove old update files
- Keep third-party drivers updated, especially graphics and network drivers, which can conflict with updates

---

## Root Cause

Common causes of Windows Update failures, in order of likelihood:

- Corrupted SoftwareDistribution folder (partially downloaded or damaged update cache files) — most common
- Insufficient disk space on the system drive for the update to download and extract
- Conflict with third-party antivirus, firewall, or system optimization software
- Corrupted system files (resolved by DISM and SFC)
- Windows Update services stuck or in a hung state
- Driver incompatibility, especially for major feature updates
- Pending restart from a previous update that was never completed
- Corrupted Windows Update components at the operating system level

---

## Escalation Decision Matrix

| Condition | Action |
|-----------|--------|
| All 7 steps completed, issue persists | Escalate to Tier 2 |
| DISM /RestoreHealth fails with an error | Escalate — deeper Windows image corruption |
| System displays a blue screen (BSOD) during or after update | Escalate — possible hardware or driver issue |
| Computer is stuck in a boot loop that automatic repair cannot resolve | Escalate — requires recovery media |
| Multiple computers in the organization fail the same update | Escalate — likely deployment or compatibility issue |
| Error codes indicate disk failure or hardware problems | Escalate — possible failing hard drive |
| Manual installation from Microsoft Catalog resolves the issue | Do not escalate — document solution |

---

## Related Articles

- [Slow Boot Time and Performance](./slow-boot-performance.md) — If the system is slow even when updates are not running
- [Speed Up Your Computer — Basic Tips](../Tier-0-Self-Service/speed-up-computer-tips.md) — Tier 0: Self-service performance tips
- [Group Policy Processing & Registry Diagnostics](../Tier-2-Technical-Support/group-policy-registry.md) — Tier 2: Advanced system diagnostics
- [BSOD Memory Dump Analysis with WinDbg](../Tier-3-Expert-Engineering/bsod-memory-dump-analysis.md) — Tier 3: Expert-level crash analysis

> **Note:** If you are looking for the Tier 0 self-service version of this article, see: [Speed Up Your Computer — Basic Tips](../Tier-0-Self-Service/speed-up-computer-tips.md) (to be created if not yet present).

---

## FAQ

**Q: How long should I wait before forcing a restart during a stuck update?**
**A:** For major feature updates, wait at least 4 hours if there are signs of activity (disk light, fan). For monthly cumulative updates, 2 hours. Only force restart if the system is completely unresponsive — no disk activity, frozen screen, Caps Lock doesn't toggle.

**Q: Will renaming the SoftwareDistribution folder delete my update history?**
**A:** Yes. Your Windows Update history will be cleared, and Windows will re-scan for needed updates. However, no personal files, installed programs, or settings are affected. Installed updates remain installed.

**Q: What is the difference between SFC and DISM?**
**A:** SFC (System File Checker) scans and repairs individual Windows system files using a local cache. DISM (Deployment Image Servicing and Management) repairs the system image itself — the master copy that SFC uses. If SFC can't fix something, it's because the master copy is damaged, so you run DISM first, then SFC.

---

## Commands and Shortcuts Quick Reference

| Action | How To Access |
|--------|---------------|
| Windows Update Troubleshooter | Settings > System > Troubleshoot > Other troubleshooters > Windows Update |
| Open Windows Update | Settings > Windows Update |
| Stop/Start update services | Command Prompt (Admin): net stop wuauserv |
| Reset update cache folders | Command Prompt (Admin): rename SoftwareDistribution and Catroot2 folders |
| SFC scan | Command Prompt (Admin): sfc /scannow |
| DISM repair | Command Prompt (Admin): DISM /Online /Cleanup-Image /RestoreHealth |
| System Configuration (clean boot) | Win + R > msconfig |
| Disk Cleanup | Start menu > Disk Cleanup > Run as administrator |
| Microsoft Update Catalog | https://www.catalog.update.microsoft.com |
| Check Windows version/build | Win + R > winver |

---

## Was this article helpful?

If this article helped resolve your issue, great. If something was unclear, missing, or did not work, please open a GitHub Issue describing the problem so we can improve it.

Suggest improvements at: https://github.com/EzioLockhart/Tier-1-Support-Knowledge-Base/issues

---

## References

- CompTIA A+ Troubleshooting Methodology: Identify the problem, Establish a theory, Test the theory, Establish a plan of action, Verify functionality, Document findings
- ITIL Incident Management best practices: Prioritize based on impact and urgency
- Microsoft official documentation: Troubleshoot Windows Update errors

---

*Tier: Tier 1 (Help Desk) | Difficulty: L2 (Intermediate) | Estimated Resolution Time: 20-60 minutes | Required Access Level: Power User | Severity: P2 (Single User Degraded)*

---

For internal use. Follow your organization's software update and change management policies.
