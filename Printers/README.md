# Printer Troubleshooting Guides

| Article | Description |
|---------|-------------|
| [Printer Shows as Offline](./printer-offline.md) | Printer status offline, Use Printer Offline setting, port configuration |
| [Print Jobs Stuck in Print Queue](./print-jobs-stuck.md) | Documents stuck, spooler service, queue clearing, driver issues |

---

## Printer Commands and Shortcuts Quick Reference

| Action | How To Access |
|--------|---------------|
| Open Services | Win + R > services.msc |
| Open spool folder | Win + R > C:\Windows\System32\spool\PRINTERS |
| Stop Print Spooler (command line) | Command Prompt (Admin): net stop spooler |
| Clear spool files (command line) | Command Prompt (Admin): del /Q /F /S "%systemroot%\System32\spool\PRINTERS\*.*" |
| Start Print Spooler (command line) | Command Prompt (Admin): net start spooler |
| Open classic Devices and Printers | Win + R > control printers |
| Open Settings Printers | Settings > Bluetooth & devices > Printers & scanners |
| Run Printer Troubleshooter | Settings > System > Troubleshoot > Other troubleshooters > Printer |
