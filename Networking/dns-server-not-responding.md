# DNS Server Not Responding

**Category:** Networking
**Last Updated:** May 2, 2026
**Applies To:** Windows 10, Windows 11, All Network Connections

---

## Symptoms

- Browser displays "DNS server not responding" or "DNS_PROBE_FINISHED_NXDOMAIN"
- Websites fail to load by name but may load by IP address
- ping to a website by name fails but ping to 8.8.8.8 works
- Network icon shows connected but "No Internet" or limited access
- All browsers on the computer show the same DNS error
- Other devices on the same network can access websites normally
- Issue may be intermittent — some sites load while others fail

---

## Quick Checks (30 seconds)

1. Try loading a website by its IP address instead of its name — if IP works but name fails, the problem is definitely DNS
2. Check if other devices on the same network can access websites — if yes, the problem is local to this computer
3. Restart your browser completely (close all windows) and try again
4. Try a different browser — if one browser works and another doesn't, the problem is browser-specific
5. If there is no internet access at all, see: [No Internet Access (Limited Connectivity)](./no-internet-access.md)

---

## Step-by-Step Resolution

### Step 1: Flush DNS Cache

1. Open Command Prompt as Administrator (Win + X > Terminal (Admin))
2. Type the following command and press Enter: ipconfig /flushdns
3. You should see: "Successfully flushed the DNS Resolver Cache."
4. Also register DNS and release/renew IP: ipconfig /registerdns, ipconfig /release, ipconfig /renew
5. Restart your browser and test if websites now load
   - A corrupted DNS cache is the most common cause of DNS errors; flushing it forces Windows to query DNS servers fresh.

### Step 2: Change DNS Server Address

1. Your ISP's default DNS server may be slow or temporarily down
2. Switch to a public DNS server like Google DNS or Cloudflare:
3. Open Settings > Network & Internet > Advanced network settings > More network adapter options
   - On Windows 10: Control Panel > Network and Sharing Center > Change adapter settings
4. Right-click your active network connection (Wi-Fi or Ethernet) > Properties
5. Select "Internet Protocol Version 4 (TCP/IPv4)" > Click "Properties"
6. Select "Use the following DNS server addresses:"
7. Enter these values:
   - Preferred DNS server: 8.8.8.8 (Google)
   - Alternate DNS server: 8.8.4.4 (Google)
   - Or use Cloudflare: 1.1.1.1 and 1.0.0.1
8. Click OK then Close
9. Open Command Prompt and flush DNS again: ipconfig /flushdns
10. Test websites in your browser
    - Changing to a reliable public DNS server bypasses your ISP's DNS if it is the source of the problem.

### Step 3: Restart DNS Client Service

1. Press Win + R, type services.msc, and press Enter
2. Scroll down and find "DNS Client"
3. Right-click "DNS Client" > "Restart"
4. If Restart is grayed out, click "Stop", wait 5 seconds, then click "Start"
5. Close Services and test websites
   - The DNS Client service manages local DNS caching; restarting it clears in-memory DNS issues that flushdns alone may not resolve.

### Step 4: Reset Network Stack Completely

1. Open Command Prompt as Administrator
2. Run these commands one by one, pressing Enter after each: netsh int ip reset, netsh winsock reset, ipconfig /flushdns
3. Restart the computer
4. After restart, test websites before opening any other applications
   - This fully resets all network settings to default, clearing any deep network configuration corruption.

### Step 5: Check Router DNS Settings

1. Access your router's admin page by typing its IP address in a browser:
   - Common addresses: 192.168.1.1, 192.168.0.1, or 192.168.1.254
2. Log in (credentials often on a sticker on the router)
3. Look for DNS Settings under Internet Setup, WAN Settings, or Network Settings
4. If the router's DNS is set to your ISP's default, try changing it to:
   - Primary: 8.8.8.8
   - Secondary: 8.8.4.4
5. Save settings and restart the router
6. After the router restarts, restart your computer and test
   - Router-level DNS problems affect all devices on the network; if multiple devices have DNS issues, the router is the likely cause.

### Step 6: Disable IPv6 Temporarily

1. IPv6 DNS issues can cause DNS failures even when IPv4 is working
2. Open Settings > Network & Internet > Advanced network settings > More network adapter options
3. Right-click your active connection > Properties
4. Uncheck "Internet Protocol Version 6 (TCP/IPv6)"
5. Click OK and restart your browser
6. Test if websites now load
7. If this fixes the problem, your router or ISP may have IPv6 DNS issues — re-enable IPv6 after the issue is resolved network-side
   - This is a temporary workaround; IPv6 should be re-enabled once the root cause is addressed.

### Step 7: Test DNS Resolution with nslookup

1. Open Command Prompt
2. Test DNS resolution for a specific website: nslookup google.com
3. Check the output:
   - If you see an IP address returned (e.g., 142.250.80.46), DNS is working for that site
   - If you see "DNS request timed out" or "Server: Unknown", your DNS server is unreachable
4. Test with a specific DNS server: nslookup google.com 8.8.8.8
   - If this works but the default test fails, your default DNS server is the problem
5. Test multiple websites to see if the issue is site-specific or global: nslookup microsoft.com, nslookup github.com
   - If some sites resolve and others don't, the problem may be with specific DNS zones

---

## Root Cause

Common causes of DNS server not responding, in order of likelihood:

- Corrupted local DNS cache (most common — resolved by flushing DNS)
- ISP DNS server temporarily down or slow
- Incorrect DNS server address configured on the computer or router
- DNS Client service stuck or crashed
- Router DNS relay failing to forward requests
- IPv6 DNS misconfiguration while IPv4 works fine
- Network adapter driver corruption affecting DNS resolution
- Firewall or security software blocking DNS traffic (UDP port 53)

---

## Escalation Criteria

Escalate to Tier 2 / Network Team if:

- Changing to public DNS (8.8.8.8) does not resolve the issue
- Multiple devices on the same network have DNS issues (indicates router or ISP problem)
- nslookup fails even with a known-working DNS server like 8.8.8.8
- ISP DNS outage is confirmed requiring ISP contact
- DNS issues persist after router restart and DNS configuration change
- Organization uses internal DNS servers that require administrative access to check
- Firewall or security policy changes are needed to allow DNS traffic

---

## Commands Quick Reference

| Command | Purpose |
|---------|---------|
| ipconfig /flushdns | Clear local DNS resolver cache |
| ipconfig /registerdns | Re-register DNS records |
| ipconfig /release | Release current IP address |
| ipconfig /renew | Request new IP address |
| netsh int ip reset | Reset TCP/IP stack to defaults |
| netsh winsock reset | Reset Windows network socket settings |
| nslookup google.com | Test DNS resolution for a domain |
| nslookup google.com 8.8.8.8 | Test DNS resolution using a specific server |
| ping 8.8.8.8 | Test basic internet connectivity (bypasses DNS) |

---

For internal use. Follow your organization's escalation procedures.
