# Application Not Responding / Frozen

- **Category:** Applications
- **Tier:** Tier 1 (Help Desk)
- **Version:** 1.0
- **Last Updated:** May 2, 2026
- **Last Reviewed:** May 2, 2026
- **Applies To:** Windows 10 (22H2), Windows 11 (23H2), All Desktop Applications
- **Difficulty:** L1 (Basic)
- **Estimated Resolution Time:** 5-15 minutes
- **Required Access Level:** User
- **Severity:** P2 (Single User, Degraded — Application Unusable)
- **Keywords:** application, frozen, not responding, hang, Task Manager, force quit, crash, unresponsive
- **Prerequisite Knowledge:** Basic Windows navigation, ability to open Task Manager

---

## Symptoms

- Application window becomes unresponsive and shows "(Not Responding)" in the title bar
- Mouse cursor changes to spinning circle or hourglass when hovering over the application
- Cannot click buttons, type text, or interact with any part of the application
- Application screen turns white or gray (whited out or ghosted appearance)
- Other applications on the computer continue to work normally
- Task Manager shows the application status as "Not Responding"
- Attempting to close the application by clicking the X button does nothing

---

## Common Error Codes

| Code | Meaning |
|------|---------|
| Event ID 1002 | Application hang detected — application stopped responding to Windows messages |
| 0x8000FFFF | Catastrophic failure — application encountered an unrecoverable error |
| 0xC0000005 | Access violation — application tried to access memory it does not own |
| 0x8007000E | Out of memory — system or application ran out of available memory |

---

## Symptom-to-Step Mapping

| If You See This | Skip To |
|-----------------|---------|
| Application just froze, might recover | Step 1 |
| Frozen for more than 2 minutes | Step 2 |
| Freezes again immediately after reopening | Step 3 |
| Application is an older program | Step 5 |
| Freezing started after a recent update | Step 4 |

---

## Triage Questions

Before starting troubleshooting, ask the user:

1. "How long has the application been frozen? Did it just happen, or has it been stuck for a while?"
2. "Were you working on something unsaved when it froze?"
3. "Does this happen every time you use this application, or just this once?"
4. "Is it one specific application frozen, or is your whole computer slow?"

---

## Quick Checks (30 seconds)

1. Wait 60 seconds — the application may be processing a heavy task and will recover on its own
2. Check if other applications are also frozen — if yes, the entire system may be overloaded, not just this app
3. Look at your hard drive activity light (physical LED or Task Manager disk usage) — constant activity may indicate the app is still working
4. Press Caps Lock or Num Lock key — if the keyboard light does not toggle, the entire system may be frozen (different issue)
5. Try pressing Esc key or clicking elsewhere in the application to cancel any stuck operation
6. If the application crashes immediately on launch rather than freezing while in use, see: [Application Crashes on Launch](./app-crashes-on-launch.md)

---

## Step-by-Step Resolution

### Step 1: Wait and Let Windows Recover the Application
1. Stop clicking on the frozen application — every click queues another action and makes the problem worse
2. Wait a full 2 minutes without interacting with the application
3. Windows will attempt to detect the unresponsive state and may display a dialog: "[App Name] is not responding. If you close the program, you might lose information."
4. If this dialog appears, click "Wait for the program to respond" first
5. If the application does not recover after 2 minutes, proceed to Step 2

**What to tell the user:** "Sometimes an application is just busy — processing a large file, running a calculation, or saving in the background. Clicking repeatedly makes it worse by piling up commands. Let's wait 2 full minutes without touching it to see if it recovers on its own."

### Step 2: Force Quit the Application Using Task Manager
1. Press Ctrl + Shift + Esc to open Task Manager directly
   - Alternatively: Ctrl + Alt + Delete > Task Manager, or right-click the taskbar > Task Manager
2. If Task Manager opens in compact mode, click "More details" at the bottom left
3. In the "Processes" tab, find the frozen application in the list under "Apps"
4. Click on the application name to select it
5. Click the "End task" button at the bottom right
6. Wait for the application to close — this may take 10-30 seconds
7. If the application does not close:
   - Go to the "Details" tab in Task Manager
   - Find the application's executable file (e.g., WINWORD.EXE for Word, EXCEL.EXE for Excel, chrome.exe for Chrome)
   - Right-click the executable > "End task tree" (this closes the application and any related sub-processes)
