# Application Crashes on Launch

- **Category:** Applications
- **Tier:** Tier 1 (Help Desk)
- **Version:** 1.0
- **Last Updated:** May 2, 2026
- **Last Reviewed:** May 2, 2026
- **Applies To:** Windows 10 (22H2), Windows 11 (23H2), All Desktop Applications
- **Difficulty:** L2 (Intermediate)
- **Estimated Resolution Time:** 15-30 minutes
- **Required Access Level:** Power User
- **Severity:** P1 (Single User, Critical — Application Cannot Be Used)
- **Keywords:** application, crash, launch, startup crash, compatibility mode, Event Viewer, driver, reinstall
- **Prerequisite Knowledge:** Basic Windows navigation, ability to open Event Viewer and Device Manager

---

## Symptoms

- Application opens briefly (splash screen or window appears) then closes immediately
- Error message appears: "[App Name] has stopped working" or "A problem caused the program to stop working correctly"
- Application crashes to desktop without any error message
- Application worked fine previously but now crashes every time it is launched
- Application crashes only when opening a specific file but works otherwise
- Windows Event Viewer shows Application Error events at the exact time of crash
- Reinstalling the application did not resolve the problem

---

## Common Error Codes

| Code | Meaning |
|------|---------|
| 0xC0000005 | Access violation — application tried to access restricted memory |
| 0xC0000135 | Application failed to initialize — missing dependency or DLL |
| 0xC0000409 | Stack buffer overflow — application corrupted its own memory stack |
| Event ID 1000 | Application Error recorded in Event Viewer with faulting module details |

---

## Symptom-to-Step Mapping

| If You See This | Skip To |
|-----------------|---------|
| Crash started after a Windows Update | Step 1 |
| Application is more than 5 years old | Step 2 |
| Error mentions permissions or access denied | Step 3 |
| Crash occurs with graphics-intensive apps | Step 4 |
| Event Viewer shows faulting module name | Step 7 |

---

## Triage Questions

Before starting troubleshooting, ask the user:

1. "Did this application ever work on this computer, or has it always crashed?"
2. "Did the crashes start after a Windows update, driver update, or new software installation?"
3. "Does the crash show any error message, or does it just disappear?"
4. "Have you tried uninstalling and reinstalling the application already?"

---

## Quick Checks (30 seconds)

1. Restart the computer — this alone resolves many temporary crash issues caused by memory conflicts or hung background processes
2. Check if other applications launch successfully — if multiple applications crash, the issue may be system-wide, not specific to one app
3. Try launching the application immediately after a fresh restart without opening any other programs first
4. Check if the application worked before a recent Windows Update — update-induced compatibility issues are common
5. Note any recent changes: new software installed, driver updated, or settings changed just before the crashing started
6. If the application opens but freezes during use rather than crashing on launch, see: [Application Not Responding / Frozen](./app-not-responding.md)

---

## Step-by-Step Resolution

### Step 1: Restart the Computer and Try Again
1. Save any open work in other applications
2. Click Start > Power > Restart
   - Select "Restart" specifically, not "Shut down" — Windows Fast Startup can preserve problematic system states across shutdowns
3. After restart, do not open any other applications yet
4. Launch only the problematic application and test
5. If the application launches successfully, the issue was a temporary memory conflict or background process that the restart cleared

**What to tell the user:** "A clean restart clears your computer's memory and stops all background processes. Sometimes a stuck process from a previous session interferes with the application. A restart gives everything a clean slate."

### Step 2: Run the Application in Compatibility Mode
1. Right-click the application's shortcut on the desktop or in the Start menu
2. Select "Properties"
3. Go to the "Compatibility" tab
4. Check the box: "Run this program in compatibility mode for:"
5. From the dropdown menu, select an older version of Windows:
   - Try Windows 8 first (most compatible for applications built for older Windows)
   - If that fails, try Windows 7
   - For very old applications, try Windows XP (Service Pack 3)
6. Also try checking the following boxes if the first attempt fails:
   - "Run this program as an administrator"
   - "Disable fullscreen optimizations" (helps with graphics-heavy applications)
7. Click "Apply" then "OK"
8. Launch the application and test
9. If it still crashes, return to Compatibility tab and try different Windows versions until one works

**What to tell the user:** "Many older applications were built for specific versions of Windows and crash on newer versions. Compatibility mode tells Windows to pretend it's an older version for just this application. We'll test a few different settings to find one that works."

### Step 3: Run the Application as Administrator
1. Some applications need elevated permissions to access system files, registry keys, or protected folders
2. Right-click the application shortcut or executable file
3. Select "Run as administrator"
4. If the User Account Control (UAC) prompt appears, click "Yes"
5. Test if the application now launches without crashing
6. If this resolves the crash, make it permanent:
   - Right-click the shortcut > Properties > Compatibility tab
   - Check "Run this program as an administrator"
   - Click "Apply" then "OK"
