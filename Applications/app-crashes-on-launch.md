# Application Crashes on Launch

**Category:** Applications
**Last Updated:** April 27, 2026
**Applies To:** Windows 10, Windows 11, All Desktop Applications

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

## Quick Checks (30 seconds)

1. Restart the computer — this alone resolves many temporary crash issues caused by memory conflicts or hung background processes
2. Check if other applications launch successfully — if multiple applications crash, the issue may be system-wide, not specific to one app
3. Try launching the application immediately after a fresh restart without opening any other programs first
4. Check if the application worked before a recent Windows Update — update-induced compatibility issues are common
5. Note any recent changes: new software installed, driver updated, or settings changed just before the crashing started

---

## Step-by-Step Resolution

### Step 1: Restart the Computer and Try Again

1. Save any open work in other applications
2. Click **Start** > **Power** > **Restart**
   - Select "Restart" specifically, not "Shut down" — Windows Fast Startup can preserve problematic system states across shutdowns
3. After restart, do not open any other applications yet
4. Launch only the problematic application and test
5. If the application launches successfully, the issue was a temporary memory conflict or background process that the restart cleared
6. If the application still crashes, continue to the next steps
   - A clean restart clears RAM, ends all processes, and resets temporary system states — this is the simplest and most overlooked fix.

### Step 2: Run the Application in Compatibility Mode

1. Right-click the application's shortcut on the desktop or in the Start menu
2. Select **"Properties"**
3. Go to the **"Compatibility"** tab
4. Check the box: **"Run this program in compatibility mode for:"**
5. From the dropdown menu, select an older version of Windows:
   - Try **Windows 8** first (most compatible for applications built for older Windows)
   - If that fails, try **Windows 7**
   - For very old applications, try **Windows XP (Service Pack 3)**
6. Also try checking the following boxes if the first attempt fails:
   - **"Run this program as an administrator"**
   - **"Disable fullscreen optimizations"** (helps with graphics-heavy applications)
7. Click **"Apply"** then **"OK"**
8. Launch the application and test
9. If it still crashes, return to Compatibility tab and try different Windows versions until one works
   - Many applications, especially older or specialized business software, were built for specific Windows versions and crash on newer versions without compatibility settings.

### Step 3: Run the Application as Administrator

1. Some applications need elevated permissions to access system files, registry keys, or protected folders
2. Right-click the application shortcut or executable file
3. Select **"Run as administrator"**
4. If the User Account Control (UAC) prompt appears, click **"Yes"**
5. Test if the application now launches without crashing
6. If this resolves the crash, make it permanent:
   - Right-click the shortcut > **Properties** > **Compatibility** tab
   - Check **"Run this program as an administrator"**
   - Click **"Apply"** then **"OK"**
7. Also try installing the application in a folder that does not require elevated permissions (e.g., C:\AppName instead of C:\Program Files) — some applications crash because they cannot write to their own install directory under Program Files
   - Running as administrator is often required for line-of-business applications that need to write to protected system areas.

### Step 4: Update Graphics Drivers

1. Many modern applications, especially those with graphical interfaces, depend on graphics drivers
2. Press **Win + X** > **Device Manager**
3. Expand **"Display adapters"**
4. Right-click your graphics card > **"Update driver"**
5. Select **"Search automatically for drivers"**
6. If Windows does not find an update, visit the manufacturer's website directly:
   - Intel: downloadcenter.intel.com
   - NVIDIA: nvidia.com/download
   - AMD: amd.com/support
7. Download and install the latest driver for your specific graphics card model
8. Restart the computer after the driver installation
9. If the crashing started after a recent driver update, try **"Roll Back Driver"** in Device Manager instead
   - Outdated or corrupted graphics drivers are a leading cause of application crashes, especially for visually intensive applications like design software, video editors, and games.

### Step 5: Repair the Application Installation

