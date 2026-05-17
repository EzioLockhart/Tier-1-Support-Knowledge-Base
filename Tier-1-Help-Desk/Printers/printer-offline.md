# Printer Shows as Offline

- **Category:** Printers
- **Tier:** Tier 1 (Help Desk)
- **Version:** 1.0
- **Last Updated:** May 2, 2026
- **Last Reviewed:** May 2, 2026
- **Applies To:** Windows 10 (22H2), Windows 11 (23H2), Network Printers, USB Printers
- **Difficulty:** L1 (Basic)
- **Estimated Resolution Time:** 10-20 minutes
- **Required Access Level:** Power User
- **Severity:** P2 (Single User, Degraded — Cannot Print)
- **Keywords:** printer, offline, printer status, Use Printer Offline, spooler, network printer, USB printer, port, IP address
- **Prerequisite Knowledge:** Basic Windows navigation, ability to open Settings and Services

---

## Symptoms

- Printer status shows "Offline" in Devices and Printers
- Print jobs sent but stuck in queue with status "Error — Offline"
- Printer has power and is physically connected but Windows does not detect it
- "Use Printer Offline" option is checked in the printer menu
- Printer was working previously but suddenly shows offline without any changes
- Other computers on the same network can still print to the same printer

---

## Common Error Codes

| Code | Meaning |
|------|---------|
| 0x0000011B | Printer driver or connection error — Windows cannot communicate with printer |
| 0x00000002 | Printer connection not available — port or network path not found |
| 0x0000007A | Print spooler service not running or unresponsive |
| 0x80070002 | Printer driver files missing or corrupted |

---

## Symptom-to-Step Mapping

| If You See This | Skip To |
|-----------------|---------|
| "Use Printer Offline" is checked | Step 1 |
| Print queue has stuck documents | Step 2 |
| Spooler service is stopped | Step 3 |
| Printer works from other computers | Step 4 |
| IP address of network printer changed | Step 6 |

---

## Triage Questions

Before starting troubleshooting, ask the user:

1. "Is the printer powered on with lights visible on the printer itself?"
2. "Is this a USB printer connected directly to your computer, or a network printer shared by others?"
3. "Can other people in your office print to this same printer?"
4. "Did this problem start after a Windows update or after moving the printer?"

---

## Quick Checks (30 seconds)

1. Is the printer powered on? Check for lights on the printer itself — no lights means no power
2. For USB printers: Is the USB cable firmly connected at both ends (printer and computer)? Try a different USB port
3. For network printers: Can you access the printer's web interface by typing its IP address in a browser?
4. Check if other computers can print to the same printer — if yes, problem is isolated to this computer
5. Look at the printer's own display screen — does it show any error messages or blinking lights?
6. If print jobs are stuck in the queue after the printer comes back online, see: [Print Jobs Stuck in Print Queue](./print-jobs-stuck.md)

---

## Step-by-Step Resolution

### Step 1: Disable "Use Printer Offline" Mode
1. Go to Settings > Bluetooth & devices > Printers & scanners
   - On Windows 10: Settings > Devices > Printers & scanners
2. Select the problematic printer from the list
3. Click "Open print queue"
4. In the print queue window, click "Printer" in the top menu bar
5. Look for "Use Printer Offline" — if it has a checkmark next to it, click it to uncheck
6. Close and reopen the print queue to verify the printer now shows "Ready"

**What to tell the user:** "Windows sometimes automatically sets a printer to offline mode after a failed print job or a brief connection hiccup. We're going to check this setting first because it's the most common and simplest fix — often just one click."

### Step 2: Set Printer as Default and Clear Print Queue
1. Go to Settings > Bluetooth & devices > Printers & scanners
2. Select your printer and click "Set as default" if the option is available
3. Click "Open print queue"
4. In the queue window, click "Printer" > "Cancel All Documents"
5. Confirm cancellation if prompted
6. If documents refuse to cancel, continue to Step 3 to restart the Print Spooler service

**What to tell the user:** "A stuck print job can cause Windows to mark the printer as offline. We're going to clear everything in the queue so the printer can start fresh. Any pending documents will need to be resent afterward."