8. Once the application closes, reopen it and check if the issue repeats

**What to tell the user:** "The application is completely stuck, so we need to force it to close. This is like turning off a frozen computer with the power button. Important: any unsaved work in this application will be lost. In the future, try to save frequently to avoid data loss during freezes."

### Step 3: Restart the Computer
1. If the application continues to freeze after force quitting and reopening, restart the computer
2. Click Start > Power > Restart
   - Do not select "Shut down" then power on — Windows Fast Startup may not fully clear the system state; always select "Restart" specifically
3. After restart, open only the problematic application first — do not open other apps immediately
4. Test the application with a simple task to see if freezing persists

**What to tell the user:** "If the app keeps freezing even after force quitting, there might be a temporary memory conflict or a stuck background process. A full restart clears everything and gives the application a clean environment to run in."

### Step 4: Update the Application to the Latest Version
1. Open the application if it is not frozen
2. Check for built-in update options:
   - Microsoft Office: File > Account > Update Options > Update Now
   - Adobe apps: Help > Check for Updates
   - Google Chrome: Three dots menu > Help > About Google Chrome (auto-checks and installs)
   - Slack, Zoom, Teams: Click profile icon > Check for Updates
3. If no built-in updater exists, visit the software developer's official website
4. Download and install the latest version
5. Restart the computer after updating

**What to tell the user:** "Software bugs that cause freezing are often fixed in newer versions. If you're running an old version, updating to the latest one may solve the problem entirely. Let's check if there's an update available."

### Step 5: Run the Application in Compatibility Mode (Older Applications)
1. Right-click the application's shortcut on the desktop or in the Start menu
2. Select "Properties"
3. Go to the "Compatibility" tab
4. Check the box: "Run this program in compatibility mode for:"
5. From the dropdown, select an older version of Windows (e.g., Windows 8, Windows 7, or Windows XP SP3 for very old applications)
6. Also try checking: "Run this program as an administrator"
7. Click "Apply" then "OK"
8. Launch the application and test
9. If the application still freezes, return to Compatibility tab and try "Disable fullscreen optimizations" — this helps some graphics-heavy applications

**What to tell the user:** "Older applications were built for earlier versions of Windows and may not play nicely with newer Windows. Compatibility mode tricks the application into thinking it's running on an older system. We're going to test a few different compatibility settings."

### Step 6: Repair or Reinstall the Application
1. First try a repair before a full reinstall (keeps settings and data):
   - Go to Settings > Apps > Installed apps (Windows 11) or Apps & features (Windows 10)
   - Find the problematic application in the list
   - Click the three dots (...) next to it > "Modify" (if available)
   - Choose "Repair" or "Quick Repair" and follow the wizard
2. If repair is unavailable or does not help, perform a clean reinstall:
   - Go to Settings > Apps > Installed apps
   - Find the application > click three dots (...) > "Uninstall"
   - Follow the uninstall wizard and restart the computer
   - Download the latest installer from the software developer's official website
   - Install the application fresh and restart again
3. For Microsoft Office specifically:
   - Use the Microsoft Support and Recovery Assistant (SARA) tool from Microsoft's website
   - This tool can automatically diagnose and repair Office installation issues
4. For stubborn uninstalls, use a third-party cleanup tool to remove leftover registry entries and files

**What to tell the user:** "The application's program files might be corrupted. We'll try a repair first, which fixes the files without affecting your settings. If that doesn't work, we'll do a clean reinstall — removing everything and starting fresh."

---

## Alternative Solutions

If the above steps do not resolve the issue, also try:

- Running the application as a different user (right-click > Run as different user) to rule out profile corruption
- Checking for conflicting software, especially antivirus programs that may scan the application during use
- Temporarily disabling hardware acceleration in the application's settings (common fix for browser and media app freezes)
- Running System File Checker: sfc /scannow to repair Windows system files the application depends on

---

## Prevention Tips

- Save your work frequently — use Ctrl + S as a habit, especially before large operations
- Keep your applications updated to the latest versions for bug fixes
- Close unused applications to free up system memory (RAM) for the apps you're actively using
- Avoid running too many browser tabs or heavy applications simultaneously
- Restart your computer at least once a week to clear temporary memory issues

