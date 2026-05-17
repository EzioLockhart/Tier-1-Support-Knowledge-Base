# Operating System Troubleshooting Guides

| Article | Description |
|---------|-------------|
| [Windows Update Stuck or Fails to Install](./windows-update-stuck.md) | Update hangs, error codes, SoftwareDistribution reset, DISM, SFC |
| [Slow Boot Time and Performance](./slow-boot-performance.md) | Long boot, sluggish system, startup programs, disk cleanup, disk health |

---

## System Diagnostic Commands Quick Reference

| Command | Description |
|---------|-------------|
| `sfc /scannow` | Scan and repair system files |
| `DISM /Online /Cleanup-Image /RestoreHealth` | Repair Windows system image |
| `chkdsk C: /f /r` | Check and repair disk errors |
| `wmic diskdrive get model, status` | Check disk SMART health status |
| `fsutil behavior query DisableDeleteNotify` | Check SSD TRIM status |
| `msconfig` | System Configuration (clean boot, startup) |
| `sysdm.cpl` | System Properties (performance settings) |
| `perfmon` | Performance Monitor |
| `eventvwr.msc` | Event Viewer |

## Shortcuts

| Action | How To Access |
|--------|---------------|
| Task Manager | Ctrl + Shift + Esc |
| System Configuration | Win + R > msconfig |
| Disk Cleanup (as admin) | Start menu > Disk Cleanup > Run as administrator |
| Storage settings | Settings > System > Storage |
| Windows Update | Settings > Windows Update |
| Windows Security | Settings > Privacy & Security > Windows Security |
