# No Internet Access (Limited Connectivity)

- **Category:** Networking
- **Version:** 1.0
- **Last Updated:** May 2, 2026
- **Last Reviewed:** May 2, 2026
- **Applies To:** Windows 10 (22H2), Windows 11 (23H2)
- **Difficulty:** L1 (Basic)
- **Estimated Resolution Time:** 10-20 minutes
- **Required Access Level:** User
- **Severity:** P1 (Single User, Critical — No Connectivity)
- **Keywords:** no internet, limited connectivity, yellow triangle, DNS, ipconfig, network, Wi-Fi, Ethernet, connectivity
- **Prerequisite Knowledge:** Basic Windows navigation, ability to open Settings and Command Prompt

---

## Symptoms

- Network icon in taskbar shows yellow triangle with exclamation mark
- Browser displays "No Internet" or "DNS_PROBE_FINISHED_NO_INTERNET"
- Apps requiring internet fail to connect
- Local network resources (printers, file shares) may still be accessible

---

## Common Error Codes

| Code | Meaning |
|------|---------|
| DNS_PROBE_FINISHED_NO_INTERNET | DNS resolution failure — computer cannot reach DNS server |
| ERR_INTERNET_DISCONNECTED | No network connection detected at all |
| ERR_NETWORK_CHANGED | Network change detected, connection interrupted |
| ERR_CONNECTION_RESET | Connection was forcibly closed by the remote host |

---

## Symptom-to-Step Mapping

| If You See This | Skip To |
|-----------------|---------|
| Red X on network icon | Step 1 |
| Yellow triangle on network icon | Step 2 |
| Connected but no websites load | Step 3 |
| IP address starts with 169.254.x.x | Step 6 |
| ping 8.8.8.8 fails completely | Step 7, then escalate |

---

## Triage Questions

Before starting troubleshooting, ask the user:

1. "Can you tell me exactly what you see on the network icon in the bottom-right corner of your screen?"
2. "Are other devices in your home or office able to connect to the internet right now?"
3. "When did this problem start, and did anything change just before it happened?"
4. "Is this a wired connection with a cable, or are you using Wi-Fi?"

---

## Quick Checks (30 seconds)

1. Is the Ethernet cable firmly plugged in? (Wired connections)
2. Is Wi-Fi turned on? Check the physical switch or function key (Fn + F2/F3)
3. Is Airplane Mode off?
4. Try loading a different website (e.g., google.com vs github.com)
5. If internet disconnects repeatedly rather than being completely unavailable, see: [Wi-Fi Keeps Disconnecting](./wifi-keeps-disconnecting.md)

---

## Step-by-Step Resolution

### Step 1: Restart Network Equipment
1. Power off the computer
2. Unplug the modem and router power cables
3. Wait 60 seconds
4. Plug in the modem first; wait for all lights to stabilize (approximately 2 minutes)
5. Plug in the router; wait for it to fully boot (approximately 2 minutes)
6. Power on the computer and test connectivity

**What to tell the user:** "We're going to restart your network equipment. This clears any temporary issues and forces a fresh connection from your ISP. You'll be offline for about 5 minutes while everything powers back up."

### Step 2: Run Windows Network Troubleshooter
1. Right-click the network icon in the taskbar
2. Select "Troubleshoot problems"
3. Follow on-screen prompts and apply any recommended fixes

**What to tell the user:** "Windows has a built-in repair tool. I'll walk you through running it now. It checks for common issues automatically and may fix the problem on its own."

### Step 3: Flush DNS and Renew IP
1. Open Command Prompt as Administrator: Press Win + X, select "Terminal (Admin)" or "Command Prompt (Admin)"
2. Run the following commands in order, pressing Enter after each:
   ipconfig /release
   ipconfig /renew
   ipconfig /flushdns
   netsh winsock reset
3. Restart the computer and test connectivity

**What to tell the user:** "These commands clear out old network settings and force your computer to request a fresh connection. It's safe and won't delete any of your files or saved Wi-Fi passwords."

### Step 4: Check Proxy Settings
1. Open Settings > Network & Internet > Proxy
2. Ensure "Use a proxy server" is set to Off (unless corporate policy requires it)
3. Disable any VPN temporarily to isolate the issue

### Step 5: Update Network Driver
1. Press Win + X > Device Manager
2. Expand "Network adapters"
3. Right-click your Wi-Fi or Ethernet adapter > "Update driver"
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
3. Test DNS resolution: nslookup google.com
4. Trace the route to identify where the connection fails: tracert 8.8.8.8
5. If ping to 8.8.8.8 fails completely, the issue is likely hardware or ISP-related

