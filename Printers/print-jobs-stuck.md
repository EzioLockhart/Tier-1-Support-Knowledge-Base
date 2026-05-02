# Print Jobs Stuck in Print Queue

**Category:** Printers
**Last Updated:** April 27, 2026
**Applies To:** Windows 10, Windows 11, Local and Network Printers

---

## Symptoms

- Print jobs appear in the queue but never print
- Queue shows status as "Printing" or "Spooling" but nothing comes out of the printer
- Multiple documents are stuck and new print jobs pile up behind them
- Attempts to delete or cancel print jobs fail — they remain in the queue
- Printer itself is powered on, has paper and ink/toner, but does not respond
- The same documents print successfully from other computers sharing the same printer
- Error message in queue: "Error — Printing" or "Sent to printer" with no further action

---

## Quick Checks (30 seconds)

1. Check the printer's physical status — is it turned on, with paper loaded, and without error lights or messages on its display?
2. Is the printer showing "Offline" in the queue window title bar? If yes, resolve that first — see: [Printer Shows as Offline](./printer-offline.md)
3. Check if the printer cable (USB or network) is securely connected at both ends
4. Try printing a test page from another computer — if it works, the problem is local to this machine
5. Look at the queue status — is there one specific document stuck at the top blocking everything behind it?

---

## Step-by-Step Resolution

### Step 1: Cancel All Documents in Print Queue

1. Go to **Settings** > **Bluetooth & devices** > **Printers & scanners**
   - On Windows 10: **Settings** > **Devices** > **Printers & scanners**
2. Select the problematic printer from the list
3. Click **"Open print queue"**
4. In the print queue window, click **"Printer"** in the top menu bar
5. Select **"Cancel All Documents"**
6. Confirm the cancellation if prompted
7. Wait for all documents to clear — this may take 30-60 seconds
8. If documents remain in the queue or new documents appear automatically, the Print Spooler service needs to be restarted (proceed to Step 2)
   - This is the simplest first step; it clears the queue programmatically through Windows. If it fails, the spooler service is likely stuck.

### Step 2: Restart the Print Spooler Service

1. Press **Win + R** to open the Run dialog
2. Type **services.msc** and press Enter
3. In the Services window, scroll down and find **"Print Spooler"**
4. Right-click **"Print Spooler"** > **"Stop"**
5. Wait 10 seconds for the service to fully stop — the Status column should show blank
6. Minimize the Services window but do not close it
7. Press **Win + R** again, type the following path exactly, and press Enter:

C:\Windows\System32\spool\PRINTERS

8. If a permission prompt appears, click **"Continue"**
9. Inside the PRINTERS folder, select all files (Ctrl + A) and delete them (Delete key)
   - These are the stuck print job files; deleting them manually clears jobs that Cancel All Documents cannot remove
   - If any file refuses to delete because it is in use, skip it — the spooler restart will release it
10. Return to the Services window, right-click **"Print Spooler"** > **"Start"**
11. Close Services and check the print queue again — it should be empty
12. Send a test print to verify the printer now works
    - The Print Spooler service manages the entire print workflow; restarting it and clearing the spool folder manually is the most reliable way to clear stuck jobs.

### Step 3: Use Command Prompt to Force Clear the Queue (Alternative Method)

1. If the Services method above does not work, use Command Prompt for a more forceful approach
2. Open **Command Prompt as Administrator** (Win + X > Terminal (Admin))
3. Run these commands one by one, pressing Enter after each:

net stop spooler
del /Q /F /S "%systemroot%\System32\spool\PRINTERS\*.*"
net start spooler

4. Explanation of the command:
   - net stop spooler — stops the Print Spooler service
   - del /Q /F /S — deletes all files (/Q = quiet, no confirmation; /F = force delete read-only files; /S = delete from subdirectories)
   - net start spooler — starts the Print Spooler service again
5. After running all three commands, open the print queue to verify it is empty
6. Send a test print to confirm the printer works
   - Command line provides a more forceful clear method that bypasses GUI limitations sometimes encountered with the Services method.

### Step 4: Remove and Re-add the Printer