1. Before doing a full reinstall, try a repair which keeps user data and settings intact
2. Go to **Settings** > **Apps** > **Installed apps** (Windows 11) or **Apps & features** (Windows 10)
3. Find the crashing application in the list
4. Click the three dots (...) next to the application name
5. If available, click **"Modify"**
6. In the setup wizard, choose **"Repair"** or **"Quick Repair"**
7. Follow the wizard prompts to completion
8. Restart the computer and test the application
9. For Microsoft Office applications specifically:
   - Right-click the Start button > **Installed apps** or **Apps & features**
   - Find Microsoft Office in the list
   - Select **"Modify"** > choose **"Quick Repair"** first
   - If Quick Repair does not work, run **"Online Repair"** (this takes longer but is more thorough)
   - Repair reinstalls core application files without removing user documents or settings.

### Step 6: Perform a Clean Reinstall of the Application

1. If repair does not resolve the crashes, perform a complete clean uninstall and reinstall
2. First, back up any application data, settings, or custom configurations
3. Uninstall the application:
   - Go to **Settings** > **Apps** > **Installed apps**
   - Find the application > three dots (...) > **"Uninstall"**
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
    - Leftover corrupted configuration files in AppData folders are a frequent cause of post-reinstall crashes; manually deleting these ensures a truly clean installation.

### Step 7: Check Event Viewer for Crash Details

1. Windows logs application crashes in Event Viewer, which can provide error codes and faulting modules that pinpoint the exact cause
2. Open **Event Viewer**:
   - Type "Event Viewer" in the Start menu search
   - Or Win + R > eventvwr.msc
3. In the left pane, expand **"Windows Logs"**
4. Click on **"Application"**
5. Look for events with **Level: Error** at the time the application crashed
6. The most relevant event IDs for application crashes:
   - **Event ID 1000:** Application Error (crash) — provides faulting module name and exception code
   - **Event ID 1001:** Windows Error Reporting — provides bucket ID for looking up known issues
7. Double-click the error event to open its details
8. Key fields to note:
   - **Faulting application name:** Confirms which application crashed
   - **Faulting module name:** The specific file (DLL, EXE) that caused the crash — this is crucial for identifying root cause
   - **Exception code:** The type of error (e.g., 0xc0000005 = memory access violation, 0xc0000135 = missing dependency)
9. Common faulting modules and what they indicate:
   - ntdll.dll — often compatibility or system corruption
   - kernelbase.dll — API call failure, often compatibility
   - appname.exe — crash within the application itself, not a dependency
   - d3d9.dll, d3d11.dll, nvoglv64.dll — graphics-related crash
10. Search the error details online (Microsoft community, vendor forums, or knowledge bases) for specific solutions related to the faulting module and exception code
    - Event Viewer crash logs provide the technical detail needed to move beyond generic troubleshooting to a specific fix.

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
- If the application opens but freezes during use rather than crashing on launch, see: [Application Not Responding / Frozen](./app-not-responding.md)

---

## Escalation Criteria

Escalate to Tier 2 / Application Support Team if:

- The application is a business-critical line-of-business (LOB) application requiring vendor support
- Event Viewer shows a specific faulting module that requires developer analysis
- Crash occurs on multiple computers across the organization (indicates deployment issue or compatibility problem)
- Application requires specific runtime frameworks (e.g., specific .NET version, Java, Visual C++) that need to be installed by IT
- The application is custom-built or internally developed and needs development team investigation
- Reinstallation and all troubleshooting steps fail repeatedly on multiple machines
- The application crashes with a specific error code that references a known bug requiring a patch from the vendor

---

## Event Viewer Crash Log Quick Reference

| Event ID | Description | Key Fields to Check |
|----------|-------------|---------------------|
| 1000 | Application Error (crash) | Faulting application name, Faulting module name, Exception code |
| 1001 | Windows Error Reporting | Bucket ID (for looking up known issues) |
| 1026 | .NET Runtime error | Exception message and stack trace |
| 1002 | Application Hang | Hung application name, Hang type |

---

## How to Open Event Viewer and Find Crash Logs

| Action | How To Access |
|--------|---------------|
| Open Event Viewer | Start menu > type "Event Viewer", or Win + R > eventvwr.msc |
| Filter for crashes | Windows Logs > Application > Filter Current Log > Event ID 1000 |
| Create custom view | Right-click "Custom Views" > Create Custom View > By Log: Application, Event IDs: 1000, 1001, 1002 |
| Export crash log | Select event > Save Selected Events > Save as .evtx or .txt |

---

For internal use. Follow your organization's software deployment and support policies.
