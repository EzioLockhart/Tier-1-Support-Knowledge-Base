# Slow Boot Time and Performance

**Category:** Operating System
**Last Updated:** April 27, 2026
**Applies To:** Windows 10, Windows 11, All Editions

---

## Symptoms

- Computer takes several minutes to boot and reach the desktop
- After login, desktop appears but system is unresponsive for extended period (cursor spinning, clicking does nothing)
- Applications take much longer than usual to open
- Overall system feels sluggish even after boot is complete
- Task Manager shows high disk usage (100%) for extended periods after startup
- Computer was previously fast but gradually slowed down over weeks or months
- Fans run loudly and constantly even during light tasks

---

## Quick Checks (30 seconds)

1. Press Ctrl + Shift + Esc to open Task Manager — check if CPU, Memory, or Disk usage is at 100% and note which process is responsible
2. Check when the computer was last restarted — Task Manager > Performance tab > CPU > look at "Up time". If it is measured in days, a restart alone may fix the issue
3. Check available free disk space on the C: drive — if less than 10% free, performance will degrade significantly
4. Look for any error messages or notifications in the system tray about updates, antivirus, or hardware issues
5. Recall if any new software was installed or any settings were changed just before the slowdown started

---

## Step-by-Step Resolution

### Step 1: Disable Unnecessary Startup Programs

1. Too many programs launching at startup is the number one cause of slow boot and initial sluggishness
2. Open **Task Manager** (Ctrl + Shift + Esc)
3. If Task Manager opens in compact mode, click **"More details"** at the bottom
4. Go to the **"Startup"** tab (left sidebar in Windows 11, top tab in Windows 10)
5. You will see a list of all programs that launch when the computer starts
6. Review the columns:
   - **Name:** The program name
   - **Publisher:** Who made the program
   - **Status:** Enabled or Disabled
   - **Startup impact:** Low, Medium, High, or Not measured — this is the key column
7. Identify programs with **"High"** startup impact:
   - Common high-impact offenders: Microsoft Teams, Slack, Spotify, Adobe Creative Cloud, Steam, OneDrive, Google Drive, Skype, Zoom, Java updater, browser toolbars
8. Right-click on unnecessary high-impact programs > **"Disable"**
   - Do not disable security software (antivirus, firewall), audio/graphics drivers, or anything from Microsoft that you do not recognize
   - Do not disable programs from your computer manufacturer that are required for hardware function (e.g., Synaptics for touchpad, Realtek for audio)
9. Disable programs you do not need immediately at startup — they can still be launched manually when needed
10. Restart the computer and observe the boot time difference
    - Each enabled startup program consumes CPU, RAM, and disk resources during boot; reducing startup programs is the single most impactful change for improving boot time.

### Step 2: Enable or Disable Fast Startup

1. Windows Fast Startup (also called Fast Boot) is a feature that saves system state to a file on shutdown to speed up the next boot
2. On some systems, Fast Startup improves boot time significantly; on others, it causes problems
3. To check and configure Fast Startup:
   - Open **Control Panel** > **Hardware and Sound** > **Power Options**
   - Click **"Choose what the power buttons do"** (left sidebar)
   - Click **"Change settings that are currently unavailable"** (requires administrator)
   - Under **"Shutdown settings"**, look for **"Turn on fast startup (recommended)"**
4. If Fast Startup is **enabled** and you are experiencing slow boots:
   - Try **disabling** it — on some hardware configurations, Fast Startup causes driver conflicts that actually slow down boot
   - Uncheck the box > **"Save changes"**
   - Shut down the computer (not Restart — Fast Startup only applies to shutdown), then power on and test boot time
5. If Fast Startup is **disabled**:
   - Try **enabling** it — this can significantly speed up boot on most modern systems
   - Check the box > **"Save changes"**
   - Shut down and power on to test
6. If neither setting change improves boot time, return it to the original setting
   - Fast Startup is effective for most computers but problematic on some; testing both settings identifies which works best for your specific system.

### Step 3: Free Up Disk Space and Run Disk Cleanup

1. Low disk space, especially on the system drive (C:), forces Windows to constantly struggle for working space
2. Check free space:
   - Open **File Explorer** > **This PC**
   - Look at the C: drive — if the bar is red or shows less than 10 GB free, the drive is critically low on space
