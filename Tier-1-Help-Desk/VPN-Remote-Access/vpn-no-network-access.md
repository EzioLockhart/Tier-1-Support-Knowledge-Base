# VPN Connected but No Network Access

- **Category:** VPN & Remote Access
- **Tier:** Tier 1 (Help Desk)
- **Version:** 1.0
- **Last Updated:** May 2, 2026
- **Last Reviewed:** May 2, 2026
- **Applies To:** Windows 10 (22H2), Windows 11 (23H2), All VPN Clients (Cisco AnyConnect, FortiClient, Pulse Secure, GlobalProtect, OpenVPN, Windows Built-in VPN)
- **Difficulty:** L2 (Intermediate)
- **Estimated Resolution Time:** 15-25 minutes
- **Required Access Level:** Power User
- **Severity:** P1 (Single User, Critical — Connected but No Corporate Access)
- **Keywords:** VPN, connected, no access, no network, DNS, split tunnel, proxy, MTU, routing, internal resources
- **Prerequisite Knowledge:** Basic Windows navigation, ability to open Command Prompt and network settings

---

## Symptoms

- VPN client shows "Connected" or green status but no network resources are accessible
- Cannot access internal company websites, intranet, or SharePoint
- Mapped network drives do not connect or show red X
- Remote Desktop (RDP) connections to internal servers fail with "Cannot connect" or timeout error
- Internet access works normally (or stops entirely, depending on VPN configuration)
- Ping to internal servers by IP address or hostname fails with "Request timed out"
- VPN connection time is counting up but zero data is being sent or received

---

## Common Error Codes

| Code | Meaning |
|------|---------|
| 0x80072741 | No route to host — VPN routing table missing internal network routes |
| 0x8007274C | Connection attempt failed — VPN adapter not receiving data |
| Error 720 | No PPP control protocols configured — VPN adapter configuration issue |
| Event ID 20227 | VPN connection established but no data flowing — routing or DNS issue |

---

## Symptom-to-Step Mapping

| If You See This | Skip To |
|-----------------|---------|
| Can ping internal IP but not hostname | Step 2 |
| No internet access after VPN connects | Step 4 |
| Mapped drives not connecting | Step 5 |
| Some internal sites work, others don't | Step 6 |
| VPN connected but zero bytes sent/received | Step 1 |

---

## Triage Questions

Before starting troubleshooting, ask the user:

1. "Can you access anything internal at all, or is everything completely unreachable?"
2. "Is your internet access still working after connecting to the VPN, or did it stop?"
3. "Can you ping an internal server by its IP address? Try 10.x.x.x or 192.168.x.x."
4. "Are you connecting from home, a hotel, a coffee shop, or somewhere else?"

---

## Quick Checks (30 seconds)

1. Verify the VPN client actually shows "Connected" — if it is still "Connecting" or "Authenticating", the connection is not fully established
2. Try accessing a resource by IP address instead of hostname (e.g., \\192.168.1.50 instead of \\fileserver) — if IP works but hostname does not, the problem is DNS
3. Check if you can access any internal resources at all, or if all internal access is blocked — helps narrow down the scope
4. Open a web browser and try loading an external website — if the internet also does not work, the VPN may be routing all traffic incorrectly
5. Disconnect the VPN, wait 30 seconds, and reconnect — a simple reconnect often resolves temporary routing issues
6. If VPN fails to connect at all with an authentication error, see: [VPN Connection Fails with Authentication Error](./vpn-authentication-error.md)

---

## Step-by-Step Resolution

### Step 1: Verify VPN Connection Details and Status
1. Check the VPN client for actual connection details, not just the "Connected" indicator:
   - Look for "Bytes Sent" and "Bytes Received" — if both show 0 after several minutes, no traffic is flowing
   - Check the connection duration timer is counting up
   - Look for the assigned virtual IP address (VPN IP) — if missing or showing 0.0.0.0, the VPN did not receive a valid IP configuration
