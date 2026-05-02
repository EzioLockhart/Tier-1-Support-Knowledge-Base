# Slow Boot Time and Performance

- **Category:** Operating System
- **Tier:** Tier 1 (Help Desk)
- **Version:** 1.0
- **Last Updated:** May 2, 2026
- **Last Reviewed:** May 2, 2026
- **Applies To:** Windows 10 (22H2), Windows 11 (23H2), All Editions
- **Difficulty:** L1 (Basic)
- **Estimated Resolution Time:** 30-60 minutes
- **Required Access Level:** Power User
- **Severity:** P2 (Single User, Degraded — Slow Performance)
- **Keywords:** slow boot, performance, sluggish, startup programs, disk cleanup, SSD, HDD, CHKDSK, RAM, virtual memory
- **Prerequisite Knowledge:** Basic Windows navigation, ability to open Task Manager and Settings

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

## Common Error Codes

| Code | Meaning |
|------|---------|
| Event ID 100 | System startup performance degradation detected |
| Event ID 101 | Application startup performance degradation detected |
| 0x80070070 | Low disk space — system drive has insufficient free space |
| Event ID 55 | Disk corruption detected — CHKDSK recommended |

---

## Symptom-to-Step Mapping

| If You See This | Skip To |
|-----------------|---------|
| Slow only during boot, fine afterward | Step 1 |
| Disk usage stuck at 100% | Step 3 |
| System has less than 10 GB free on C: | Step 3 |
| Slow with animations and transitions | Step 5 |
| Slow performance started suddenly | Step 6 |

---

## Triage Questions

Before starting troubleshooting, ask the user:

1. "Is the slowness only during startup, or does it continue after you've been using the computer for a while?"
2. "Have you installed any new software or updates recently before the slowdown started?"
3. "Does your computer have a traditional hard drive (HDD) or a solid-state drive (SSD)?"
4. "When was the last time you restarted your computer — not just closed the lid, but a full restart?"

---

## Quick Checks (30 seconds)

1. Press Ctrl + Shift + Esc to open Task Manager — check if CPU, Memory, or Disk usage is at 100% and note which process is responsible
2. Check when the computer was last restarted — Task Manager > Performance tab > CPU > look at "Up time". If it is measured in days, a restart alone may fix the issue
3. Check available free disk space on the C: drive — if less than 10% free, performance will degrade significantly
4. Look for any error messages or notifications in the system tray about updates, antivirus, or hardware issues
5. Recall if any new software was installed or any settings were changed just before the slowdown started
6. If the slowness started specifically during or after a Windows Update, see: [Windows Update Stuck or Fails to Install](./windows-update-stuck.md)

---

## Step-by-Step Resolution

### Step 1: Disable Unnecessary Startup Programs
1. Too many programs launching at startup is the number one cause of slow boot and initial sluggishness
2. Open Task Manager (Ctrl + Shift + Esc)
3. If Task Manager opens in compact mode, click "More details" at the bottom
4. Go to the "Startup" tab (left sidebar in Windows 11, top tab in Windows 10)
5. You will see a list of all programs that launch when the computer starts
6. Review the columns:
   - Name: The program name
   - Publisher: Who made the program
   - Status: Enabled or Disabled
   - Startup impact: Low, Medium, High, or Not measured — this is the key column
7. Identify programs with "High" startup impact:
   - Common high-impact offenders: Microsoft Teams, Slack, Spotify, Adobe Creative Cloud, Steam, OneDrive, Google Drive, Skype, Zoom, Java updater
8. Right-click on unnecessary high-impact programs > "Disable"
   - Do not disable security software (antivirus, firewall), audio/graphics drivers, or anything from Microsoft that you do not recognize
9. Disable programs you do not need immediately at startup — they can still be launched manually when needed
10. Restart the computer and observe the boot time difference

**What to tell the user:** "Every program that starts automatically with Windows consumes memory and processing power during boot. Think of it like trying to leave a parking lot with 20 cars all trying to exit at the same time. We're going to identify the programs slowing things down and stop the ones you don't need right away."

