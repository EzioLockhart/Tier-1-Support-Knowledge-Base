# Printer Shows as Offline

**Category:** Printers
**Last Updated:** April 27, 2026
**Applies To:** Windows 10, Windows 11, Network Printers, USB Printers

---

## Symptoms

- Printer status shows "Offline" in Devices and Printers
- Print jobs sent but stuck in queue with status "Error — Offline"
- Printer has power and is physically connected but Windows does not detect it
- "Use Printer Offline" option is checked in the printer menu
- Printer was working previously but suddenly shows offline without any changes
- Other computers on the same network can still print to the same printer

---

## Quick Checks (30 seconds)

1. Is the printer powered on? Check for lights on the printer itself — no lights means no power
2. For USB printers: Is the USB cable firmly connected at both ends (printer and computer)? Try a different USB port
3. For network printers: Can you access the printer's web interface by typing its IP address in a browser?
4. Check if other computers can print to the same printer — if yes, problem is isolated to this computer
5. Look at the printer's own display screen — does it show any error messages or blinking lights?

---

## Step-by-Step Resolution

### Step 1: Disable "Use Printer Offline" Mode

1. Go to **Settings** > **Bluetooth & devices** > **Printers & scanners**
   - On Windows 10: **Settings** > **Devices** > **Printers & scanners**
2. Select the problematic printer from the list
3. Click **"Open print queue"**
4. In the print queue window, click **"Printer"** in the top menu bar
5. Look for **"Use Printer Offline"** — if it has a checkmark next to it, click it to uncheck
6. Close and reopen the print queue to verify the printer now shows "Ready"
   - This is the most common and simplest fix; Windows sometimes enables this setting automatically after a failed print job or connectivity hiccup.

### Step 2: Set Printer as Default and Clear Print Queue

1. Go to **Settings** > **Bluetooth & devices** > **Printers & scanners**
2. Select your printer and click **"Set as default"** if the option is available
3. Click **"Open print queue"**
4. In the queue window, click **"Printer"** > **"Cancel All Documents"**
5. Confirm cancellation if prompted
6. If documents refuse to cancel, continue to Step 3 to restart the Print Spooler service
   - Stuck print jobs can cause Windows to mark the printer as offline even when it is physically connected and powered on.

### Step 3: Restart the Print Spooler Service

1. Press **Win + R** to open the Run dialog
2. Type **services.msc** and press Enter
3. In the Services window, scroll down and find **"Print Spooler"**
4. Right-click **"Print Spooler"** > **"Stop"**
5. Wait 10 seconds for the service to fully stop
6. Minimize the Services window (do not close it)
7. Press **Win + R** again, type the following path, and press Enter:

C:\Windows\System32\spool\PRINTERS

8. If prompted for administrator permission, click **Continue**
9. Delete **all files** inside the PRINTERS folder (these are stuck print jobs)
   - If any files cannot be deleted, skip them — they may be in use
10. Return to the Services window, right-click **"Print Spooler"** > **"Start"**
11. Close Services and check if the printer now shows online
    - The Print Spooler manages all print jobs; restarting it clears stuck jobs that can force the printer offline.

### Step 4: Remove and Re-add the Printer

1. Go to **Settings** > **Bluetooth & devices** > **Printers & scanners**
2. Select the problematic printer
3. Click **"Remove"** and confirm deletion
4. Restart the computer
5. After restart, go back to **Settings** > **Bluetooth & devices** > **Printers & scanners**
6. Click **"Add device"** or **"Add printer"**
7. Windows will search for available printers — select your printer when it appears
8. If the printer does not appear automatically, click **"Add manually"** and follow the wizard
   - For network printers: Select "Add a printer using an IP address or hostname", enter the printer's IP, and follow prompts
   - For USB printers: Ensure the printer is connected and powered on before clicking Add device
9. Print a test page to confirm functionality
   - Re-adding the printer clears any corrupted printer configuration on Windows.

### Step 5: Update or Reinstall Printer Driver