1. If print jobs continue to get stuck even after clearing the queue, the printer installation itself may be corrupted
2. Go to **Settings** > **Bluetooth & devices** > **Printers & scanners**
3. Select the problematic printer and click **"Remove"**
4. Confirm removal and restart the computer
5. After restart, go back to **Settings** > **Bluetooth & devices** > **Printers & scanners**
6. Click **"Add device"** or **"Add printer"**
7. Windows will search for available printers — select your printer when it appears
8. If the printer does not appear automatically, click **"Add manually"**:
   - For network printers: select "Add a printer using an IP address or hostname", enter the printer's IP address, and follow prompts
   - For USB printers: ensure the printer is connected and powered on, then retry Add device
9. Set the newly added printer as the default printer if desired
10. Print a test page to confirm functionality
    - Removing and re-adding the printer clears any printer-specific configuration corruption that causes recurring queue problems.

### Step 5: Power Cycle the Printer

1. Sometimes the problem is on the printer itself, not the computer
2. Turn off the printer using its power button
3. Unplug the printer's power cable from the wall outlet or the back of the printer
4. Wait a full 60 seconds — this allows the printer's internal memory to fully clear
5. Plug the power cable back in
6. Turn the printer back on and wait for it to fully initialize (lights stabilize, any startup sounds complete)
7. For network printers: wait an additional 30 seconds for the printer to reacquire its IP address and reconnect to the network
8. On the computer, clear the print queue again using Steps 1 or 2
9. Send a test print
   - Power cycling clears the printer's internal memory, which may contain corrupted or partial print data that causes the printer to freeze and ignore incoming jobs from the computer.

### Step 6: Reinstall or Update the Printer Driver

1. A corrupted or outdated printer driver can cause print jobs to get stuck repeatedly
2. Press **Win + X** > **Device Manager**
3. Expand **"Print queues"** or **"Printers"**
4. Right-click your printer > **"Uninstall device"**
5. Check the box **"Attempt to remove the driver for this device"** if available, then click **"Uninstall"**
6. Restart the computer
7. After restart, download the latest driver from the printer manufacturer's website:
   - Search for your exact printer model number
   - Download the driver package for your version of Windows
   - Install the driver package — most downloads include an automatic installer
8. After installation, add the printer again (Step 4)
9. Print a test page
   - A fresh driver eliminates driver-level corruption or incompatibility that causes repeated queue blockages.

---

## Root Cause

Common causes of print jobs stuck in queue, in order of likelihood:

- Print Spooler service hung or in a crashed state (most common — restart clears it)
- A single corrupted print job blocking the entire queue (the document at the top blocks all jobs behind it)
- Communication error between the computer and printer (USB loose, network drop, or IP address change during printing)
- Printer's internal memory buffer full or containing corrupted data (resolved by power cycling the printer)
- Outdated or corrupted printer driver producing malformed print data
- Large or complex document (e.g., high-resolution PDF, large spreadsheet) overwhelming the printer's memory
- Third-party software conflict (e.g., PDF creation software, print-to-file utilities interfering with the spooler)

---

## Escalation Criteria

Escalate to Tier 2 / Printer Team if:

- The same printer has queue problems across multiple computers (indicates printer hardware, firmware, or network issue)
- Print Spooler service repeatedly stops or crashes even after a restart
- The printer's firmware needs an update that requires administrative access
- Physical printer error persists after power cycling (hardware failure suspected)
- The issue affects a high-volume or business-critical printer requiring immediate attention
- The printer requires service maintenance (e.g., print head cleaning, roller replacement)
- Driver reinstallation does not resolve the recurring queue blockage

---

## Commands and Shortcuts Quick Reference

| Action | How To Access |
|--------|---------------|
| Open Services | Win + R > services.msc |
| Open spool folder (GUI) | Win + R > C:\Windows\System32\spool\PRINTERS |
| Stop spooler (Command Line) | Command Prompt (Admin): net stop spooler |
| Clear spool files (Command Line) | Command Prompt (Admin): del /Q /F /S "%systemroot%\System32\spool\PRINTERS\*.*" |
| Start spooler (Command Line) | Command Prompt (Admin): net start spooler |
| Open Devices and Printers (classic) | Win + R > control printers |
| Open Settings Printers | Settings > Bluetooth & devices > Printers & scanners |

---

For internal use. Follow your organization's printer and device management policies.