### Step 2: Enable or Disable Fast Startup
1. Windows Fast Startup (also called Fast Boot) saves system state to a file on shutdown to speed up the next boot
2. On some systems, Fast Startup improves boot time significantly; on others, it causes problems
3. To check and configure Fast Startup:
   - Open Control Panel > Hardware and Sound > Power Options
   - Click "Choose what the power buttons do" (left sidebar)
   - Click "Change settings that are currently unavailable" (requires administrator)
   - Under "Shutdown settings", look for "Turn on fast startup (recommended)"
4. If Fast Startup is enabled and you are experiencing slow boots:
   - Try disabling it — on some hardware configurations, Fast Startup causes driver conflicts
   - Uncheck the box > "Save changes"
   - Shut down the computer (not Restart), then power on and test boot time
5. If Fast Startup is disabled:
   - Try enabling it — this can significantly speed up boot on most modern systems
   - Check the box > "Save changes"
   - Shut down and power on to test
6. If neither setting change improves boot time, return it to the original setting

**What to tell the user:** "Fast Startup is a feature that saves your system state so it boots faster next time. But on some computers, it actually causes problems. We're going to test whether it's helping or hurting your boot time by toggling it and comparing."

### Step 3: Free Up Disk Space and Run Disk Cleanup
1. Low disk space, especially on the system drive (C:), forces Windows to constantly struggle for working space
2. Check free space:
   - Open File Explorer > This PC
   - Look at the C: drive — if the bar is red or shows less than 10 GB free, the drive is critically low
3. Delete unnecessary files using Windows built-in tools:
   - Open Settings > System > Storage
   - Click "Temporary files"
   - Select: Windows Update Cleanup, Delivery Optimization Files, Temporary files, Recycle Bin, Thumbnails
   - Click "Remove files"
4. Run Disk Cleanup for more options:
   - Type "Disk Cleanup" in the Start menu search
   - Right-click "Disk Cleanup" > "Run as administrator"
   - Select the C: drive > OK
   - Check all boxes — especially "Windows Update Cleanup" (can be several GB) and "Previous Windows installation(s)" (can be 20+ GB)
   - Click "OK" > "Delete Files"
5. Uninstall unused applications: Settings > Apps > Installed apps, sort by size
6. Move large personal files (videos, photos, downloads) to an external drive or cloud storage
7. After freeing at least 15-20 GB, restart and test performance

**What to tell the user:** "Windows needs free space on your drive like a workshop needs clear floor space. When the drive gets too full, Windows has to constantly shuffle things around to make room. We're going to clear out temporary files, old updates, and unused programs to give Windows room to breathe."

### Step 4: Adjust Virtual Memory (Paging File) Settings
1. Virtual memory uses a portion of your hard drive as overflow RAM when physical RAM is full
2. Incorrect virtual memory settings can cause severe performance issues
3. Check current settings:
   - Press Win + R, type sysdm.cpl, press Enter
   - Go to the "Advanced" tab
   - Under "Performance", click "Settings"
   - Go to the "Advanced" tab
   - Under "Virtual memory", click "Change"
4. Ensure "Automatically manage paging file size for all drives" is checked (recommended for most users)
   - If it is already checked, Windows is managing virtual memory properly
5. If automatic management is unchecked and custom sizes are set:
   - The initial and maximum sizes may be too small
   - Recommended minimum: 1.5 times your physical RAM
   - Example: If you have 8 GB RAM, set Initial size to 12288 MB and Maximum size to 24576 MB
   - Or simply check "Automatically manage paging file size for all drives" to let Windows handle it
6. Click "Set" then "OK" and restart the computer

**What to tell the user:** "Virtual memory is like an overflow parking lot for your computer's RAM. When RAM fills up, Windows uses your hard drive as temporary space. If this overflow area is too small, your computer slows to a crawl. Windows usually manages this well, but let's verify the settings."

