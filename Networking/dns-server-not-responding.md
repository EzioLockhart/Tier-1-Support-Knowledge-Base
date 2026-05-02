# DNS Server Not Responding

- **Category:** Networking
- **Version:** 1.0
- **Last Updated:** May 2, 2026
- **Last Reviewed:** May 2, 2026
- **Applies To:** Windows 10 (22H2), Windows 11 (23H2)
- **Difficulty:** L2 (Intermediate)
- **Estimated Resolution Time:** 10-20 minutes
- **Required Access Level:** Power User
- **Severity:** P1 (Single User, Critical — Cannot Browse Web)
- **Keywords:** DNS, server not responding, NXDOMAIN, nslookup, DNS cache, DNS server, name resolution, connectivity
- **Prerequisite Knowledge:** Basic Windows navigation, ability to open Command Prompt and network settings

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

## Common Error Codes

| Code | Meaning |
|------|---------|
| DNS_PROBE_FINISHED_NXDOMAIN | DNS server returned non-existent domain — name cannot be resolved |
| DNS_PROBE_FINISHED_BAD_CONFIG | DNS configuration on the computer is incorrect or corrupted |
| DNS_PROBE_FINISHED_NO_INTERNET | DNS server is unreachable — no response from configured DNS |
| ERR_NAME_NOT_RESOLVED | The domain name could not be resolved to an IP address |

---

## Symptom-to-Step Mapping

| If You See This | Skip To |
|-----------------|---------|
| ping 8.8.8.8 works but websites fail by name | Step 1 |
| nslookup fails with "timed out" | Step 2 |
| Issue affects all devices on same network | Step 5 |
| DNS errors started after Windows Update | Step 4 |
| Some websites load but others fail | Step 7 |

---

## Triage Questions

Before starting troubleshooting, ask the user:

1. "Can you load a website by typing its IP address instead of its name? For example, try typing 142.250.80.46 for Google."
2. "Are other devices on the same Wi-Fi or network able to browse the internet normally?"
3. "Did this problem start suddenly, or has it been happening intermittently for a while?"
4. "Have you or anyone else changed any router or network settings recently?"

---

## Quick Checks (30 seconds)

1. Try loading a website by its IP address instead of its name — if IP works but name fails, the problem is definitely DNS
2. Check if other devices on the same network can access websites — if yes, the problem is local to this computer
3. Restart your browser completely (close all windows) and try again
4. Try a different browser — if one browser works and another doesn't, the problem is browser-specific
5. If there is no internet access at all (not just DNS issues), see: [No Internet Access (Limited Connectivity)](./no-internet-access.md)

---

## Step-by-Step Resolution

### Step 1: Flush DNS Cache
1. Open Command Prompt as Administrator: Press Win + X > Terminal (Admin)
2. Run the following commands in order, pressing Enter after each:
   ipconfig /flushdns
   ipconfig /registerdns
   ipconfig /release
   ipconfig /renew
3. Restart your browser and test if websites now load

**What to tell the user:** "Your computer keeps a local cache of website addresses to load pages faster. Sometimes that cache gets corrupted. We're going to clear it and force your computer to look up website addresses fresh. This is safe and takes less than a minute."

### Step 2: Change DNS Server Address
1. Open Settings > Network & Internet > Advanced network settings > More network adapter options
   - On Windows 10: Control Panel > Network and Sharing Center > Change adapter settings
2. Right-click your active network connection (Wi-Fi or Ethernet) > Properties
3. Select "Internet Protocol Version 4 (TCP/IPv4)" > Click "Properties"
4. Select "Use the following DNS server addresses:"
5. Enter these values:
   - Preferred DNS server: 8.8.8.8 (Google)
   - Alternate DNS server: 8.8.4.4 (Google)
   - Or use Cloudflare: 1.1.1.1 and 1.0.0.1
6. Click OK then Close
7. Open Command Prompt and flush DNS again: ipconfig /flushdns
8. Test websites in your browser

**What to tell the user:** "Your ISP's DNS server might be slow or down. We're going to switch to Google's public DNS servers, which are fast and reliable. Think of DNS as the phonebook of the internet — we're just using a different phonebook."

### Step 3: Restart DNS Client Service
1. Press Win + R, type services.msc, and press Enter
2. Scroll down and find "DNS Client"
3. Right-click "DNS Client" > "Restart"
4. If Restart is grayed out, click "Stop", wait 5 seconds, then click "Start"
5. Close Services and test websites

**What to tell the user:** "Windows has a background service that handles all DNS lookups. Sometimes this service gets stuck. We're going to restart it, which is like rebooting just the DNS part of your computer."

### Step 4: Reset Network Stack Completely
1. Open Command Prompt as Administrator
2. Run these commands one by one, pressing Enter after each:
   netsh int ip reset
   netsh winsock reset
   ipconfig /flushdns
3. Restart the computer
4. After restart, test websites before opening any other applications

**What to tell the user:** "We're going to do a complete reset of all network settings on your computer. This clears out any deep configuration corruption. Your computer will need to restart, and everything network-related will be set back to default."

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

**What to tell the user:** "If multiple devices in your home are having DNS issues, the router itself might be the problem. We're going to change the DNS settings on the router so every device benefits. You'll need your router login credentials for this step."

### Step 6: Disable IPv6 Temporarily
1. Open Settings > Network & Internet > Advanced network settings > More network adapter options
   - On Windows 10: Control Panel > Network and Sharing Center > Change adapter settings
2. Right-click your active connection > Properties
3. Uncheck "Internet Protocol Version 6 (TCP/IPv6)"
4. Click OK and restart your browser
5. Test if websites now load
6. If this fixes the problem, your router or ISP may have IPv6 DNS issues

