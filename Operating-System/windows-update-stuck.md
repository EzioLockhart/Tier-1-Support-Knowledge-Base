# Windows Update Stuck or Fails to Install

**Category:** Operating System
**Last Updated:** April 27, 2026
**Applies To:** Windows 10, Windows 11, All Editions (Home, Pro, Enterprise)

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

## Quick Checks (30 seconds)

1. Is the computer plugged into power (laptops)? Updates may pause on battery power to prevent shutdown during installation
2. Is there an active internet connection? Open a browser and test if websites load — updates require internet for downloading
3. How long has the update been stuck? Windows updates can legitimately take 30-60 minutes on older or slower systems
4. Check if the hard drive activity light is blinking — constant activity indicates the update is still working, just slowly
5. Press Ctrl + Alt + Delete — if Task Manager opens, the system is not fully frozen; if nothing happens, the system may be hard-locked

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
   - Forcing a restart during an active update can corrupt Windows; only do this as a last resort when the system is clearly hung.

### Step 2: Run Windows Update Troubleshooter

1. Open **Settings** > **System** > **Troubleshoot** > **Other troubleshooters**
   - On Windows 10: **Settings** > **Update & Security** > **Troubleshoot** > **Additional troubleshooters**
2. Find **"Windows Update"** in the list and click **"Run"**
3. The troubleshooter will automatically:
   - Check for pending restarts
   - Verify update services are running
   - Check for corrupted update files
   - Fix incorrect system settings that block updates
4. Follow any recommended fixes and allow the troubleshooter to apply changes
5. Restart the computer after the troubleshooter completes
6. After restart, go to **Settings** > **Windows Update** and click **"Check for updates"**
   - The built-in troubleshooter resolves many common update problems automatically and should always be the first diagnostic step.

### Step 3: Reset Windows Update Components (SoftwareDistribution Folder)

1. This is one of the most effective fixes for stuck or failing updates
2. Open **Command Prompt as Administrator** (Win + X > Terminal (Admin))
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
8. After restart, go to **Settings** > **Windows Update** > **Check for updates**
9. Windows will recreate the SoftwareDistribution folder and re-download updates from scratch
   - This process clears any corrupted or partially downloaded update files that are causing the update to fail or hang.

### Step 4: Run DISM and SFC to Repair System Files

1. Corrupted system files can cause updates to fail repeatedly
2. Open **Command Prompt as Administrator** (Win + X > Terminal (Admin))
3. First, run the System File Checker (SFC) scan to find and repair corrupted Windows files:

sfc /scannow

4. Wait for the scan to complete — this can take 15-45 minutes depending on your system speed
5. SFC will display one of these results when complete:
   - "Windows Resource Protection did not find any integrity violations." — all files are intact, proceed
   - "Windows Resource Protection found corrupt files and successfully repaired them." — issues fixed, restart and test updates
   - "Windows Resource Protection found corrupt files but was unable to fix some of them." — proceed to DISM below
6. Next, run DISM (Deployment Image Servicing and Management) to repair the Windows system image:

DISM /Online /Cleanup-Image /RestoreHealth

7. DISM will check the Windows image against Windows Update servers and repair any corruption — this can take 30-90 minutes
8. The progress bar may appear to pause at certain percentages; this is normal — do not cancel it
9. Once DISM completes successfully, run SFC again (sfc /scannow) to ensure all issues are resolved
10. Restart the computer and retry Windows Update
    - DISM and SFC together repair both the Windows component store (DISM) and individual system files (SFC), resolving update failures caused by system corruption.

### Step 5: Free Up Disk Space and Verify Storage

1. Windows updates, especially feature updates, need significant free space to download and install
2. Check available disk space:
   - Open **Settings** > **System** > **Storage**
   - Ensure the system drive (usually C:) has at least 20-30 GB of free space for major updates
   - For monthly cumulative updates, at least 5-10 GB free is recommended
3. Free up space using Windows built-in tools:
   - In Storage settings, click **"Temporary files"**
   - Select items to remove: Windows Update Cleanup, Delivery Optimization Files, Temporary files, Recycle Bin
   - Click **"Remove files"**
4. Also run Disk Cleanup as Administrator for more options:
   - Type "Disk Cleanup" in Start menu, right-click it > **"Run as administrator"**
   - Select the system drive (C:)
   - Check all boxes, especially **"Windows Update Cleanup"** and **"Previous Windows installation(s)"**
   - Click **"OK"** then **"Delete Files"**
