# Wi-Fi Keeps Disconnecting (Intermittent Wireless Drops)

- **Category:** Networking
- **Version:** 1.0
- **Last Updated:** May 2, 2026
- **Last Reviewed:** May 2, 2026
- **Applies To:** Windows 10 (22H2), Windows 11 (23H2)
- **Difficulty:** L2 (Intermediate)
- **Estimated Resolution Time:** 15-30 minutes
- **Required Access Level:** Power User
- **Severity:** P2 (Single User, Degraded — Intermittent Connectivity)
- **Keywords:** Wi-Fi, wireless, disconnect, intermittent, signal, adapter, power management, driver, channel, interference
- **Prerequisite Knowledge:** Basic Windows navigation, ability to open Device Manager and Command Prompt

---

## Symptoms

- Device disconnects from Wi-Fi randomly, sometimes reconnects automatically
- Network icon shows "No Internet" or disconnected icon briefly before reconnecting
- Video calls, streaming, or downloads interrupted frequently
- Other devices on the same network may or may not be affected
- Issue may occur at specific times or locations (e.g., far from router, during peak hours)

---

## Common Error Codes

| Code | Meaning |
|------|---------|
| DNS_PROBE_FINISHED_NO_INTERNET | DNS resolution failure after Wi-Fi drop |
| ERR_NETWORK_CHANGED | Network change detected during disconnection |
| ERR_INTERNET_DISCONNECTED | Complete loss of internet during Wi-Fi drop |
| EVENT ID 8002 | Wi-Fi adapter reported disconnection in system log |

---

## Symptom-to-Step Mapping

| If You See This | Skip To |
|-----------------|---------|
| Wi-Fi disconnects when laptop is on battery | Step 3 |
| Wi-Fi drops every few minutes consistently | Step 4 |
| Signal strength is weak (1-2 bars) | Step 6 |
| Issue started after Windows Update | Step 5 |
| Other devices on same network also disconnect | Step 6 (router), then escalate |

---

## Triage Questions

Before starting troubleshooting, ask the user:

1. "Does the Wi-Fi disconnect when you're close to the router, far away, or both?"
2. "Do other devices in your home or office have the same problem on the same Wi-Fi network?"
3. "When did this start happening, and did you install any updates or new software around that time?"
4. "Are you using a laptop on battery power when this happens, or plugged in?"

---

## Quick Checks (30 seconds)

1. Is the Wi-Fi signal strength indicator low? (fewer bars = weaker signal)
2. Does moving closer to the router improve stability?
3. Check if other devices in the same spot experience similar drops — if yes, likely a router or ISP issue
4. Quickly toggle Airplane Mode ON, wait 5 seconds, then OFF — forces a fresh connection
5. Verify no physical damage to the Wi-Fi adapter (USB dongle loose? Laptop switch accidentally off?)
6. If there is no internet access at all (not intermittent drops), see: [No Internet Access (Limited Connectivity)](./no-internet-access.md)

---

## Step-by-Step Resolution

### Step 1: Forget and Reconnect to Wi-Fi Network
1. Go to Settings > Network & Internet > Wi-Fi
2. Click "Manage known networks"
3. Select the problematic Wi-Fi network
4. Click "Forget"
5. Click the Wi-Fi icon in the taskbar, select the network, enter password, and reconnect

**What to tell the user:** "We're going to remove your saved Wi-Fi network and reconnect fresh. This clears any corrupted settings tied to that network. You'll need your Wi-Fi password ready."

### Step 2: Run Windows Network Troubleshooter
1. Right-click the network icon in the taskbar
2. Select "Troubleshoot problems"
3. Select "Wi-Fi" if prompted
4. Follow on-screen recommendations and apply any fixes

**What to tell the user:** "Windows has a built-in diagnostic tool specifically for Wi-Fi. Let's run it now — it checks for common issues and may apply a fix automatically."

### Step 3: Disable Wi-Fi Power Management
1. Press Win + X > Device Manager
2. Expand "Network adapters"
3. Right-click your Wi-Fi adapter (look for "Wireless", "WLAN", or brand name like Intel or Realtek)
4. Select "Properties"
5. Go to the "Power Management" tab
6. Uncheck the box: "Allow the computer to turn off this device to save power"
7. Go to the "Advanced" tab
8. Find "Power Output" or "Transmit Power" property, set value to "Highest" or 100% if available
9. Click OK and restart the computer

**What to tell the user:** "Your computer may be turning off the Wi-Fi adapter to save battery. We're going to disable that power-saving feature so your Wi-Fi stays on all the time. This is the most common fix for laptops dropping Wi-Fi."

### Step 4: Flush DNS and Reset Network Stack
1. Open Command Prompt as Administrator: Press Win + X > Terminal (Admin)
2. Run the following commands one by one, pressing Enter after each:
   ipconfig /flushdns
   netsh int ip reset
   netsh winsock reset
   netsh wlan show profiles
3. Restart the computer

**What to tell the user:** "These commands reset all your network settings back to default. This clears any corrupt configurations that might be causing the drops. It won't delete your saved Wi-Fi passwords."

### Step 5: Update or Rollback Wi-Fi Driver
1. Open Device Manager > Network adapters
2. Right-click your Wi-Fi adapter > "Update driver"
3. Select "Search automatically for drivers"
4. If Windows finds a new driver, install it and restart
5. If the issue started after a recent driver update, try "Roll Back Driver" instead (if the button is not greyed out)

**What to tell the user:** "A bad or outdated Wi-Fi driver is a very common cause of disconnections. We'll check if there's a newer driver available, or if a recent update caused the problem, we can roll it back."

