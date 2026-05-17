# Print Jobs Stuck in Print Queue

- **Category:** Printers
- **Tier:** Tier 1 (Help Desk)
- **Version:** 1.0
- **Last Updated:** May 2, 2026
- **Last Reviewed:** May 2, 2026
- **Applies To:** Windows 10 (22H2), Windows 11 (23H2), Local and Network Printers
- **Difficulty:** L1 (Basic)
- **Estimated Resolution Time:** 10-15 minutes
- **Required Access Level:** Power User
- **Severity:** P2 (Single User, Degraded — Cannot Print)
- **Keywords:** printer, queue, stuck, spooler, print jobs, cancel documents, printing, spooling, PRINTERS folder
- **Prerequisite Knowledge:** Basic Windows navigation, ability to open Services and Command Prompt

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

## Common Error Codes

| Code | Meaning |
|------|---------|
| 0x0000007A | Print spooler service is not running or is unresponsive |
| 0x000003E3 | Print job was deleted before it could be sent to the printer |
| 0x00000002 | Printer connection not available — port or network path issue |
| 0x80070706 | Print spooler cannot access the spool file — file locked or corrupted |

---

## Symptom-to-Step Mapping

| If You See This | Skip To |
|-----------------|---------|
| One specific document stuck at top of queue | Step 1 |
| Cancel All Documents does nothing | Step 2 |
| Queue clears but new jobs get stuck again | Step 4 |
| Printer works from other computers | Step 5 |
| Problem returns days after being fixed | Step 6 |

---

## Triage Questions

Before starting troubleshooting, ask the user:

1. "Is it one specific document stuck at the top, or are all print jobs failing?"
2. "Can other people in your office print to this same printer successfully?"
3. "Have you tried canceling the print jobs? What happened when you did?"
4. "Did this start after printing a specific type of document, like a large PDF or spreadsheet?"

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
1. Go to Settings > Bluetooth & devices > Printers & scanners
   - On Windows 10: Settings > Devices > Printers & scanners
2. Select the problematic printer from the list
3. Click "Open print queue"
4. In the print queue window, click "Printer" in the top menu bar
5. Select "Cancel All Documents"
6. Confirm the cancellation if prompted
7. Wait for all documents to clear — this may take 30-60 seconds
8. If documents remain in the queue, proceed to Step 2

**What to tell the user:** "We're going to cancel everything waiting in the print queue. This is the simplest approach — telling Windows to stop all printing and clear the list. Sometimes this works immediately. If it doesn't, we'll take stronger steps."

### Step 2: Restart the Print Spooler Service
1. Press Win + R to open the Run dialog
2. Type services.msc and press Enter
3. In the Services window, scroll down and find "Print Spooler"
4. Right-click "Print Spooler" > "Stop"
5. Wait 10 seconds for the service to fully stop — the Status column should show blank
6. Minimize the Services window but do not close it
7. Press Win + R again, type the following path exactly, and press Enter: C:\Windows\System32\spool\PRINTERS
8. If a permission prompt appears, click "Continue"
9. Inside the PRINTERS folder, select all files (Ctrl + A) and delete them (Delete key)
   - These are the stuck print job files; deleting them manually clears jobs that Cancel All Documents cannot remove
   - If any file refuses to delete because it is in use, skip it
10. Return to the Services window, right-click "Print Spooler" > "Start"
11. Close Services and check the print queue again — it should be empty
12. Send a test print to verify the printer now works

**What to tell the user:** "The Print Spooler is the background service that manages every print job. When it gets stuck, it's like a traffic jam where no cars move. We're going to stop the service, manually remove the stuck files, and restart it. This clears everything and gives the printer a fresh start."

### Step 3: Use Command Prompt to Force Clear the Queue
1. If the Services method does not work, use Command Prompt for a more forceful approach
2. Open Command Prompt as Administrator: Win + X > Terminal (Admin)
3. Run these commands one by one, pressing Enter after each:
   net stop spooler
   del /Q /F /S "%systemroot%\System32\spool\PRINTERS\*.*"
   net start spooler