2. Open Command Prompt and check your network configuration: ipconfig /all
3. Look for the VPN adapter in the output — it may be named after your VPN client
4. Verify the VPN adapter has:
   - A valid IP address (not 0.0.0.0 or 169.254.x.x, which is an APIPA auto-configuration failure address)
   - A subnet mask
   - DNS server addresses (usually the company's internal DNS servers)
   - Default gateway (may or may not be present depending on VPN configuration)
5. If the VPN adapter shows no IP address or an APIPA address (169.254.x.x), disconnect and reconnect to obtain a new IP lease

**What to tell the user:** "Your VPN shows as connected, but it might not have received a valid network configuration from the server. It's like having a phone call where you can hear the line is open but no one is speaking. We need to check if your VPN actually got an IP address and network settings."

### Step 2: Flush DNS and Reset Network Stack
1. After connecting to VPN, the local DNS cache may still contain old entries that do not resolve through the VPN tunnel
2. Open Command Prompt as Administrator: Win + X > Terminal (Admin)
3. Run the following commands one at a time, pressing Enter after each:
   ipconfig /flushdns
   ipconfig /registerdns
   netsh int ip reset
   netsh winsock reset
4. Wait for each command to complete before running the next
5. Restart the computer after running all commands
6. After restart, connect to the VPN first, then test access to internal resources

**What to tell the user:** "Your computer keeps a local DNS cache — a phonebook of website addresses. When you connect to VPN, that old phonebook may still point to the wrong places. We're going to clear it completely and force your computer to use the VPN's DNS servers for internal addresses."

### Step 3: Check Network Profile and Firewall Settings
1. When connected to VPN, Windows may classify the VPN connection as a "Public" network, which enables stricter firewall rules
2. Check the network profile:
   - Open Settings > Network & Internet
   - Look for your VPN connection in the network list
   - Check if it says "Public network" or "Private network"
3. If set to Public, change it to Private:
   - Windows 11: Click on the VPN connection > "Properties" > Under Network profile type, select "Private network"
   - Windows 10: Click on the VPN connection > Under Network profile, select "Private"
4. Temporarily disable Windows Firewall to test:
   - Settings > Privacy & Security > Windows Security > Firewall & network protection
   - Select the active network profile > Turn off "Microsoft Defender Firewall"
   - Test access to internal resources
   - Turn the firewall back on immediately after testing
5. If disabling the firewall resolves the issue, add a firewall exception for the VPN client

**What to tell the user:** "Windows treats new networks as 'Public' by default, which blocks many types of connections for security. Your VPN connection might be classified as Public, and Windows is blocking access to your company's internal resources. We're going to change it to Private, which trusts the network more."

### Step 4: Check Split Tunneling Configuration
1. Split tunneling determines whether only company traffic goes through the VPN (split tunnel) or all internet traffic goes through the VPN (full tunnel)
2. With split tunneling:
   - Internal company resources should be accessible through the VPN
   - Internet traffic (Google, YouTube) goes through your regular internet connection
3. With full tunneling:
   - All traffic, both internal and internet, goes through the VPN
   - If the internet also does not work, the VPN server's routing may be down
4. To check your routing, open Command Prompt and type: route print
5. Look at the routing table — the VPN adapter should have routes to your company's internal IP ranges (e.g., 10.x.x.x, 172.16.x.x, 192.168.x.x)
6. If no internal routes are listed, the VPN did not push the correct routing configuration
7. You cannot change split tunneling from your end — this is a server-side setting

**What to tell the user:** "Your organization may use split tunneling, where only work traffic goes through the VPN. If the routing rules aren't set up correctly, your computer doesn't know which traffic to send through the VPN tunnel. This is a server-side issue, but understanding it helps us know when to escalate."

### Step 5: Check Proxy Server Settings
1. Many organizations require a specific proxy server configuration to access internal resources after connecting to VPN
2. Check current proxy settings:
   - Settings > Network & Internet > Proxy
   - Look at "Manual proxy setup" — is a proxy server configured?
   - Check "Automatically detect settings" is enabled if your organization uses automatic proxy detection (WPAD)
3. If a proxy is required but not configured:
   - Enter the proxy server address and port provided by your IT department
   - Check "Don't use the proxy server for local (intranet) addresses" if instructed
4. If the proxy is configured but internal resources still do not load:
   - Try disabling the proxy temporarily to test direct access
   - If direct access works, the proxy server or its configuration is the problem
5. Proxy settings may also be configured via Group Policy and cannot be changed locally

**What to tell the user:** "Your company might use a proxy server for internal web access. Without the correct proxy settings, your browser won't know how to reach internal websites even though the VPN is connected. We're going to verify your proxy configuration."

### Step 6: Adjust MTU (Maximum Transmission Unit) Size
1. MTU mismatch can cause some or all network traffic to fail over VPN
2. The VPN adds encryption overhead to each network packet, which can exceed the maximum packet size allowed
3. Test for MTU issues:
   - Open Command Prompt and type: ping [internal server IP] -f -l 1472
   - Replace [internal server IP] with an actual internal server IP address
   - The -f flag sets "Don't Fragment" and -l 1472 sets the packet size
   - If you get "Packet needs to be fragmented but DF set", the packet is too large
4. Reduce the packet size by 10 and test again: ping [internal server IP] -f -l 1400
5. Continue reducing until the ping succeeds — the highest successful value plus 28 (for headers) is your maximum MTU
6. To set a lower MTU on the VPN adapter:
   - Open Command Prompt as Administrator
   - Identify your VPN adapter name from ipconfig
   - Set the MTU: netsh interface ipv4 set subinterface "VPN Adapter Name" mtu=1400 store=persistent
7. Disconnect and reconnect the VPN, then test access to internal resources

**What to tell the user:** "The VPN adds a security wrapper around your data, which makes each packet slightly larger. If your internet connection has a size limit that these enlarged packets exceed, they get dropped silently. We're going to test and adjust the packet size to find the sweet spot."

### Step 7: Reinstall or Update the VPN Client
1. A corrupted VPN client or outdated virtual network adapter driver can cause a false "Connected" state with no actual data flow
2. Check if there is a newer version of the VPN client available from your organization's software portal or the vendor's website
3. If an update is available, download and install it
4. If already on the latest version, perform a clean reinstall:
   - Disconnect the VPN
   - Uninstall the VPN client from Settings > Apps > Installed apps
   - Restart the computer
   - Check for and delete leftover VPN adapter entries in Device Manager under "Network adapters"
   - Restart the computer again
   - Reinstall the VPN client using the latest installer
   - Restart one final time, then connect and test

**What to tell the user:** "The VPN client creates a virtual network adapter on your computer. If that virtual adapter or the client software is corrupted, it can show as connected while passing no data. We're going to completely remove and reinstall the VPN client for a clean start."

---

## Alternative Solutions

If the above steps do not resolve the issue, also try:

- Connecting from a different network (e.g., mobile hotspot) to rule out home network configuration issues
- Temporarily disabling IPv6 on your network adapter, as IPv6 routing conflicts can prevent IPv4 VPN traffic
- Checking if another VPN client or virtual adapter from a previous installation is conflicting
- Using the VPN's built-in diagnostic or log collection tool to analyze connection details

---

## Prevention Tips

- Keep your VPN client updated to the latest version provided by your organization
- After connecting to VPN, always test access to a known internal resource before starting work
- Note your organization's internal DNS server addresses for manual testing when needed
- Restart your home router periodically to prevent routing table issues that can interfere with VPN
- Save your IT helpdesk contact for quick escalation when VPN routing issues occur

---

## Root Cause

Common causes of VPN connected but no network access, in order of likelihood:

- DNS cache not updated after VPN connection (resolved by flushing DNS) — most common
- Windows Firewall treating the VPN connection as a Public network and blocking resource access
- Split tunneling misconfiguration — internal routes not properly pushed to the client
- Missing or incorrect proxy server configuration for internal resource access
- MTU size too large causing packet fragmentation and silent data loss
- VPN virtual network adapter driver corrupted or outdated
- VPN server-side issue — routing, DHCP pool exhausted, or server overload
- Conflicting network configuration from another VPN client or virtual adapter still installed

---

## Escalation Decision Matrix

| Condition | Action |
|-----------|--------|
| All 7 steps completed, issue persists | Escalate to Tier 2 |
| Multiple users cannot access internal resources after connecting | Escalate — likely server-side issue |
| Routes to internal networks are missing from the route table | Escalate — server-side routing configuration |
| VPN adapter receives no IP address or APIPA address after multiple reconnects | Escalate — DHCP pool may be exhausted |
| Split tunneling or full tunnel configuration needs to be changed | Escalate — server-side setting |
| Proxy configuration is managed by Group Policy and requires changes | Escalate — requires admin modification |
| Internal DNS servers are unreachable from the VPN subnet | Escalate — server-side DNS issue |

---

## Related Articles

- [VPN Connection Fails with Authentication Error](./vpn-authentication-error.md) — If VPN fails to connect at all with login errors
- [VPN Connection Tips — Self-Service Guide](../Tier-0-Self-Service/vpn-connection-tips.md) — Tier 0: Self-service guide for users
- [Firewall Rule & VPN Gateway Configuration Analysis](../Tier-2-Technical-Support/firewall-vpn-gateway.md) — Tier 2: Advanced VPN diagnostics
- [VPN Split Tunnel Architecture & Routing Design](../Tier-3-Expert-Engineering/vpn-split-tunnel-architecture.md) — Tier 3: VPN architecture analysis

> **Note:** If you are looking for the Tier 0 self-service version of this article, see: [VPN Connection Tips — Self-Service Guide](../Tier-0-Self-Service/vpn-connection-tips.md) (to be created if not yet present).

---

## FAQ

**Q: Why can I ping an internal server by IP but not by hostname?**
**A:** This is a DNS issue. Your VPN assigned you internal DNS servers, but your computer is still using your home router's DNS. Flush your DNS cache (Step 2) to force your computer to use the VPN's DNS servers for internal hostnames.

**Q: Why does my internet stop working when I connect to the VPN?**
**A:** Your organization likely uses full tunneling — routing all traffic through the corporate network. If the corporate internet gateway is slow or down, your internet will stop working. Check with your IT department if split tunneling is available as an alternative.

**Q: What does "Packet needs to be fragmented but DF set" mean?**
**A:** It means a data packet is too large for your network path, and it's not allowed to be split into smaller pieces. This is a classic MTU issue (Step 6). Reducing the MTU size on your VPN adapter usually solves it.

---

## Commands and Shortcuts Quick Reference

| Action | How To Access |
|--------|---------------|
| Check IP configuration | Command Prompt: ipconfig /all |
| Flush DNS | Command Prompt (Admin): ipconfig /flushdns |
| Show routing table | Command Prompt: route print |
| Test MTU with ping | Command Prompt: ping [IP] -f -l [size] |
| Set MTU on adapter | Command Prompt (Admin): netsh interface ipv4 set subinterface "Adapter Name" mtu=1400 store=persistent |
| Reset network stack | Command Prompt (Admin): netsh int ip reset and netsh winsock reset |
| Check network profile | Settings > Network & Internet > View connection properties |
| Check proxy settings | Settings > Network & Internet > Proxy |
| Check Windows Firewall | Settings > Privacy & Security > Windows Security > Firewall & network protection |

---

## Was this article helpful?

If this article helped resolve your issue, great. If something was unclear, missing, or did not work, please open a GitHub Issue describing the problem so we can improve it.

Suggest improvements at: https://github.com/EzioLockhart/Tier-1-Support-Knowledge-Base/issues

---

## References

- CompTIA A+ Troubleshooting Methodology: Identify the problem, Establish a theory, Test the theory, Establish a plan of action, Verify functionality, Document findings
- ITIL Incident Management best practices: Prioritize based on impact and urgency; VPN connectivity loss affects all remote work
- Microsoft official documentation: Troubleshoot VPN connection and routing issues

---

*Tier: Tier 1 (Help Desk) | Difficulty: L2 (Intermediate) | Estimated Resolution Time: 15-25 minutes | Required Access Level: Power User | Severity: P1 (Single User Critical)*

---

For internal use. Follow your organization's VPN and network security policies.