7. Also try installing the application in a folder that does not require elevated permissions (e.g., C:\AppName instead of C:\Program Files) — some applications crash because they cannot write to their own install directory under Program Files

**What to tell the user:** "Some applications need special permissions to access parts of your system. Without those permissions, they crash immediately. We're going to give this application administrator rights to see if that's the problem."

### Step 4: Update Graphics Drivers
1. Many modern applications, especially those with graphical interfaces, depend on graphics drivers
2. Press Win + X > Device Manager
3. Expand "Display adapters"
4. Right-click your graphics card > "Update driver"
5. Select "Search automatically for drivers"
6. If Windows does not find an update, visit the manufacturer's website directly:
   - Intel: downloadcenter.intel.com
   - NVIDIA: nvidia.com/download
   - AMD: amd.com/support
7. Download and install the latest driver for your specific graphics card model
8. Restart the computer after the driver installation
9. If the crashing started after a recent driver update, try "Roll Back Driver" in Device Manager instead

**What to tell the user:** "Your graphics driver translates what applications want to display into what your screen shows. A corrupted or outdated graphics driver is a leading cause of application crashes, especially for visually intensive programs. We're going to check for an update."

### Step 5: Repair the Application Installation
1. Before doing a full reinstall, try a repair which keeps user data and settings intact
2. Go to Settings > Apps > Installed apps (Windows 11) or Apps & features (Windows 10)
3. Find the crashing application in the list
4. Click the three dots (...) next to the application name
5. If available, click "Modify"
6. In the setup wizard, choose "Repair" or "Quick Repair"
7. Follow the wizard prompts to completion
8. Restart the computer and test the application
9. For Microsoft Office applications specifically:
   - Find Microsoft Office in the list
   - Select "Modify" > choose "Quick Repair" first
   - If Quick Repair does not work, run "Online Repair" (this takes longer but is more thorough)

**What to tell the user:** "The application's core files might be corrupted. A repair reinstalls the essential program files without removing your documents or settings. Think of it like fixing a few broken pages in a book rather than replacing the whole book."

### Step 6: Perform a Clean Reinstall of the Application
1. If repair does not resolve the crashes, perform a complete clean uninstall and reinstall
2. First, back up any application data, settings, or custom configurations
3. Uninstall the application:
   - Go to Settings > Apps > Installed apps
   - Find the application > three dots (...) > "Uninstall"
   - Follow the uninstall wizard
4. After uninstall, restart the computer
5. Delete leftover application folders that the uninstaller may leave behind:
   - C:\Program Files\ApplicationName
   - C:\Program Files (x86)\ApplicationName
   - C:\ProgramData\ApplicationName
   - C:\Users\%username%\AppData\Local\ApplicationName
   - C:\Users\%username%\AppData\Roaming\ApplicationName
6. Restart the computer again
7. Download the latest installer from the software developer's official website
8. Install the application fresh
9. Launch and test before restoring any backed-up settings
10. If the application now works, restore settings one at a time to identify if a specific setting was causing the crash

**What to tell the user:** "A regular uninstall sometimes leaves behind corrupted settings files that a fresh install picks right back up. We're going to do a deep clean — remove every trace of the application, then install it completely fresh. This gives us the cleanest possible installation."

### Step 7: Check Event Viewer for Crash Details
1. Windows logs application crashes in Event Viewer, which can provide error codes and faulting modules that pinpoint the exact cause
2. Open Event Viewer: Type "Event Viewer" in the Start menu search, or Win + R > eventvwr.msc
3. In the left pane, expand "Windows Logs"
4. Click on "Application"
5. Look for events with Level: Error at the time the application crashed
6. The most relevant event IDs for application crashes:
   - Event ID 1000: Application Error (crash) — provides faulting module name and exception code
   - Event ID 1001: Windows Error Reporting — provides bucket ID for looking up known issues
7. Double-click the error event to open its details
8. Key fields to note:
   - Faulting application name: Confirms which application crashed
   - Faulting module name: The specific file (DLL, EXE) that caused the crash — this is crucial for identifying root cause
   - Exception code: The type of error (e.g., 0xc0000005 = memory access violation, 0xc0000135 = missing dependency)
9. Common faulting modules and what they indicate:
   - ntdll.dll — often compatibility or system corruption
   - kernelbase.dll — API call failure, often compatibility
   - appname.exe — crash within the application itself, not a dependency
   - d3d9.dll, d3d11.dll, nvoglv64.dll — graphics-related crash
10. Search the error details online for specific solutions

**What to tell the user:** "Windows keeps a detailed log of every application crash. I'm going to look at that log to find the exact file that's causing the crash and the specific error code. This is like reading the black box from an airplane — it tells us exactly what went wrong."

---

## Alternative Solutions