4. Explanation of the commands:
   - net stop spooler — stops the Print Spooler service
   - del /Q /F /S — deletes all files (/Q = quiet, no confirmation; /F = force delete read-only files; /S = delete from subdirectories)
   - net start spooler — starts the Print Spooler service again
5. After running all three commands, open the print queue to verify it is empty
6. Send a test print to confirm the printer works

**What to tell the user:** "The graphical interface sometimes can't force-remove stuck jobs. We're using the command line, which gives us more direct control. These three commands stop the spooler, delete everything stuck, and restart it — all in one sequence."

### Step 4: Remove and Re-add the Printer
1. If print jobs continue to get stuck even after clearing the queue, the printer installation itself may be corrupted
2. Go to Settings > Bluetooth & devices > Printers & scanners
3. Select the problematic printer and click "Remove"
4. Confirm removal and restart the computer
5. After restart, go back to Settings > Bluetooth & devices > Printers & scanners
6. Click "Add device" or "Add printer"
7. Windows will search for available printers — select your printer when it appears
8. If the printer does not appear automatically, click "Add manually":
   - For network printers: select "Add a printer using an IP address or hostname", enter the printer's IP address
   - For USB printers: ensure the printer is connected and powered on, then retry Add device
9. Set the newly added printer as the default printer if desired
10. Print a test page to confirm functionality

**What to tell the user:** "If print jobs keep getting stuck after clearing the queue, the printer setup on your computer might have a deeper corruption. We're going to remove the printer completely and add it back fresh. This clears any bad configuration without affecting the printer itself."

### Step 5: Power Cycle the Printer
1. Sometimes the problem is on the printer itself, not the computer
2. Turn off the printer using its power button
3. Unplug the printer's power cable from the wall outlet or the back of the printer
4. Wait a full 60 seconds — this allows the printer's internal memory to fully clear
5. Plug the power cable back in
6. Turn the printer back on and wait for it to fully initialize (lights stabilize, any startup sounds complete)
7. For network printers: wait an additional 30 seconds for the printer to reacquire its IP address
8. On the computer, clear the print queue again using Steps 1 or 2
9. Send a test print

**What to tell the user:** "The printer itself has its own small computer inside with memory that stores incoming print data. If that memory gets full or corrupted, the printer stops processing jobs. Power cycling — fully unplugging it — clears that internal memory."

### Step 6: Reinstall or Update the Printer Driver
1. A corrupted or outdated printer driver can cause print jobs to get stuck repeatedly
2. Press Win + X > Device Manager
3. Expand "Print queues" or "Printers"
4. Right-click your printer > "Uninstall device"
5. Check the box "Attempt to remove the driver for this device" if available, then click "Uninstall"
6. Restart the computer
7. After restart, download the latest driver from the printer manufacturer's website:
   - Search for your exact printer model number
   - Download the driver package for your version of Windows
   - Install the driver package
8. After installation, add the printer again (Step 4)
9. Print a test page

**What to tell the user:** "The printer driver translates your documents into a language the printer understands. A corrupted driver creates malformed data that gets stuck in the queue. We're going to install a fresh driver directly from the manufacturer, which gives the printer a clean translator."

---

## Alternative Solutions

If the above steps do not resolve the issue, also try:

- Printing the document as a PDF first, then printing the PDF — this bypasses application-specific formatting issues
- Reducing the print quality or resolution for large documents that may overwhelm the printer's memory
- Connecting via a different method (e.g., USB instead of network, or vice versa) to isolate the connection type
- Checking if the document itself is corrupted by printing a different simple document like a test page

---

## Prevention Tips

- Avoid printing extremely large documents (100+ pages) in one job — split them into smaller batches
- Restart your computer at least once a week to refresh the Print Spooler service
- Keep printer drivers updated through Windows Update or the manufacturer's website
- For network printers, ensure the printer has a static IP address to prevent connection interruptions
- Empty your print queue regularly — don't let failed jobs accumulate

