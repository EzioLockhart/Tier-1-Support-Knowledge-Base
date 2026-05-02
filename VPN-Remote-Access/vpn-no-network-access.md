# VPN Connected but No Network Access

**Category:** VPN & Remote Access
**Last Updated:** April 27, 2026
**Applies To:** Windows 10, Windows 11, All VPN Clients (Cisco AnyConnect, FortiClient, Pulse Secure, GlobalProtect, OpenVPN, Microsoft Always On VPN, Windows Built-in VPN)

---

## Symptoms

- VPN client shows "Connected" or green status but no network resources are accessible
- Cannot access internal company websites, intranet, or SharePoint
- Mapped network drives do not connect or show red X
- Remote Desktop (RDP) connections to internal servers fail with "Cannot connect" or timeout error
- Internet access works normally (or stops entirely, depending on VPN configuration)
- Ping to internal servers by IP address or hostname fails with "Request timed out" or "Destination host unreachable"
- VPN connection time is counting up but zero data is being sent or received
- If VPN fails to connect at all with an authentication error, see: [VPN Connection Fails with Authentication Error](./vpn-authentication-error.md)

---

## Quick Checks (30 seconds)

1. Verify the VPN client actually shows "Connected" — if it is still "Connecting" or "Authenticating", the connection is not fully established
2. Try accessing a resource by IP address instead of hostname (e.g., \\192.168.1.50 instead of \\fileserver) — if IP works but hostname does not, the problem is DNS
3. Check if you can access any internal resources at all, or if all internal access is blocked — helps narrow down the scope
4. Open a web browser and try loading an external website — if the internet also does not work, the VPN may be routing all traffic incorrectly
5. Disconnect the VPN, wait 30 seconds, and reconnect — a simple reconnect often resolves temporary routing issues

---

## Step-by-Step Resolution

### Step 1: Verify VPN Connection Details and Status

1. Check the VPN client for actual connection details, not just the "Connected" indicator:
   - Look for "Bytes Sent" and "Bytes Received" — if both show 0 or very low numbers after being connected for several minutes, no actual traffic is flowing
   - Check the connection duration timer is counting up
   - Look for the assigned virtual IP address (VPN IP) — if missing or showing 0.0.0.0, the VPN did not receive a valid IP configuration
2. Open **Command Prompt** and check your network configuration:

ipconfig /all