If the above steps do not resolve the issue, also try:

- Installing the application on a different computer to determine if the issue is with the application or the specific machine
- Running the application under a different user profile to rule out user profile corruption
- Performing a clean boot (msconfig > disable all non-Microsoft services) to identify conflicting software
- Checking for and installing any missing runtime frameworks: .NET Framework, Visual C++ Redistributables, DirectX, Java

---

## Prevention Tips

- Keep your applications updated to the latest versions for bug fixes and compatibility improvements
- Keep your graphics drivers and Windows updates current
- Before installing new software, create a system restore point as a safety net
- Avoid installing applications from untrusted sources that may bundle incompatible DLLs
- Periodically review and uninstall unused applications to reduce system clutter

---

## Root Cause

Common causes of application crashes on launch, in order of likelihood:

- Temporary memory conflict or hung background process (resolved by restart — most common)
- Application incompatible with the current version of Windows (resolved by compatibility mode)
- Missing or corrupted application dependency files (DLLs, frameworks like .NET, Visual C++ Redistributables)
- Graphics driver outdated or corrupted (especially for visually intensive applications)
- Application files corrupted due to incomplete update, disk error, or malware
- Corrupted user profile or application configuration files in AppData
- Conflicting third-party software (antivirus, screen overlays, system optimization tools)
- Insufficient permissions to access required system resources (resolved by running as administrator)

---

## Escalation Decision Matrix

| Condition | Action |
|-----------|--------|
| All 7 steps completed, issue persists | Escalate to Tier 2 |
| Application is a business-critical line-of-business (LOB) app | Escalate — requires vendor support |
| Event Viewer shows a specific faulting module requiring developer analysis | Escalate — Tier 3 investigation needed |
| Crash occurs on multiple computers across the organization | Escalate — likely deployment or compatibility issue |
| Application requires specific runtime frameworks to be deployed | Escalate — requires admin deployment |
| Application is custom-built or internally developed | Escalate — needs development team |
| Reinstallation resolves the crash | Do not escalate — document solution |

---

## Related Articles

- [Application Not Responding / Frozen](./app-not-responding.md) — If the application opens but freezes during use
- [Close Frozen Apps & Basic Application Fixes](../Tier-0-Self-Service/close-frozen-apps.md) — Tier 0: Self-service guide for users
- [Application Compatibility & Shim Database Analysis](../Tier-2-Technical-Support/app-compatibility-shim.md) — Tier 2: Advanced compatibility diagnostics
- [Memory Dump Analysis for Application Crashes (WinDbg)](../Tier-3-Expert-Engineering/memory-dump-analysis.md) — Tier 3: Expert-level debugging

> **Note:** If you are looking for the Tier 2 Application Compatibility article or Tier 3 Memory Dump Analysis, these are planned for future creation within their respective tier folders.

---

## FAQ

**Q: Why does an application crash only when opening a specific file?**
**A:** This usually means the file itself is corrupted, or the file type association is broken. Try opening a different file in the same application. If that works, the problem is with the specific file, not the application.

**Q: What is a faulting module and why does it matter?**
**A:** A faulting module is the specific file (usually a DLL) that caused the crash. It matters because it tells you what component failed. For example, if nvoglv64.dll is the faulting module, your NVIDIA graphics driver is the problem. This saves hours of trial-and-error troubleshooting.

**Q: Will compatibility mode slow down my application?**
**A:** Usually not noticeably. Compatibility mode changes how Windows presents itself to the application, but doesn't significantly impact performance. Any minor overhead is worth it for an application that actually works.

---

## Event Viewer Crash Log Quick Reference

| Event ID | Description | Key Fields to Check |
|----------|-------------|---------------------|
| 1000 | Application Error (crash) | Faulting application name, Faulting module name, Exception code |
| 1001 | Windows Error Reporting | Bucket ID (for looking up known issues) |
| 1026 | .NET Runtime error | Exception message and stack trace |
| 1002 | Application Hang | Hung application name, Hang type |

---

## Was this article helpful?

If this article helped resolve your issue, great. If something was unclear, missing, or did not work, please open a GitHub Issue describing the problem so we can improve it.

Suggest improvements at: https://github.com/EzioLockhart/Tier-1-Support-Knowledge-Base/issues

---

## References

- CompTIA A+ Troubleshooting Methodology: Identify the problem, Establish a theory, Test the theory, Establish a plan of action, Verify functionality, Document findings
- ITIL Incident Management best practices: Prioritize based on impact and urgency
- Microsoft official documentation: Troubleshoot application compatibility issues

---

*Tier: Tier 1 (Help Desk) | Difficulty: L2 (Intermediate) | Estimated Resolution Time: 15-30 minutes | Required Access Level: Power User | Severity: P1 (Single User Critical)*

---

For internal use. Follow your organization's software deployment and support policies.
