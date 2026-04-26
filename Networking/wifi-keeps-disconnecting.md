# Wi-Fi Keeps Disconnecting (Intermittent Wireless Drops)

**Category:** Networking  
**Last Updated:** April 26, 2026  
**Applies To:** Windows 10, Windows 11, Wi-Fi connected devices

---

## Symptoms

- Device disconnects from Wi-Fi randomly, sometimes reconnects automatically
- Network icon shows "No Internet" or disconnected icon briefly before reconnecting
- Video calls, streaming, or downloads interrupted frequently
- Other devices on the same network may or may not be affected
- Issue may occur at specific times or locations (e.g., far from router, during peak hours)

---

## Quick Checks (30 seconds)

1. Is the Wi-Fi signal strength indicator low? (fewer bars = weaker signal)
2. Does moving closer to the router improve stability?
3. Check if other devices in the same spot experience similar drops — if yes, likely a router/ISP issue
4. Quickly toggle Airplane Mode ON, wait 5 seconds, then OFF — forces a fresh connection
5. Verify no physical damage to the Wi-Fi adapter (USB dongle loose? Laptop switch accidentally off?)

---

## Step-by-Step Resolution

### Step 1: Forget and Reconnect to Wi-Fi Network

1. Go to **Settings** > **Network & Internet** > **Wi-Fi**
2. Click **"Manage known networks"**
3. Select the problematic Wi-Fi network
4. Click **"Forget"**
5. Click the Wi-Fi icon in the taskbar, select the network, enter password, and reconnect
   - This clears any saved network profile corruption.

### Step 2: Run Windows Network Troubleshooter

1. Right-click the network icon in the taskbar
2. Select **"Troubleshoot problems"**
3. Select **"Wi-Fi"** if prompted
4. Follow on-screen recommendations and apply any fixes

### Step 3: Disable Wi-Fi Power Management (Prevents Adapter Sleeping)

1. Press Win + X > **Device Manager**
2. Expand **"Network adapters"**
3. Right-click your **Wi-Fi adapter** (look for "Wireless", "WLAN", or brand name like Intel/Realtek)
4. Select **"Properties"**
5. Go to the **"Power Management"** tab
6. **Uncheck** the box: "Allow the computer to turn off this device to save power"
7. Go to the **"Advanced"** tab
8. Find **"Power Output"** or **"Transmit Power"** property, set value to **"Highest"** or **100%** if available
9. Click **OK** and restart the computer

### Step 4: Flush DNS and Reset Network Stack

1. Open **Command Prompt as Administrator** (Win + X > **Terminal (Admin)**)
2. Type the following commands one by one, pressing Enter after each:

ipconfig /flushdns
netsh int ip reset
netsh winsock reset
netsh wlan show profiles

3. Restart the computer
   - This resets all network settings to default, clearing any corrupt configurations.

### Step 5: Update or Rollback Wi-Fi Driver

1. Open **Device Manager** > **Network adapters**
2. Right-click your Wi-Fi adapter > **"Update driver"**
3. Select **"Search automatically for drivers"**
4. If Windows finds a new driver, install it and restart
5. If the issue started after a recent driver update, try **"Roll Back Driver"** instead (if the button is not greyed out)
   - A bad driver update is a common cause of Wi-Fi drops.

### Step 6: Change Wi-Fi Channel/Channel Width (Interference Reduction)

1. Open **Command Prompt** and type:

netsh wlan show networks mode=bssid

2. Identify your network's channel number and note neighbouring networks' channels
3. Access your router's admin page (usually 192.168.1.1 or 192.168.0.1) via a browser
4. Log in (credentials often on router sticker)
5. Go to **Wireless Settings** or **Wi-Fi Settings**
6. Change the **Channel** from "Auto" to a less congested channel (e.g., 1, 6, or 11 for 2.4 GHz; 36, 40, 44, 48 for 5 GHz)
7. Set **Channel Width** to 20 MHz (2.4 GHz) or 40/80 MHz (5 GHz) — narrower width reduces interference
8. Save and restart the router
   - This requires router admin access; escalate if you lack credentials.

### Step 7: Disable IPv6 (Temporary Fix)

1. Go to **Settings** > **Network & Internet** > **Advanced network settings** > **More network adapter options**
   - On Windows 10: Use Control Panel > Network and Sharing Center > Change adapter settings
2. Right-click your **Wi-Fi** connection > **Properties**
3. Uncheck **"Internet Protocol Version 6 (TCP/IPv6)"**
4. Click **OK** and restart
   - Some older routers or ISPs have IPv6 misconfigurations causing disconnects; this is a temporary workaround.

---

## Root Cause

Common causes of Wi-Fi disconnects, in order of likelihood:

- Power management putting the Wi-Fi adapter to sleep (most common on laptops)
- Corrupted network profile or DNS cache
- Outdated or buggy Wi-Fi driver
- Signal interference from neighboring Wi-Fi networks, Bluetooth devices, microwave ovens, or cordless phones
- Router firmware issues or channel congestion
- IPv6 incompatibility with the network
- Hardware fault in the Wi-Fi adapter or router

---

## Escalation Criteria

Escalate to Tier 2 / Network Team if:

- Issue persists across multiple devices in the same area (indicates router/AP problem)
- Driver updates and power management changes do not resolve the issue
- User is unable to change router settings (admin access needed)
- Frequent disconnections only on a specific band (2.4 GHz vs 5 GHz) suggest hardware defect
- The device drops Wi-Fi even when placed next to the router

---

## Commands Quick Reference

| Command | Purpose |
|---------|---------|
| ipconfig /flushdns | Clear DNS resolver cache |
| netsh int ip reset | Reset TCP/IP stack |
| netsh winsock reset | Reset Windows network socket settings |
| netsh wlan show profiles | List saved Wi-Fi networks |
| netsh wlan show networks mode=bssid | Show nearby Wi-Fi networks with their channels |
| ping -t 8.8.8.8 | Continuous ping to monitor connection stability |

---

For internal use. Follow your organization's escalation procedures.