**What to tell the user:** "IPv6 is a newer internet protocol, but some routers and ISPs have problems with their IPv6 DNS. We're going to temporarily disable IPv6 as a test. If this works, we'll keep it disabled until the underlying issue is fixed network-side."

### Step 7: Test DNS Resolution with nslookup
1. Open Command Prompt
2. Test DNS resolution for a specific website: nslookup google.com
3. Check the output:
   - If you see an IP address returned (e.g., 142.250.80.46), DNS is working for that site
   - If you see "DNS request timed out" or "Server: Unknown", your DNS server is unreachable
4. Test with a specific DNS server: nslookup google.com 8.8.8.8
   - If this works but the default test fails, your default DNS server is the problem
5. Test multiple websites: nslookup microsoft.com, nslookup github.com

**What to tell the user:** "Let's run a diagnostic test to see exactly where DNS is failing. This will tell us whether the problem is with your DNS server, your router, or something else entirely."

---

## Alternative Solutions

If the above steps do not resolve the issue, also try:

- Booting into Safe Mode with Networking to rule out third-party firewall or antivirus interference
- Temporarily disabling any VPN software, which can override DNS settings
- Checking the hosts file (C:\Windows\System32\drivers\etc\hosts) for incorrect entries that may block specific websites
- Resetting the router to factory defaults and reconfiguring from scratch

---

## Prevention Tips

- Use a reliable public DNS server like Google DNS (8.8.8.8) or Cloudflare (1.1.1.1) instead of relying on your ISP's DNS
- Restart your router monthly to clear its DNS cache and memory
- Keep your network adapter drivers updated through Windows Update
- Avoid installing multiple antivirus or firewall programs that may conflict and interfere with DNS
- Bookmark key IP addresses (like 8.8.8.8) for testing connectivity when DNS is down

---

## Root Cause

Common causes of DNS server not responding, in order of likelihood:

- Corrupted local DNS cache on the computer (most common — resolved by flushing DNS)
- ISP DNS server temporarily down or slow
- Incorrect DNS server address configured on the computer or router
- DNS Client service stuck or crashed on the computer
- Router DNS relay failing to forward requests to the ISP
- IPv6 DNS misconfiguration while IPv4 works fine
- Network adapter driver corruption affecting DNS resolution
- Firewall or security software blocking DNS traffic (UDP port 53)

---

## Escalation Decision Matrix

| Condition | Action |
|-----------|--------|
| All 7 steps completed, issue persists | Escalate to Tier 2 |
| Changing to public DNS (8.8.8.8) does not resolve | Escalate — likely deeper network issue |
| Multiple devices on the same network have DNS issues | Escalate — likely router or ISP problem |
| nslookup fails even with known-working DNS server like 8.8.8.8 | Escalate — UDP port 53 may be blocked |
| ISP DNS outage confirmed via downdetector or ISP status page | Escalate — requires ISP contact |
| Organization uses internal DNS servers requiring admin access | Escalate for internal DNS server check |
| Issue occurs only on specific websites while others work | Continue troubleshooting, check hosts file |

---

## Related Articles

- [No Internet Access (Limited Connectivity)](./no-internet-access.md) — If there is no internet connection at all
- [Wi-Fi Keeps Disconnecting](./wifi-keeps-disconnecting.md) — If the connection drops repeatedly rather than failing to resolve names

---

## FAQ

**Q: What is DNS and why does it matter?**
**A:** DNS stands for Domain Name System. Think of it like the phonebook of the internet. When you type "google.com", DNS translates that name into an IP address like 142.250.80.46 that computers use to connect. If DNS fails, your computer can't look up where websites are located.

**Q: Is it safe to use Google DNS (8.8.8.8) instead of my ISP's DNS?**
**A:** Yes, it is safe. Google DNS and Cloudflare DNS (1.1.1.1) are reputable, fast, and used by millions of people. In fact, they are often faster and more reliable than ISP DNS servers.

**Q: Will changing DNS settings affect my internet speed?**
**A:** It will not affect download or upload speeds, but it can make websites feel faster because DNS lookups happen more quickly. A slow DNS server can make browsing feel sluggish even on a fast connection.

---

## Commands Quick Reference

| Command | Purpose |
|---------|---------|
| ipconfig /flushdns | Clear local DNS resolver cache |
| ipconfig /registerdns | Re-register DNS records with the network |
| ipconfig /release | Release current IP address |
| ipconfig /renew | Request new IP address from DHCP |
| netsh int ip reset | Reset TCP/IP stack to defaults |
| netsh winsock reset | Reset Windows network socket settings |
| nslookup google.com | Test DNS resolution for a domain name |
| nslookup google.com 8.8.8.8 | Test DNS resolution using a specific DNS server |
| ping 8.8.8.8 | Test basic internet connectivity (bypasses DNS) |

---

## Was this article helpful?

If this article helped resolve your issue, great. If something was unclear, missing, or did not work, please open a GitHub Issue describing the problem so we can improve it.

Suggest improvements at: https://github.com/EzioLockhart/Tier-1-Support-Knowledge-Base/issues

---

## References

- CompTIA A+ Troubleshooting Methodology: Identify the problem, Establish a theory, Test the theory, Establish a plan of action, Verify functionality, Document findings
- ITIL Incident Management best practices: Prioritize based on impact and urgency
- Microsoft official documentation: Fix DNS resolution issues in Windows

---

*Difficulty: L2 (Intermediate) | Estimated Resolution Time: 10-20 minutes | Required Access Level: Power User | Severity: P1 (Single User Critical)*

---

For internal use. Follow your organization's escalation procedures.