---

## Root Cause

Common causes of applications freezing, in order of likelihood:

- Temporary overload from processing a large file, calculation, or background operation (most common — resolves with waiting)
- Insufficient system memory (RAM) — application demands more memory than available
- Software bug in the current version of the application
- Outdated application version incompatible with recent Windows updates
- Conflicting background processes or other applications competing for resources
- Corrupted application files or user profile settings
- Graphics driver incompatibility (especially for graphics-heavy or video applications)
- Hardware limitations — application requires more CPU or RAM than the computer can provide

---

## Escalation Decision Matrix

| Condition | Action |
|-----------|--------|
| All 6 steps completed, issue persists | Escalate to Tier 2 |
| Same application freezes across multiple computers in the organization | Escalate — likely deployment or network-wide issue |
| Reinstallation and compatibility mode do not resolve | Escalate — deeper system or compatibility issue |
| Application is a business-critical line-of-business (LOB) app | Escalate — requires vendor support |
| Error messages appear with specific error codes | Escalate — advanced diagnosis needed |
| Freezing accompanied by system-wide slowdowns or blue screens | Escalate — possible hardware failure |
| Issue resolved by update or reinstall | Do not escalate — document solution |

---

## Related Articles

- [Application Crashes on Launch](./app-crashes-on-launch.md) — If the application closes immediately on opening rather than freezing
- [Close Frozen Apps & Basic Application Fixes](../Tier-0-Self-Service/close-frozen-apps.md) — Tier 0: Self-service guide for users
- [Application Compatibility & Shim Database Analysis](../Tier-2-Technical-Support/app-compatibility-shim.md) — Tier 2: Advanced compatibility diagnostics
- [Memory Dump Analysis for Application Crashes (WinDbg)](../Tier-3-Expert-Engineering/memory-dump-analysis.md) — Tier 3: Expert-level crash analysis

> **Note:** If you are looking for the Tier 0 self-service version of this article, see: [Close Frozen Apps & Basic Application Fixes](../Tier-0-Self-Service/close-frozen-apps.md) (to be created if not yet present).

---

## FAQ

**Q: Why does an application freeze even though my computer has plenty of RAM?**
**A:** RAM is not the only factor. The application might be waiting for a response from the hard drive, network, or another program. It could also be stuck in an infinite loop or have a memory leak where it keeps requesting more RAM until none is left.

**Q: Will force quitting an application corrupt my files?**
**A:** It can. If the application was in the middle of saving a file when frozen, force quitting may corrupt that file. This is why Step 1 is always to wait first — patience gives the application a chance to finish what it was doing.

**Q: How can I tell if the problem is the application or my whole computer?**
**A:** Try pressing Caps Lock. If the light toggles, your computer is still responding — the problem is just the application. If Caps Lock does nothing, your entire system may be hung, which requires a different approach.

---

## Keyboard Shortcuts Quick Reference

| Shortcut | Action |
|----------|--------|
| Ctrl + Shift + Esc | Open Task Manager directly |
| Ctrl + Alt + Delete | Open security screen (access Task Manager, Lock, Sign out) |
| Alt + F4 | Close the currently active (focused) application window |
| Alt + Tab | Switch between open applications |
| Win + Tab | Open Task View to see all open windows |
| Esc | Cancel current operation in many applications |

---

## Was this article helpful?

If this article helped resolve your issue, great. If something was unclear, missing, or did not work, please open a GitHub Issue describing the problem so we can improve it.

Suggest improvements at: https://github.com/EzioLockhart/Tier-1-Support-Knowledge-Base/issues

---

## References

- CompTIA A+ Troubleshooting Methodology: Identify the problem, Establish a theory, Test the theory, Establish a plan of action, Verify functionality, Document findings
- ITIL Incident Management best practices: Prioritize based on impact and urgency
- Microsoft official documentation: Troubleshoot application performance issues

---

*Tier: Tier 1 (Help Desk) | Difficulty: L1 (Basic) | Estimated Resolution Time: 5-15 minutes | Required Access Level: User | Severity: P2 (Single User Degraded)*

---

For internal use. Follow your organization's escalation procedures.