3. Delete unnecessary files using Windows built-in tools:
   - Open **Settings** > **System** > **Storage**
   - Click **"Temporary files"**
   - Windows will scan and present a list of file types that can be safely deleted
   - Select: Windows Update Cleanup, Delivery Optimization Files, Temporary files, Recycle Bin, Thumbnails
   - Click **"Remove files"**
4. Run Disk Cleanup for more options:
   - Type "Disk Cleanup" in the Start menu search
   - Right-click **"Disk Cleanup"** > **"Run as administrator"**
   - Select the C: drive > **OK**
   - After scanning, check all boxes — especially:
     - **"Windows Update Cleanup"** (can be several GB)
     - **"Previous Windows installation(s)"** (can be 20+ GB — only appears after a major Windows feature update)
     - **"Temporary files"**
     - **"Delivery Optimization Files"**
   - Click **"OK"** > **"Delete Files"**
5. Uninstall unused applications:
   - **Settings** > **Apps** > **Installed apps**
   - Sort by size to identify large programs
   - Uninstall anything you no longer use
6. Move large personal files (videos, photos, music, downloads) to an external drive or cloud storage
7. After freeing at least 15-20 GB, restart and test performance
   - Windows requires free space for virtual memory paging, temporary files, and update downloads; without adequate free space, every operation slows down.

### Step 4: Adjust Virtual Memory (Paging File) Settings

1. Virtual memory uses a portion of your hard drive as overflow RAM when physical RAM is full
2. Incorrect virtual memory settings can cause severe performance issues
3. Check current settings:
   - Press **Win + R**, type **sysdm.cpl**, press Enter
   - Go to the **"Advanced"** tab
   - Under **"Performance"**, click **"Settings"**
   - Go to the **"Advanced"** tab
   - Under **"Virtual memory"**, click **"Change"**
4. Ensure **"Automatically manage paging file size for all drives"** is checked (recommended for most users)
   - If it is already checked, Windows is managing virtual memory properly — close the dialog
5. If automatic management is unchecked and custom sizes are set:
   - The initial and maximum sizes may be too small
   - Recommended minimum: 1.5 times your physical RAM
   - Example: If you have 8 GB RAM, set Initial size to 12288 MB and Maximum size to 24576 MB
   - Or simply check **"Automatically manage paging file size for all drives"** to let Windows handle it
6. Click **"Set"** then **"OK"** and restart the computer
   - Insufficient virtual memory causes "Out of Memory" errors, application crashes, and extreme slowness when physical RAM is exhausted.

### Step 5: Optimize Visual Effects for Performance

1. Windows visual effects (animations, transparency, shadows) consume CPU and GPU resources
2. Disable or reduce visual effects for better performance:
   - Press **Win + R**, type **sysdm.cpl**, press Enter
   - Go to the **"Advanced"** tab
   - Under **"Performance"**, click **"Settings"**
   - On the **"Visual Effects"** tab, you have three options:
     - **"Let Windows choose what's best for my computer"** (default, balanced)
     - **"Adjust for best appearance"** (all effects on — slowest)
     - **"Adjust for best performance"** (all effects off — fastest, but looks basic)
3. For a balance of performance and appearance:
   - Select **"Custom"**
   - Uncheck the most resource-intensive effects:
     - Animate windows when minimizing and maximizing
     - Animations in the taskbar
     - Fade or slide menus into view
     - Fade or slide ToolTips into view
     - Show shadows under windows
     - Show translucent selection rectangle
     - Slide open combo boxes
     - Taskbar animations
   - Keep checked: "Smooth edges of screen fonts" (this makes text readable)
4. Click **"Apply"** and test system responsiveness
   - Reducing visual effects frees up GPU and CPU resources, which is especially noticeable on computers with integrated graphics or older hardware.

### Step 6: Scan for Malware and Viruses

1. Malware infections are a common cause of sudden, severe performance degradation
2. Run a full scan with Windows Security (built-in):
   - Open **Settings** > **Privacy & Security** > **Windows Security**
   - Click **"Virus & threat protection"**
   - Under **"Current threats"**, click **"Scan options"**
   - Select **"Full scan"** (this scans every file and can take 1-4 hours)
   - Click **"Scan now"**
3. While the full scan runs, also run the Microsoft Defender Offline scan for deeply hidden threats:
   - In the same Scan options menu, select **"Microsoft Defender Offline scan"**
   - Click **"Scan now"** — the computer will restart and scan before Windows loads
