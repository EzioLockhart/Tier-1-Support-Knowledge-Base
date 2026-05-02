# No Internet Access (Limited Connectivity)

**Category:** Networking
**Last Updated:** May 2, 2026
**Applies To:** Windows 10, Windows 11

---

## Symptoms

- Network icon in taskbar shows yellow triangle with exclamation mark
- Browser displays "No Internet" or "DNS_PROBE_FINISHED_NO_INTERNET"
- Apps requiring internet fail to connect
- Local network resources (printers, file shares) may still be accessible
- If internet disconnects repeatedly rather than being completely unavailable, see: [Wi-Fi Keeps Disconnecting](./wifi-keeps-disconnecting.md)

---

## Quick Checks (30 seconds)

1. Is the Ethernet cable firmly plugged in? (Wired connections)
2. Is Wi-Fi turned on? Check the physical switch or function key (Fn + F2/F3)
3. Is Airplane Mode off?
4. Try loading a different website (e.g., google.com vs github.com)

---

## Step-by-Step Resolution

### Step 1: Restart Network Equipment
1. Power off the computer
2. Unplug the modem and router power cables
3. Wait 60 seconds
4. Plug in the modem first; wait for all lights to stabilize (approx. 2 minutes)
5. Plug in the router; wait for it to fully boot (approx. 2 minutes)
6. Power on the computer and test connectivity

### Step 2: Run Windows Network Troubleshooter
1. Right-click the network icon in the taskbar
2. Select "Troubleshoot problems"
3. Follow on-screen prompts and apply any recommended fixes

### Step 3: Flush DNS and Renew IP (Command Line)
1. Open Command Prompt as Administrator:
   - Press Win + X, select "Terminal (Admin)" or "Command Prompt (Admin)"
2. Run the following commands in order, pressing Enter after each:
   ipconfig /release
   ipconfig /renew
   ipconfig /flushdns
   netsh winsock reset
3. Restart the computer and test connectivity

### Step 4: Check Proxy Settings
1. Open Settings > Network & Internet > Proxy
2. Ensure "Use a proxy server" is set to Off (unless corporate policy requires it)
3. Disable any VPN temporarily to isolate the issue

### Step 5: Update Network Driver
1. Press Win + X > Device Manager
2. Expand "Network adapters"
3. Right-click your Wi-Fi/Ethernet adapter > "Update driver"
4. Select "Search automatically for drivers"
5. Restart the computer after the update completes

### Step 6: Check IP Configuration
1. Open Command Prompt and type: ipconfig /all
2. Look for your network adapter and check:
   - IPv4 Address: Should start with 192.168.x.x, 10.x.x.x, or 172.16-31.x.x
   - Default Gateway: Should match your router's IP (usually 192.168.1.1 or 192.168.0.1)
   - DNS Servers: Should show valid addresses
3. If the IP address starts with 169.254.x.x, the computer failed to get an IP from DHCP — restart the router and computer
4. If no IP address is shown, the adapter may be disabled — right-click and enable it in Network Connections

### Step 7: Test Connectivity with Ping and Traceroute
1. Open Command Prompt
2. Test internet connectivity: ping 8.8.8.8
   - If successful, your internet connection is working and the problem may be DNS-related
3. Test DNS resolution: nslookup google.com
   - If this fails but ping to 8.8.8.8 works, you have a DNS problem — try changing DNS to 8.8.8.8 and 8.8.4.4 in network adapter properties
4. Trace the route to identify where the connection fails: tracert 8.8.8.8
   - Look for timeouts or long delays at specific hops to identify network bottlenecks

---

## Root Cause

Common causes include:
- Router/Modem needing a power cycle (most common)
- DNS cache corruption
- IP address conflict on the network
- Outdated or corrupted network drivers
- Incorrect proxy/VPN configuration
- DHCP server failure (computer not receiving valid IP)
- ISP outage in your area
- Firewall blocking internet access

---

## Escalation Criteria

Escalate to Tier 2 / Network Team if:
- The issue affects multiple users simultaneously
- Pinging 8.8.8.8 fails (indicates hardware or ISP issue)
- The above steps do not resolve the issue
- The user requires administrative access to network equipment
- ISP outage is confirmed requiring provider contact
- Network adapter shows "Code 10" or other error in Device Manager

---

## Commands Quick Reference

| Command | Purpose |
|---------|---------|
| ipconfig /release | Release current IP address |
| ipconfig /renew | Request new IP address |
| ipconfig /flushdns | Clear DNS resolver cache |
| netsh winsock reset | Reset Windows network stack |
| ipconfig /all | Display full IP configuration |
| ping 8.8.8.8 | Test internet connectivity |
| nslookup google.com | Test DNS resolution |
| tracert 8.8.8.8 | Trace route to destination |

---

For internal use. Follow your organization's escalation procedures.