---

## Root Cause

Common causes of print jobs stuck in queue, in order of likelihood:

- Print Spooler service hung or in a crashed state (most common — restart clears it)
- A single corrupted print job blocking the entire queue (the document at the top blocks all jobs behind it)
- Communication error between the computer and printer (USB loose, network drop, or IP address change during printing)
- Printer's internal memory buffer full or containing corrupted data (resolved by power cycling)
- Outdated or corrupted printer driver producing malformed print data
- Large or complex document (e.g., high-resolution PDF, large spreadsheet) overwhelming the printer's memory
- Third-party software conflict (e.g., PDF creation software, print-to-file utilities interfering with the spooler)

---

## Escalation Decision Matrix

| Condition | Action |
|-----------|--------|
| All 6 steps completed, issue persists | Escalate to Tier 2 |
| Same printer has queue problems across multiple computers | Escalate — likely printer hardware, firmware, or network issue |
| Print Spooler service repeatedly stops or crashes | Escalate — possible system-level corruption |
| Printer firmware needs an update requiring administrative access | Escalate for firmware update |
| Physical printer error persists after power cycling | Escalate — hardware failure suspected |
| Issue affects a high-volume or business-critical printer | Escalate with urgency |
| Driver reinstallation resolves the issue | Do not escalate — document solution |

---

## Related Articles

- [Printer Shows as Offline](./printer-offline.md) — If the printer shows offline before jobs get stuck
- [Print Server Queue Corruption & SNMP Configuration](../Tier-2-Technical-Support/print-server-snmp.md) — Tier 2: Advanced queue diagnostics

---

## FAQ

**Q: Why do print jobs reappear after I delete them from the queue?**
**A:** This usually means the Print Spooler service has a persistent corruption. Use the command-line method in Step 3 rather than the graphical Cancel All Documents — it's more forceful. If jobs still reappear, the spooler may need a full reset including clearing the PRINTERS folder manually.

**Q: Will restarting the Print Spooler affect other printers connected to my computer?**
**A:** Yes. The Print Spooler service manages all printers on your computer. When you restart it, all print queues for all printers are cleared. Any pending jobs for other printers will also be deleted.

**Q: Can a large document really get stuck just because of its size?**
**A:** Yes. Large documents, especially high-resolution PDFs or spreadsheets with many pages, can exceed the printer's memory capacity. The printer receives part of the job, runs out of memory, and stops responding — leaving the job stuck in the queue on your computer.

---

## Commands and Shortcuts Quick Reference

| Action | How To Access |
|--------|---------------|
| Open Services | Win + R > services.msc |
| Open spool folder (GUI) | Win + R > C:\Windows\System32\spool\PRINTERS |
| Stop spooler (Command Line) | net stop spooler |
| Clear spool files (Command Line) | del /Q /F /S "%systemroot%\System32\spool\PRINTERS\*.*" |
| Start spooler (Command Line) | net start spooler |
| Open classic Devices and Printers | Win + R > control printers |
| Open Settings Printers | Settings > Bluetooth & devices > Printers & scanners |

---

## Was this article helpful?

If this article helped resolve your issue, great. If something was unclear, missing, or did not work, please open a GitHub Issue describing the problem so we can improve it.

Suggest improvements at: https://github.com/EzioLockhart/Tier-1-Support-Knowledge-Base/issues

---

## References

- CompTIA A+ Troubleshooting Methodology: Identify the problem, Establish a theory, Test the theory, Establish a plan of action, Verify functionality, Document findings
- ITIL Incident Management best practices: Prioritize based on impact and urgency
- Microsoft official documentation: Fix printer problems in Windows

---

*Tier: Tier 1 (Help Desk) | Difficulty: L1 (Basic) | Estimated Resolution Time: 10-15 minutes | Required Access Level: Power User | Severity: P2 (Single User Degraded)*

---

For internal use. Follow your organization's escalation procedures.