4. For a second opinion, run a free on-demand scanner:
   - Malwarebytes Free: malwarebytes.com
   - Download, install, run a full scan, and remove any detected threats
5. After scans complete and any threats are removed, restart the computer and test performance
6. Ensure real-time protection is enabled:
   - Windows Security > Virus & threat protection > Manage settings > Real-time protection: ON
   - Malware can disable Windows processes, hijack system resources, and run hidden background tasks that consume CPU and disk, causing extreme slowness.

### Step 7: Check Disk Health and File System Integrity

1. A failing or corrupted hard drive causes severe performance problems and can lead to data loss
2. Run CHKDSK to check and repair file system errors:
   - Open **Command Prompt as Administrator** (Win + X > Terminal (Admin))
   - Type the following command and press Enter:

chkdsk C: /f /r

   - /f fixes file system errors; /r locates bad sectors and recovers readable data
   - If C: is the system drive, CHKDSK will ask to schedule the scan for the next restart — type Y and press Enter
   - Restart the computer and let CHKDSK run (it can take 1-4 hours depending on drive size and health)
3. Check the drive's SMART status for signs of hardware failure:
   - Open **Command Prompt as Administrator**
   - Type the following and press Enter:

wmic diskdrive get model, status

   - If the status shows anything other than "OK" (e.g., "Pred Fail" or "Bad"), the hard drive is failing and must be replaced immediately
4. If the computer uses a traditional Hard Disk Drive (HDD) and is still slow after all other steps:
   - Consider upgrading to a Solid State Drive (SSD) — this is the single biggest hardware upgrade for boot and performance improvement
   - An SSD can reduce boot time from 3-5 minutes to 20-30 seconds on the same system
5. For existing SSDs:
   - Ensure TRIM is enabled (TRIM helps SSDs manage unused data blocks):
     - Open **Command Prompt as Administrator**
     - Type: fsutil behavior query DisableDeleteNotify
     - If the result is 0, TRIM is enabled and working; if 1, TRIM is disabled
   - Check with the SSD manufacturer's tool (Samsung Magician, Crucial Storage Executive, etc.) for firmware updates
   - A failing hard drive or SSD without TRIM support will cause progressively worsening performance until the drive fails completely.

---

## Root Cause

Common causes of slow boot and performance, in order of likelihood:

- Too many programs launching at startup (most common — each program consumes boot resources)
- Low disk space on the system drive (less than 10% free)
- Hard Disk Drive (HDD) instead of Solid State Drive (SSD) — traditional HDDs are 5-10 times slower than SSDs
- Malware or virus infection consuming system resources in the background
- Windows Fast Startup misconfigured for the specific hardware
- Insufficient virtual memory (paging file too small)
- Too many visual effects enabled on older or lower-spec hardware
- Failing hard drive or SSD with file system errors or bad sectors

---

## Escalation Criteria

Escalate to Tier 2 / Desktop Engineering Team if:

- CHKDSK finds bad sectors — the drive may be failing and should be evaluated for replacement
- SMART status shows "Pred Fail" or "Bad" — the hard drive requires immediate replacement
- The computer is still slow after all troubleshooting steps including disabling startup programs, freeing disk space, and malware scans
- The computer requires an SSD upgrade (hardware procurement and data migration)
- Performance issue affects multiple computers across the organization (possible software deployment or update issue)
- User requires additional RAM upgrade beyond what is currently installed
- Windows repair installation or full reinstallation is needed due to unresolvable system-level corruption
- The computer is under warranty and requires hardware service

---

## Commands and Shortcuts Quick Reference

| Action | How To Access |
|--------|---------------|
| Open Task Manager | Ctrl + Shift + Esc |
| Startup programs | Task Manager > Startup tab |
| System Properties (Performance) | Win + R > sysdm.cpl |
| Disk Cleanup | Start menu > Disk Cleanup > Run as administrator |
| Storage settings | Settings > System > Storage |
| Check disk health (SMART) | Command Prompt (Admin): wmic diskdrive get model, status |
| Check and repair disk | Command Prompt (Admin): chkdsk C: /f /r |
| Check TRIM (SSD) | Command Prompt: fsutil behavior query DisableDeleteNotify |
| Check system uptime | Task Manager > Performance > CPU > Up time |
| Windows Security scan | Settings > Privacy & Security > Windows Security > Virus & threat protection |

---

For internal use. Follow your organization's hardware replacement and software management policies.