1. Press **Win + X** > **Device Manager**
2. Expand **"Print queues"** or **"Printers"**
3. Right-click your printer > **"Update driver"**
4. Select **"Search automatically for drivers"**
5. If Windows finds a new driver, install it and restart
6. If no update is found or the issue persists:
   - Go to the printer manufacturer's website (HP, Canon, Epson, Brother, etc.)
   - Search for your exact printer model number
   - Download the latest driver package for your version of Windows
   - Install the downloaded driver and restart the computer
7. If the issue started after a recent driver update, try **"Roll Back Driver"** instead
   - Corrupted or outdated drivers are a frequent cause of printer communication failures.

### Step 6: Verify Network Printer IP Address and Port

1. On the printer's physical display panel, navigate to **Network Settings** or **Network Configuration**
2. Find and note the printer's **IP address** (e.g., 192.168.1.50)
3. Print a **Network Configuration Page** if available on the printer menu
4. On the computer, go to **Settings** > **Bluetooth & devices** > **Printers & scanners**
5. Select the printer > **"Printer properties"** (not "Printing preferences")
6. Go to the **"Ports"** tab
7. Find the port with the checkmark — it should match the printer's current IP address
8. If the IP does not match:
   - Click **"Add Port"** > **"Standard TCP/IP Port"** > **"New Port"**
   - Enter the printer's current IP address and complete the wizard
   - Select the new port and click **"Apply"**
9. If the printer uses a WSD port (Web Services for Devices), try switching to an IP-based port instead — WSD ports are less reliable
   - Printers with dynamic IP addresses can change IPs if the router or printer restarts, causing the computer to point to the wrong address.

### Step 7: Run Windows Printer Troubleshooter

1. Open **Settings** > **System** > **Troubleshoot** > **Other troubleshooters**
   - On Windows 10: **Settings** > **Update & Security** > **Troubleshoot** > **Additional troubleshooters**
2. Find **"Printer"** in the list and click **"Run"**
3. Follow the on-screen prompts and apply any recommended fixes
4. The troubleshooter will check for common issues including spooler problems, driver issues, and communication errors
5. Restart the computer after the troubleshooter completes
   - The built-in troubleshooter automates many of the manual checks above and can identify issues that were missed.

---

## Root Cause

Common causes of printer showing offline, in order of likelihood:

- "Use Printer Offline" setting accidentally enabled in Windows (most common)
- Stuck print jobs in the queue blocking communication
- Print Spooler service crashed or in a hung state
- Corrupted printer configuration or driver on the local computer
- USB cable loose, damaged, or connected through a faulty USB hub
- Network printer IP address changed (e.g., after router restart or DHCP lease expiry)
- WSD port instability (Windows default for network printers but less reliable than TCP/IP port)
- Printer firmware bug or printer hardware fault
- Windows Update installing an incompatible driver automatically

---

## Escalation Criteria

Escalate to Tier 2 / Network Team if:

- Multiple users cannot connect to the same network printer (indicates printer hardware or network issue)
- Printer's IP address cannot be pinged from any computer on the network
- The printer does not appear on the printer's own display panel network settings (network card failure)
- Driver reinstallation and port reconfiguration do not resolve the issue
- The printer shows offline repeatedly within hours of being fixed
- Printer firmware update is required but admin access is needed
- Physical hardware issue suspected (e.g., printer display shows error code, unusual noises, or no power despite verified power source)

---

## Commands and Shortcuts Quick Reference

| Action | How To Access |
|--------|---------------|
| Open Services | Win + R > services.msc |
| Open Print Spooler folder | C:\Windows\System32\spool\PRINTERS |
| Open Devices and Printers (classic) | Win + R > control printers |
| Open Settings Printers | Settings > Bluetooth & devices > Printers & scanners |
| Run Printer Troubleshooter | Settings > System > Troubleshoot > Other troubleshooters > Printer |
| Printer Properties (Ports tab) | Select printer > Printer properties > Ports |

---

For internal use. Follow your organization's escalation procedures.