### Step 6: Change Wi-Fi Channel and Reduce Interference
1. Open Command Prompt and type: netsh wlan show networks mode=bssid
2. Identify your network's channel number and note neighbouring networks' channels
3. Access your router's admin page (usually 192.168.1.1 or 192.168.0.1) via a browser
4. Log in (credentials often on router sticker)
5. Go to Wireless Settings or Wi-Fi Settings
6. Change the Channel from "Auto" to a less congested channel:
   - For 2.4 GHz: Channels 1, 6, or 11 (non-overlapping)
   - For 5 GHz: Channels 36, 40, 44, or 48
7. Set Channel Width to 20 MHz (2.4 GHz) or 40/80 MHz (5 GHz)
8. Save and restart the router

**What to tell the user:** "Your Wi-Fi might be competing with nearby networks on the same channel. Think of it like too many people trying to talk on the same radio frequency. We're going to switch to a less crowded channel. You'll need your router login credentials."

### Step 7: Disable IPv6 Temporarily
1. Go to Settings > Network & Internet > Advanced network settings > More network adapter options
2. On Windows 10: Use Control Panel > Network and Sharing Center > Change adapter settings
3. Right-click your Wi-Fi connection > Properties
4. Uncheck "Internet Protocol Version 6 (TCP/IPv6)"
5. Click OK and restart

**What to tell the user:** "Some older routers or ISPs have compatibility issues with IPv6. We're going to temporarily disable it as a test. If this fixes the problem, we'll know the router or ISP needs an update. This is safe to leave disabled."

---

## Alternative Solutions

If the above steps do not resolve the issue, also try:

- Connecting to the 5 GHz band instead of 2.4 GHz (if your router supports both) — 5 GHz has less interference but shorter range
- Using a USB Wi-Fi adapter as a replacement if the built-in adapter is faulty
- Updating your router's firmware from the manufacturer's website
- Changing the Wi-Fi security type in router settings (e.g., WPA2-PSK AES instead of WPA/WPA2 mixed mode)

---

## Prevention Tips

- Position your router in a central, elevated location away from walls and metal objects
- Keep your Wi-Fi adapter drivers updated through Windows Update
- Avoid placing the router near microwave ovens, cordless phones, baby monitors, or Bluetooth devices
- Restart your router once a month to clear memory and refresh connections
- If your router is more than 5 years old, consider upgrading to a newer model with better range and stability

---

## Root Cause

Common causes of Wi-Fi disconnections, in order of likelihood:

- Power management putting the Wi-Fi adapter to sleep to save battery (most common on laptops)
- Corrupted network profile or DNS cache on the computer
- Outdated or buggy Wi-Fi adapter driver
- Signal interference from neighboring Wi-Fi networks on the same channel
- Router firmware issues or channel congestion
- IPv6 incompatibility with the router or ISP
- Physical distance from router or obstacles blocking the signal
- Hardware fault in the Wi-Fi adapter or router

---

## Escalation Decision Matrix

| Condition | Action |
|-----------|--------|
| All 7 steps completed, issue persists | Escalate to Tier 2 |
| Issue affects multiple devices in the same location | Escalate — likely router or access point problem |
| User unable to access router admin page (no credentials) | Escalate if channel change is required |
| Frequent disconnections only on one specific band (2.4 vs 5 GHz) | Escalate — possible hardware defect |
| Device drops Wi-Fi even when placed next to the router | Escalate — likely adapter hardware failure |
| Driver rollback not available and update doesn't fix it | Escalate — may need manufacturer-specific driver |
| Single user, single device, steps partially resolve | Continue troubleshooting, try Alternative Solutions |

---

## Related Articles

- [No Internet Access (Limited Connectivity)](./no-internet-access.md) — If there is no internet at all, not intermittent drops
- [DNS Server Not Responding](./dns-server-not-responding.md) — If connected but websites fail to load by name

---

## FAQ

**Q: Why does my Wi-Fi only drop when I'm on battery power?**
**A:** This is almost certainly the Wi-Fi Power Management setting covered in Step 3. Windows tries to save battery by turning off the Wi-Fi adapter when it thinks it's not in use. Disabling this setting prevents that behavior.

**Q: How do I know if the problem is my computer or my router?**
**A:** Check if other devices (phone, tablet, another computer) also disconnect from the same Wi-Fi network. If they do, the problem is the router or ISP. If only your computer drops, the problem is with your computer's Wi-Fi adapter or settings.

**Q: Will changing my router channel affect other devices?**
**A:** No. All your devices will automatically follow the new channel. The change is seamless — they will reconnect on the new channel without you having to do anything on each device.

---

## Commands Quick Reference

| Command | Purpose |
|---------|---------|
| ipconfig /flushdns | Clear local DNS resolver cache |
| netsh int ip reset | Reset TCP/IP stack to defaults |
| netsh winsock reset | Reset Windows network socket settings |
| netsh wlan show profiles | List all saved Wi-Fi networks |
| netsh wlan show networks mode=bssid | Show nearby Wi-Fi networks with channel details |
| ping -t 8.8.8.8 | Continuous ping to monitor connection stability |

---

## Was this article helpful?

If this article helped resolve your issue, great. If something was unclear, missing, or did not work, please open a GitHub Issue describing the problem so we can improve it.

Suggest improvements at: https://github.com/EzioLockhart/Tier-1-Support-Knowledge-Base/issues

---

## References

- CompTIA A+ Troubleshooting Methodology: Identify the problem, Establish a theory, Test the theory, Establish a plan of action, Verify functionality, Document findings
- ITIL Incident Management best practices: Prioritize based on impact and urgency
- Microsoft official documentation: Fix Wi-Fi connection issues in Windows

---

*Difficulty: L2 (Intermediate) | Estimated Resolution Time: 15-30 minutes | Required Access Level: Power User | Severity: P2 (Single User Degraded)*

---

For internal use. Follow your organization's escalation procedures.
