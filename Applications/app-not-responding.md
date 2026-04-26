# Application Not Responding / Frozen

**Category:** Applications
**Last Updated:** April 27, 2026
**Applies To:** Windows 10, Windows 11, All Desktop Applications

---

## Symptoms

- Application window becomes unresponsive and shows "(Not Responding)" in the title bar
- Mouse cursor changes to spinning circle or hourglass when hovering over the application
- Cannot click buttons, type text, or interact with any part of the application
- Application screen turns white or gray (whited out / ghosted appearance)
- Other applications on the computer continue to work normally
- Task Manager shows the application status as "Not Responding"
- Attempting to close the application by clicking the X button does nothing

---

## Quick Checks (30 seconds)

1. Wait 60 seconds — the application may be processing a heavy task and will recover on its own
2. Check if other applications are also frozen — if yes, the entire system may be overloaded, not just this app
3. Look at your hard drive activity light (physical LED or Task Manager disk usage) — constant activity may indicate the app is still working
4. Press Caps Lock or Num Lock key — if the keyboard light does not toggle, the entire system may be frozen (different issue)
5. Try pressing Esc key or clicking elsewhere in the application to cancel any stuck operation

---

## Step-by-Step Resolution

### Step 1: Wait and Let Windows Recover the Application

1. Stop clicking on the frozen application — every click queues another action and makes the problem worse
2. Wait a full 2 minutes without interacting with the application
3. Windows will attempt to detect the unresponsive state and may display a dialog: "[App Name] is not responding. If you close the program, you might lose information."
4. If this dialog appears, click **"Wait for the program to respond"** first
5. If the application does not recover after 2 minutes, proceed to Step 2
   - Many applications freeze temporarily during intensive tasks like opening large files, running calculations, or auto-saving; patience often resolves the issue without data loss.

### Step 2: Force Quit the Application Using Task Manager

1. Press **Ctrl + Shift + Esc** to open Task Manager directly
   - Alternatively: **Ctrl + Alt + Delete** > Task Manager, or right-click the taskbar > Task Manager
2. If Task Manager opens in compact mode, click **"More details"** at the bottom left
3. In the **"Processes"** tab, find the frozen application in the list under "Apps"
4. Click on the application name to select it
5. Click the **"End task"** button at the bottom right
6. Wait for the application to close — this may take 10-30 seconds
7. If the application does not close:
   - Go to the **"Details"** tab in Task Manager
   - Find the application's executable file (e.g., WINWORD.EXE for Word, EXCEL.EXE for Excel, chrome.exe for Chrome)
   - Right-click the executable > **"End task tree"** (this closes the application and any related sub-processes)
8. Once the application closes, reopen it and check if the issue repeats
   - Force quitting will lose any unsaved work; always try Step 1 first to avoid data loss.

### Step 3: Restart the Computer

1. If the application continues to freeze after force quitting and reopening, restart the computer
2. Click **Start** > **Power** > **Restart**
   - Do not select "Shut down" then power on — Windows Fast Startup may not fully clear the system state; always select "Restart" specifically
3. After restart, open only the problematic application first — do not open other apps immediately
4. Test the application with a simple task to see if freezing persists
   - A restart clears the system memory (RAM), ends all background processes, and resets any temporary system conflicts that may be causing the application to freeze.

### Step 4: Update the Application to the Latest Version

1. Open the application if it is not frozen
2. Check for built-in update options:
   - **Microsoft Office:** File > Account > Update Options > Update Now
   - **Adobe apps:** Help > Check for Updates
   - **Google Chrome:** Three dots menu > Help > About Google Chrome (auto-checks and installs)
   - **Slack, Zoom, Teams:** Click profile icon > Check for Updates
3. If no built-in updater exists, visit the software developer's official website
4. Download and install the latest version
5. Restart the computer after updating
   - Software bugs that cause freezing are often fixed in newer versions; running outdated software is a common root cause.

### Step 5: Run the Application in Compatibility Mode (Older Applications)

1. Right-click the application's shortcut on the desktop or in the Start menu
2. Select **"Properties"**
3. Go to the **"Compatibility"** tab
4. Check the box: **"Run this program in compatibility mode for:"**
5. From the dropdown, select an older version of Windows (e.g., Windows 8, Windows 7, or Windows XP SP3 for very old applications)
6. Also try checking: **"Run this program as an administrator"**
7. Click **"Apply"** then **"OK"**
8. Launch the application and test
9. If the application still freezes, return to Compatibility tab and try **"Disable fullscreen optimizations"** — this helps some graphics-heavy applications
   - Older applications may not fully support newer Windows versions; compatibility mode emulates the older environment.

### Step 6: Repair or Reinstall the Application

1. First try a repair before a full reinstall (keeps settings and data):
   - Go to **Settings** > **Apps** > **Installed apps** (Windows 11) or **Apps & features** (Windows 10)
   - Find the problematic application in the list
   - Click the three dots (...) next to it > **"Modify"** (if available)
   - Choose **"Repair"** or **"Quick Repair"** and follow the wizard
2. If repair is unavailable or does not help, perform a clean reinstall:
   - Go to **Settings** > **Apps** > **Installed apps**
   - Find the application > click three dots (...) > **"Uninstall"**
   - Follow the uninstall wizard and restart the computer
   - Download the latest installer from the software developer's official website
   - Install the application fresh and restart again
3. For Microsoft Office specifically:
   - Use the Microsoft Support and Recovery Assistant (SARA) tool from Microsoft's website
   - This tool can automatically diagnose and repair Office installation issues
4. For stubborn uninstalls, use a third-party cleanup tool like Revo Uninstaller (free version) to remove leftover registry entries and files
   - A clean reinstall removes corrupted program files, registry entries, and configuration files that may be causing freezes.

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

## Escalation Criteria

Escalate to Tier 2 / Application Support Team if:

- The same application freezes across multiple computers in the organization (indicates a network-wide or deployment issue)
- Reinstallation and compatibility mode do not resolve the problem
- The application is a business-critical line-of-business (LOB) application requiring vendor support
- Error messages appear with specific error codes that require advanced diagnosis
- The application requires elevated administrative permissions that the user does not have
- Freezing is accompanied by system-wide slowdowns, blue screens, or repeated crashes (may indicate hardware failure)
- The application is custom-built or internally developed and needs developer investigation

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

For internal use. Follow your organization's escalation procedures.