**What to tell the user:** "We've completed all the standard fixes on your computer. If you're still not online, the problem is likely with your internet service provider. I'll escalate this to our network team who can contact your ISP or check for wider outages."

---

## Alternative Solutions

If the above steps do not resolve the issue, also try:

- Connecting via mobile phone hotspot to isolate whether the problem is with your ISP or your computer
- Using a USB-to-Ethernet adapter if the built-in network port is suspected faulty
- Performing a full Network Reset: Settings > Network & Internet > Advanced network settings > Network Reset (note: this removes all saved Wi-Fi networks)
- Booting into Safe Mode with Networking to rule out third-party software interference

---

## Prevention Tips

- Restart your router and modem once a month to clear memory and prevent DNS cache buildup
- Keep network drivers updated through Windows Update regularly
- Avoid placing your router near microwave ovens, cordless phones, baby monitors, or large metal objects
- Use a surge protector for your network equipment to prevent damage from power fluctuations
- Save your ISP's support phone number in your contacts for quick access during outages

---

## Root Cause

Common causes in order of likelihood:

- Router or modem needing a power cycle (most common — temporary memory or connection issues)
- DNS cache corruption on the local computer
- IP address conflict on the network
- Outdated or corrupted network adapter drivers
- Incorrect proxy or VPN configuration
- DHCP server failure (computer not receiving a valid IP address)
- ISP outage in your area
- Firewall or security software blocking internet access

---

## Escalation Decision Matrix

| Condition | Action |
|-----------|--------|
| All 7 steps completed, issue persists | Escalate to Tier 2 |
| ping 8.8.8.8 fails from multiple devices on same network | Escalate — likely ISP or router hardware issue |
| Issue affects multiple users in same location simultaneously | Escalate — likely network infrastructure issue |
| User requires access to router admin page but lacks credentials | Escalate if router config change is required |
| Network adapter shows "Code 10" or "Code 43" in Device Manager | Escalate — likely hardware fault |
| ISP outage confirmed via downdetector or ISP status page | Escalate — requires ISP contact |
| Single user, no other devices affected | Continue troubleshooting, do not escalate yet |

---

## Related Articles

- [Wi-Fi Keeps Disconnecting](./wifi-keeps-disconnecting.md) — If internet drops repeatedly rather than being completely unavailable
- [DNS Server Not Responding](./dns-server-not-responding.md) — If connected but websites fail to load by name

---

## FAQ

**Q: Will resetting my network stack delete my saved Wi-Fi passwords?**
**A:** No. Saved Wi-Fi passwords are stored separately in Windows Credential Manager and are not affected by netsh or ipconfig commands. However, a full Network Reset will remove saved networks.

**Q: How do I know if my ISP is down and not my computer?**
**A:** Check downdetector.com or your ISP's official status page from a mobile device on cellular data. If other devices in your home on the same network also cannot connect, it is very likely an ISP outage.

**Q: Why does restarting the router and modem fix so many problems?**
**A:** Routers and modems are small computers that run continuously. Over time, their memory can fill up, their internal IP tables can get corrupted, or they can lose sync with the ISP. A restart clears all of this and forces a clean reconnection.

---

## Commands Quick Reference

| Command | Purpose |
|---------|---------|
| ipconfig /release | Release current IP address |
| ipconfig /renew | Request new IP address from DHCP |
| ipconfig /flushdns | Clear local DNS resolver cache |
| netsh winsock reset | Reset Windows network socket settings |
| ipconfig /all | Display full IP configuration for all adapters |
| ping 8.8.8.8 | Test basic internet connectivity (bypasses DNS) |
| nslookup google.com | Test DNS resolution for a domain name |
| tracert 8.8.8.8 | Trace network path to identify failure point |

---

## Was this article helpful?

If this article helped resolve your issue, great. If something was unclear, missing, or did not work, please open a GitHub Issue describing the problem so we can improve it.

Suggest improvements at: https://github.com/EzioLockhart/Tier-1-Support-Knowledge-Base/issues

---

## References

- CompTIA A+ Troubleshooting Methodology: Identify the problem, Establish a theory, Test the theory, Establish a plan of action, Verify functionality, Document findings
- ITIL Incident Management best practices: Prioritize based on impact and urgency
- Microsoft official documentation: Fix network connection issues in Windows

---

*Difficulty: L1 (Basic) | Estimated Resolution Time: 10-20 minutes | Required Access Level: User | Severity: P1 (Single User Critical)*

---

For internal use. Follow your organization's escalation procedures.