### Step 3: Restart the Print Spooler Service
1. Press Win + R to open the Run dialog
2. Type services.msc and press Enter
3. In the Services window, scroll down and find "Print Spooler"
4. Right-click "Print Spooler" > "Stop"
5. Wait 10 seconds for the service to fully stop
6. Minimize the Services window (do not close it)
7. Press Win + R again, type the following path, and press Enter: C:\Windows\System32\spool\PRINTERS
8. If prompted for administrator permission, click Continue
9. Delete all files inside the PRINTERS folder (these are stuck print jobs)
10. Return to the Services window, right-click "Print Spooler" > "Start"
11. Close Services and check if the printer now shows online

**What to tell the user:** "The Print Spooler is a background service that manages all printing on your computer. When it gets stuck, it can force your printer to show as offline. We're going to restart it and clear out any stuck print files. This is like rebooting just the printing part of Windows."

### Step 4: Remove and Re-add the Printer
1. Go to Settings > Bluetooth & devices > Printers & scanners
2. Select the problematic printer
3. Click "Remove" and confirm deletion
4. Restart the computer
5. After restart, go back to Settings > Bluetooth & devices > Printers & scanners
6. Click "Add device" or "Add printer"
7. Windows will search for available printers — select your printer when it appears
8. If the printer does not appear automatically, click "Add manually":
   - For network printers: Select "Add a printer using an IP address or hostname", enter the printer's IP, and follow prompts
   - For USB printers: Ensure the printer is connected and powered on before clicking Add device
9. Print a test page to confirm functionality

**What to tell the user:** "Sometimes the printer installation on your computer gets corrupted. We're going to remove it completely and add it back fresh. This clears any bad settings while keeping the printer itself unchanged. You'll need to know the printer's IP address if it's a network printer."

### Step 5: Update or Reinstall Printer Driver
1. Press Win + X > Device Manager
2. Expand "Print queues" or "Printers"
3. Right-click your printer > "Update driver"
4. Select "Search automatically for drivers"
5. If Windows finds a new driver, install it and restart
6. If no update is found or the issue persists:
   - Go to the printer manufacturer's website (HP, Canon, Epson, Brother, etc.)
   - Search for your exact printer model number
   - Download the latest driver package for your version of Windows
   - Install the downloaded driver and restart the computer
7. If the issue started after a recent driver update, try "Roll Back Driver" instead

**What to tell the user:** "Printer drivers are the translators between your computer and the printer. A corrupted or outdated driver causes communication failures. We're going to check for an updated driver or install a fresh one from the manufacturer."

### Step 6: Verify Network Printer IP Address and Port
1. On the printer's physical display panel, navigate to Network Settings or Network Configuration
2. Find and note the printer's IP address (e.g., 192.168.1.50)
3. Print a Network Configuration Page if available on the printer menu
4. On the computer, go to Settings > Bluetooth & devices > Printers & scanners
5. Select the printer > "Printer properties" (not "Printing preferences")
6. Go to the "Ports" tab
7. Find the port with the checkmark — it should match the printer's current IP address
8. If the IP does not match:
   - Click "Add Port" > "Standard TCP/IP Port" > "New Port"
   - Enter the printer's current IP address and complete the wizard
   - Select the new port and click "Apply"
9. If the printer uses a WSD port (Web Services for Devices), try switching to an IP-based port instead

**What to tell the user:** "Network printers are identified by their IP address, like a house address for delivering mail. If the printer's IP address changed — which can happen after a router restart — your computer is looking for it at the wrong address. We're going to update the address to match."

### Step 7: Run Windows Printer Troubleshooter
1. Open Settings > System > Troubleshoot > Other troubleshooters
   - On Windows 10: Settings > Update & Security > Troubleshoot > Additional troubleshooters
2. Find "Printer" in the list and click "Run"
3. Follow the on-screen prompts and apply any recommended fixes
4. The troubleshooter will check for common issues including spooler problems, driver issues, and communication errors
5. Restart the computer after the troubleshooter completes