5. Uninstall unused applications from **Settings** > **Apps** > **Installed apps**
6. Move large personal files (videos, photos, documents) to an external drive or cloud storage
7. After freeing space, restart and try Windows Update again
   - Insufficient disk space is a leading cause of update failures; Windows may not provide a clear "not enough space" warning and instead fail with a generic error code.

### Step 6: Install Updates in a Clean Boot State

1. Third-party software and services can interfere with Windows Update
2. Perform a clean boot to start Windows with only Microsoft services:
   - Press **Win + R**, type **msconfig**, and press Enter
   - Go to the **"Services"** tab
   - Check **"Hide all Microsoft services"** (this is important — do not skip)
   - Click **"Disable all"** (this disables only non-Microsoft services)
   - Go to the **"Startup"** tab > click **"Open Task Manager"**
   - In Task Manager's Startup tab, disable all startup items by right-clicking each > **"Disable"**
   - Close Task Manager and click **"OK"** in System Configuration
   - Click **"Restart"** when prompted
3. After restart, the computer will be in a clean boot state
4. Run Windows Update immediately:
   - **Settings** > **Windows Update** > **Check for updates**
   - Install all available updates
5. After updates complete successfully, re-enable normal startup:
   - Open **msconfig** again (Win + R > msconfig)
   - On the **"General"** tab, select **"Normal startup"**
   - Click **"OK"** and restart
   - All your third-party services and startup programs will be restored
   - Clean boot isolates update failures caused by conflicting third-party software.

### Step 7: Manually Download and Install the Failing Update

1. If a specific update keeps failing, you can download it directly from the Microsoft Update Catalog
2. Identify the failing update's KB number:
   - Go to **Settings** > **Windows Update** > **Update history**
   - Find the update that failed and note its KB number (e.g., KB5034441)
3. Open a browser and go to: https://www.catalog.update.microsoft.com
4. Search for the KB number (e.g., "KB5034441")
5. Find the correct version for your system:
   - Check your Windows version: Settings > System > About > look at "System type" (64-bit or 32-bit)
   - Download the matching version (usually "x64-based systems" for modern computers)
6. Click **"Download"** and save the .msu file
7. Once downloaded, double-click the .msu file to install it manually
8. Follow the installation wizard and restart when prompted
9. After restart, check **Settings** > **Windows Update** to confirm the update installed successfully
   - Manual installation bypasses the automatic update process and can succeed when automatic updates repeatedly fail.

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

## Escalation Criteria

Escalate to Tier 2 / Desktop Engineering Team if:

- DISM /RestoreHealth fails with an error (indicates deeper Windows image corruption that may require a repair install)
- The same update continues to fail after all troubleshooting steps above
- The system displays a blue screen (BSOD) during or after update installation
- The computer is stuck in a boot loop that automatic repair cannot resolve
- Multiple computers in the organization fail to install the same update (indicates a deployment or compatibility issue)
- The failing update is a driver update that requires vendor-specific investigation
- The computer requires an in-place upgrade or clean Windows installation to resolve the issue
- Error codes indicate disk failure or hardware problems (e.g., 0x80070002 or 0x8007045D may indicate a failing hard drive)

---

## Commands and Shortcuts Quick Reference

| Action | How To Access |
|--------|---------------|
| Windows Update Troubleshooter | Settings > System > Troubleshoot > Other troubleshooters > Windows Update |
| Open Windows Update | Settings > Windows Update, or Win + R > ms-settings:windowsupdate |
| Stop/Start update services | Command Prompt (Admin): net stop wuauserv, net start wuauserv |
| Reset update cache folders | Command Prompt (Admin): rename SoftwareDistribution and Catroot2 folders |
| SFC scan | Command Prompt (Admin): sfc /scannow |
| DISM repair | Command Prompt (Admin): DISM /Online /Cleanup-Image /RestoreHealth |
| System Configuration (msconfig) | Win + R > msconfig |
| Disk Cleanup | Start menu > Disk Cleanup > Run as administrator |
| Microsoft Update Catalog | https://www.catalog.update.microsoft.com |
| Check Windows version/build | Win + R > winver, or Settings > System > About |

---

For internal use. Follow your organization's software update and change management policies.