### Step 5: Optimize Visual Effects for Performance
1. Windows visual effects (animations, transparency, shadows) consume CPU and GPU resources
2. Disable or reduce visual effects for better performance:
   - Press Win + R, type sysdm.cpl, press Enter
   - Go to the "Advanced" tab > Under "Performance", click "Settings"
   - On the "Visual Effects" tab, you have three options:
     - "Let Windows choose what's best for my computer" (default, balanced)
     - "Adjust for best appearance" (all effects on — slowest)
     - "Adjust for best performance" (all effects off — fastest, but looks basic)
3. For a balance of performance and appearance:
   - Select "Custom"
   - Uncheck the most resource-intensive effects: animations when minimizing/maximizing, taskbar animations, fade or slide menus, shadows under windows, translucent selection rectangle
   - Keep checked: "Smooth edges of screen fonts" (this makes text readable)
4. Click "Apply" and test system responsiveness

**What to tell the user:** "Windows spends processing power on visual effects like animations and shadows. On older computers or those with integrated graphics, these effects can significantly slow things down. We're going to turn off the most resource-hungry ones while keeping the ones that make text readable."

### Step 6: Scan for Malware and Viruses
1. Malware infections are a common cause of sudden, severe performance degradation
2. Run a full scan with Windows Security (built-in):
   - Open Settings > Privacy & Security > Windows Security
   - Click "Virus & threat protection"
   - Under "Current threats", click "Scan options"
   - Select "Full scan" (this scans every file and can take 1-4 hours)
   - Click "Scan now"
3. While the full scan runs, also run the Microsoft Defender Offline scan for deeply hidden threats:
   - In the same Scan options menu, select "Microsoft Defender Offline scan"
   - Click "Scan now" — the computer will restart and scan before Windows loads
4. For a second opinion, run a free on-demand scanner:
   - Malwarebytes Free: malwarebytes.com
   - Download, install, run a full scan, and remove any detected threats
5. After scans complete and any threats are removed, restart and test performance
6. Ensure real-time protection is enabled: Windows Security > Virus & threat protection > Manage settings > Real-time protection: ON

**What to tell the user:** "Malware can secretly use your computer's resources in the background — mining cryptocurrency, sending spam, or just running hidden processes. A sudden performance drop is sometimes the only sign. We're going to run a deep scan to make sure your system is clean."

### Step 7: Check Disk Health and File System Integrity
1. A failing or corrupted hard drive causes severe performance problems and can lead to data loss
2. Run CHKDSK to check and repair file system errors:
   - Open Command Prompt as Administrator: Win + X > Terminal (Admin)
   - Type: chkdsk C: /f /r
   - /f fixes file system errors; /r locates bad sectors and recovers readable data
   - If C: is the system drive, CHKDSK will ask to schedule the scan for the next restart — type Y and press Enter
   - Restart and let CHKDSK run (it can take 1-4 hours)
3. Check the drive's SMART status for signs of hardware failure:
   - Open Command Prompt as Administrator
   - Type: wmic diskdrive get model, status
   - If the status shows anything other than "OK" (e.g., "Pred Fail" or "Bad"), the drive is failing
4. If the computer uses a traditional Hard Disk Drive (HDD) and is still slow:
   - Consider upgrading to a Solid State Drive (SSD) — this is the single biggest hardware upgrade for boot and performance
   - An SSD can reduce boot time from 3-5 minutes to 20-30 seconds
5. For existing SSDs, ensure TRIM is enabled:
   - Open Command Prompt as Administrator
   - Type: fsutil behavior query DisableDeleteNotify
   - If the result is 0, TRIM is enabled; if 1, TRIM is disabled and should be enabled

**What to tell the user:** "Your hard drive is like the foundation of your house. If it's failing, everything built on top suffers. We're going to check its health and repair any file system errors. If your computer still uses a traditional spinning hard drive, upgrading to an SSD is the single best investment you can make for speed."

---

## Alternative Solutions

If the above steps do not resolve the issue, also try:

- Running the Windows Performance Monitor (perfmon) to identify specific bottlenecks
- Checking for BIOS updates from your computer or motherboard manufacturer
- Disabling Windows Search indexing temporarily to see if it's causing high disk usage
- Performing a Windows in-place upgrade repair, which reinstalls Windows while keeping your files and apps

---

## Prevention Tips

- Restart your computer at least once a week — do not rely on sleep or hibernate for long periods
- Keep at least 15-20% of your system drive free at all times
- Review your startup programs every few months and disable anything you no longer need
- Keep Windows and all drivers updated for performance fixes and improvements
- Consider upgrading to an SSD if your computer still uses a traditional hard drive

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

## Escalation Decision Matrix

| Condition | Action |
|-----------|--------|
| All 7 steps completed, issue persists | Escalate to Tier 2 |
| CHKDSK finds bad sectors — drive may be failing | Escalate — evaluate for replacement |
| SMART status shows "Pred Fail" or "Bad" | Escalate urgently — drive requires immediate replacement |
| Computer is still slow after disabling startup programs and freeing space | Escalate — deeper investigation needed |
| Computer requires an SSD upgrade (hardware procurement) | Escalate for hardware purchase and data migration |
| Performance issue affects multiple computers organization-wide | Escalate — possible software deployment or update issue |
| Windows repair installation or full reinstallation is needed | Escalate — requires backup and reimaging |

---

## Related Articles

- [Windows Update Stuck or Fails to Install](./windows-update-stuck.md) — If the slowness started after a Windows Update
- [Speed Up Your Computer — Basic Tips](../Tier-0-Self-Service/speed-up-computer-tips.md) — Tier 0: Self-service performance tips
- [Group Policy Processing & Registry Diagnostics](../Tier-2-Technical-Support/group-policy-registry.md) — Tier 2: Advanced system diagnostics
- [BSOD Memory Dump Analysis with WinDbg](../Tier-3-Expert-Engineering/bsod-memory-dump-analysis.md) — Tier 3: Expert-level system analysis

> **Note:** If you are looking for the Tier 0 self-service version of this article, see: [Speed Up Your Computer — Basic Tips](../Tier-0-Self-Service/speed-up-computer-tips.md) (to be created if not yet present).

---

## FAQ

**Q: Why is my computer still slow after disabling all startup programs?**
**A:** The hard drive itself may be the bottleneck. If your computer uses a traditional HDD, it will always be slower than an SSD. Additionally, malware, insufficient RAM, or a failing drive could be the cause. Continue through the remaining steps, especially Step 3 (disk space) and Step 7 (disk health).

**Q: How much RAM do I need for good performance?**
**A:** For Windows 10/11, 8 GB is the minimum for comfortable use. 16 GB is recommended for multitasking with multiple applications. If you have 4 GB or less, your computer relies heavily on virtual memory, which is much slower than physical RAM.

**Q: Is it normal for disk usage to hit 100% at startup?**
**A:** Briefly, yes — Windows loads many services at startup. But if it stays at 100% for more than 5-10 minutes after reaching the desktop, something is wrong. Common causes include Windows Search indexing, antivirus scanning, or a failing drive.

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

## Was this article helpful?

If this article helped resolve your issue, great. If something was unclear, missing, or did not work, please open a GitHub Issue describing the problem so we can improve it.

Suggest improvements at: https://github.com/EzioLockhart/Tier-1-Support-Knowledge-Base/issues

---

## References

- CompTIA A+ Troubleshooting Methodology: Identify the problem, Establish a theory, Test the theory, Establish a plan of action, Verify functionality, Document findings
- ITIL Incident Management best practices: Prioritize based on impact and urgency
- Microsoft official documentation: Tips to improve PC performance in Windows

---

*Tier: Tier 1 (Help Desk) | Difficulty: L1 (Basic) | Estimated Resolution Time: 30-60 minutes | Required Access Level: Power User | Severity: P2 (Single User Degraded)*

---

For internal use. Follow your organization's hardware replacement and software management policies.