**What to tell the user:** "Windows has a built-in printer diagnostic tool. Let's run it now — it checks for problems automatically and can apply fixes for issues we might have missed. Think of it as a second set of eyes looking at the problem."

---

## Alternative Solutions

If the above steps do not resolve the issue, also try:

- Connecting the printer to a different USB port or using a different USB cable
- Power cycling the printer: turn it off, unplug for 60 seconds, plug back in, and turn on
- Checking if the printer firmware needs an update from the manufacturer's website
- Temporarily disabling Windows Firewall to test if it's blocking printer communication

---

## Prevention Tips

- Restart your computer and printer at least once a month to clear memory and refresh connections
- Keep printer drivers updated through Windows Update or the manufacturer's website
- For network printers, assign a static IP address to prevent it from changing after router restarts
- Avoid using WSD ports for network printers — use Standard TCP/IP ports instead, which are more reliable
- Label your printer with its IP address so you can quickly reconfigure it if needed

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

## Escalation Decision Matrix

| Condition | Action |
|-----------|--------|
| All 7 steps completed, issue persists | Escalate to Tier 2 |
| Multiple users cannot connect to the same network printer | Escalate — likely printer hardware or network issue |
| Printer's IP address cannot be pinged from any computer | Escalate — network card or physical connection failure |
| Driver reinstallation and port reconfiguration do not resolve | Escalate — deeper system or compatibility issue |
| Printer shows offline repeatedly within hours of being fixed | Escalate — possible firmware or hardware fault |
| Printer firmware update is required but admin access needed | Escalate for firmware update |
| Physical issue suspected (error code on printer display, unusual noises) | Escalate — hardware repair needed |

---

## Related Articles

- [Print Jobs Stuck in Print Queue](./print-jobs-stuck.md) — If the printer shows online but documents won't print
- [Print Server Queue Corruption & SNMP Configuration](../Tier-2-Technical-Support/print-server-snmp.md) — Tier 2: Advanced printer diagnostics

---

## FAQ

**Q: Why does my printer keep going offline even after I fix it?**
**A:** Repeated offline issues usually indicate one of three things: the printer has a dynamic IP that keeps changing, you're using a WSD port instead of a TCP/IP port, or the printer has a firmware bug. Switch to a static IP and TCP/IP port as a permanent fix.

**Q: What is the difference between a WSD port and a TCP/IP port?**
**A:** WSD (Web Services for Devices) is Windows' automatic discovery method. It's convenient but less reliable than a standard TCP/IP port, which uses the printer's IP address directly. For business environments, always use TCP/IP ports for stability.

**Q: Will removing and re-adding the printer delete my print jobs?**
**A:** Yes. Any pending print jobs stuck in the queue will be lost when you remove the printer. If you need to keep a document, cancel the print job first and save the document before removing the printer.

---

## Commands and Shortcuts Quick Reference

| Action | How To Access |
|--------|---------------|
| Open Services | Win + R > services.msc |
| Open Print Spooler folder | C:\Windows\System32\spool\PRINTERS |
| Open classic Devices and Printers | Win + R > control printers |
| Open Settings Printers | Settings > Bluetooth & devices > Printers & scanners |
| Run Printer Troubleshooter | Settings > System > Troubleshoot > Other troubleshooters > Printer |
| Printer Properties (Ports tab) | Select printer > Printer properties > Ports |

---

## Was this article helpful?

If this article helped resolve your issue, great. If something was unclear, missing, or did not work, please open a GitHub Issue describing the problem so we can improve it.

Suggest improvements at: https://github.com/EzioLockhart/Tier-1-Support-Knowledge-Base/issues

---

## References

- CompTIA A+ Troubleshooting Methodology: Identify the problem, Establish a theory, Test the theory, Establish a plan of action, Verify functionality, Document findings
- ITIL Incident Management best practices: Prioritize based on impact and urgency
- Microsoft official documentation: Fix printer connection and printing problems in Windows

---

*Tier: Tier 1 (Help Desk) | Difficulty: L1 (Basic) | Estimated Resolution Time: 10-20 minutes | Required Access Level: Power User | Severity: P2 (Single User Degraded)*

---

For internal use. Follow your organization's escalation procedures.