3. Look for the VPN adapter in the output — it may be named after your VPN client (e.g., "Cisco AnyConnect Secure Mobility Client", "Pulse Secure", or "PPP adapter")
4. Verify the VPN adapter has:
   - A valid IP address (not 0.0.0.0 or 169.254.x.x, which is an APIPA auto-configuration failure address)
   - A subnet mask
   - DNS server addresses (usually the company's internal DNS servers)
   - Default gateway (may or may not be present depending on VPN configuration)
5. If the VPN adapter shows no IP address or an APIPA address (169.254.x.x), the VPN server did not assign proper network settings — disconnect and reconnect to obtain a new IP lease
   - A VPN that shows connected but did not receive a valid IP configuration cannot route traffic to internal resources.

### Step 2: Flush DNS and Reset Network Stack

1. After connecting to VPN, the local DNS cache may still contain old entries that do not resolve through the VPN tunnel
2. Open **Command Prompt as Administrator** (Win + X > Terminal (Admin))
3. Run the following commands one at a time, pressing Enter after each:

ipconfig /flushdns
ipconfig /registerdns
netsh int ip reset
netsh winsock reset

4. Wait for each command to complete before running the next
5. Restart the computer after running all commands
6. After restart, connect to the VPN first, then test access to internal resources
   - DNS cache flushing forces Windows to use the VPN-assigned DNS servers for internal hostname resolution.

### Step 3: Check Network Profile and Firewall Settings

1. When connected to VPN, Windows may classify the VPN connection as a "Public" network, which enables stricter firewall rules that block internal resource access
2. Check the network profile:
   - Open **Settings** > **Network & Internet**
   - Look for your VPN connection in the network list
   - Check if it says "Public network" or "Private network"
3. If set to Public, change it to Private:
   - Windows 11: Click on the VPN connection > **"Properties"** > Under Network profile type, select **"Private network"**
   - Windows 10: Click on the VPN connection > Under Network profile, select **"Private"**
4. Temporarily disable Windows Firewall to test if it is blocking VPN traffic:
   - **Settings** > **Privacy & Security** > **Windows Security** > **Firewall & network protection**
   - Select the active network profile > Turn off **"Microsoft Defender Firewall"**
   - Test access to internal resources
   - Whether it works or not, turn the firewall back on immediately after testing
5. If disabling the firewall resolves the issue, add a firewall exception for the VPN client or change the network profile to Private permanently
6. Also check third-party firewalls (Norton, McAfee, Bitdefender, ZoneAlarm) — many include their own network filtering that can block VPN traffic
   - Windows Firewall profiles treat Public networks as untrusted and block many types of incoming connections required for VPN access to internal resources.

### Step 4: Check Split Tunneling Configuration

1. Split tunneling determines whether only company traffic goes through the VPN (split tunnel) or all internet traffic goes through the VPN (full tunnel)
2. With split tunneling:
   - Internal company resources should be accessible through the VPN
   - Internet traffic (Google, YouTube, news sites) goes through your regular internet connection
   - If split tunneling is misconfigured, internal traffic may not be properly routed through the VPN
3. With full tunneling:
   - All traffic, both internal and internet, goes through the VPN
   - If the internet also does not work, the VPN server's routing to the internet may be down
4. To check your routing:
   - Open **Command Prompt** and type:

route print

   - Look at the routing table — the VPN adapter should have routes to your company's internal IP ranges (e.g., 10.x.x.x, 172.16.x.x, 192.168.x.x)
   - If no internal routes are listed, the VPN did not push the correct routing configuration
5. You cannot change split tunneling from your end — this is a server-side setting
6. If split tunneling is suspected as the issue, note this in the ticket and escalate to the network team
   - Understanding whether your organization uses split or full tunnel helps narrow down whether the problem is with internal routing or general VPN connectivity.

### Step 5: Check Proxy Server Settings

1. Many organizations require a specific proxy server configuration to access internal resources after connecting to VPN
2. Check current proxy settings:
   - **Settings** > **Network & Internet** > **Proxy**
   - Look at "Manual proxy setup" — is a proxy server configured?
   - Check "Automatically detect settings" is enabled if your organization uses automatic proxy detection (WPAD)
3. If a proxy is required but not configured:
   - Enter the proxy server address and port provided by your IT department
   - Check "Don't use the proxy server for local (intranet) addresses" if instructed
4. If the proxy is configured but internal resources still do not load:
   - Try disabling the proxy temporarily to test direct access
   - If direct access works, the proxy server or its configuration is the problem
5. Proxy settings may also be configured via Group Policy and cannot be changed locally — if so, note this and escalate
   - Missing or incorrect proxy configuration is a very common cause of "VPN connected but can't access anything" because all browser and application traffic is trying to go through a proxy that is only reachable via the VPN, creating a deadlock.

### Step 6: Adjust MTU (Maximum Transmission Unit) Size

1. MTU mismatch can cause some or all network traffic to fail over VPN
2. The VPN adds encryption overhead to each network packet, which can exceed the maximum packet size allowed by your network path
3. Test for MTU issues:
   - Open **Command Prompt** and type:

ping [internal server IP] -f -l 1472

   - Replace [internal server IP] with an actual internal server IP address
   - The -f flag sets "Don't Fragment" and -l 1472 sets the packet size
   - If you get "Packet needs to be fragmented but DF set", the packet is too large
4. Reduce the packet size by 10 and test again:

ping [internal server IP] -f -l 1400

5. Continue reducing until the ping succeeds — the highest successful value plus 28 (for headers) is your maximum MTU
6. To set a lower MTU on the VPN adapter:
   - Open **Command Prompt as Administrator**
   - Identify your VPN adapter name from ipconfig (e.g., "Ethernet 2", "Cisco AnyConnect")
   - Set the MTU:

netsh interface ipv4 set subinterface "VPN Adapter Name" mtu=1400 store=persistent

   - Replace "VPN Adapter Name" with your actual VPN adapter name and 1400 with your tested value
7. Disconnect and reconnect the VPN, then test access to internal resources
   - MTU issues are especially common on home broadband connections (DSL, cable) and when using VPN over Wi-Fi; lowering MTU resolves fragmentation issues that silently drop network traffic.

### Step 7: Reinstall or Update the VPN Client

1. A corrupted VPN client or outdated virtual network adapter driver can cause a false "Connected" state with no actual data flow
2. Check if there is a newer version of the VPN client available from your organization's software portal or the vendor's website
3. If an update is available, download and install it
4. If already on the latest version, perform a clean reinstall:
   - Disconnect the VPN
   - Uninstall the VPN client from **Settings** > **Apps** > **Installed apps**
   - Restart the computer
   - Check for and delete leftover VPN adapter entries:
     - Open **Device Manager** (Win + X > Device Manager)
     - Expand **"Network adapters"**
     - Look for any adapters with the VPN client name (e.g., "Cisco AnyConnect Virtual Miniport Adapter", "Pulse Secure Virtual Adapter")
     - Right-click and select **"Uninstall device"**
   - Restart the computer again
   - Reinstall the VPN client using the latest installer from your organization or vendor
   - Restart one final time, then connect and test
5. If the VPN client requires administrator rights to install and you do not have them, escalate to IT
   - A corrupted virtual network adapter driver can show as fully connected in the VPN client while passing no actual data, making this a critical step when all routing and DNS checks appear normal.

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

## Escalation Criteria

Escalate to Tier 2 / Network Team if:

- Multiple users cannot access internal resources after connecting to the same VPN server (indicates server-side issue)
- Routes to internal networks are missing from the route table after VPN connection
- VPN adapter receives no IP address or an APIPA address (169.254.x.x) after multiple reconnects
- Split tunneling or full tunnel configuration needs to be changed (server-side setting)
- Proxy configuration is managed by Group Policy and requires changes
- VPN server logs need to be reviewed to determine why traffic is not routing
- The VPN server's DHCP pool may be exhausted (no available IP addresses to assign)
- Internal DNS servers are unreachable from the VPN subnet

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

For internal use. Follow your organization's VPN and network security policies.
