# VPN Connection Fails with Authentication Error

- **Category:** VPN & Remote Access
- **Tier:** Tier 1 (Help Desk)
- **Version:** 1.0
- **Last Updated:** May 2, 2026
- **Last Reviewed:** May 2, 2026
- **Applies To:** Windows 10 (22H2), Windows 11 (23H2), Built-in VPN Client, Cisco AnyConnect, FortiClient, Pulse Secure, GlobalProtect, OpenVPN, Microsoft 365 VPN
- **Difficulty:** L2 (Intermediate)
- **Estimated Resolution Time:** 10-20 minutes
- **Required Access Level:** Power User
- **Severity:** P1 (Single User, Critical — Cannot Access Corporate Network)
- **Keywords:** VPN, authentication, login failed, credentials, MFA, firewall, VPN client, server address, AnyConnect
- **Prerequisite Knowledge:** Basic Windows navigation, ability to open Command Prompt and Credential Manager

---

## Symptoms

- VPN client displays error message: "Authentication failed", "Login failed", or "Invalid credentials"
- User enters username and password but connection does not complete
- Error code specific to the VPN client (e.g., Error 691, Error 812, Error 13801 for Windows VPN)
- VPN attempts to connect, hangs on "Verifying credentials" or "Authenticating", then fails
- User is certain the username and password are correct but VPN still rejects them
- Two-factor authentication (MFA/2FA) prompt does not appear or times out
- VPN was working previously but suddenly stopped authenticating without any changes

---

## Common Error Codes

| Code | Meaning |
|------|---------|
| Error 691 | Access denied — username or password invalid on this domain |
| Error 812 | Connection prevented by policy — check NPS/RADIUS server configuration |
| Error 13801 | Authentication failed — certificate issue or PEAP configuration error |
| Error 789 | L2TP connection attempt failed — security layer authentication failure |

---

## Symptom-to-Step Mapping

| If You See This | Skip To |
|-----------------|---------|
| User recently changed their password | Step 1 |
| VPN worked yesterday but not today | Step 3 |
| MFA prompt not appearing | Step 7 |
| Error mentions "certificate" | Step 3 |
| VPN fails only on one specific network | Step 2 |

---

## Triage Questions

Before starting troubleshooting, ask the user:

1. "Can you confirm the exact username format you're using — does it include a domain prefix like DOMAIN\username?"
2. "Did you recently change your network or domain password?"
3. "Are you using the same computer and network as before, or are you somewhere new (hotel, coffee shop, home)?"
4. "Do you receive a multi-factor authentication prompt on your phone, or does nothing appear?"

---

## Quick Checks (30 seconds)

1. Ask the user to confirm they are entering the correct username (check DOMAIN\username or username@domain.com format if required)
2. Verify the user has a working internet connection — open a browser and load any website
3. Try typing the password into Notepad first to see it clearly (prevent typos from hidden characters), then copy into the VPN client
4. Check if Caps Lock is on — this is a frequent cause of authentication failures
5. Ask if the user has recently changed their domain/network password and not updated it in the VPN client
6. Check if the user has an active VPN session on another device (some VPNs only allow one connection per user)
7. If VPN connects successfully but you cannot access internal resources after connecting, see: [VPN Connected but No Network Access](./vpn-no-network-access.md)

---

## Step-by-Step Resolution

### Step 1: Verify Username Format and Credentials
1. Confirm the exact username format required by your organization's VPN:
   - Domain prefix: DOMAIN\username (e.g., CONTOSO\john.doe)
   - UPN format: username@domain.com (e.g., john.doe@contoso.com)
   - Username only: john.doe (no domain prefix, common with third-party VPN clients)
2. Ask the user to type their password into Notepad to verify there are no typing errors:
   - Check for accidental spaces before or after the password
   - Verify special characters are being typed correctly on the keyboard layout (e.g., @ vs " on UK vs US keyboards)
3. If the user recently changed their domain password, the VPN client may still have the old password stored:
   - Open the VPN client and look for a saved password field
   - Delete the saved password and re-enter the new one
   - Some VPN clients have a "Forget Password" or "Clear Saved Credentials" option

**What to tell the user:** "The most common cause of VPN authentication failures is the username format being wrong. Some VPNs require just your username, others need DOMAIN\username, and others need your full email address. Let's verify which format your organization uses and make sure we're using the right one."

### Step 2: Verify Internet Connectivity and Firewall
1. Check the user has a working internet connection:
   - Open a browser and navigate to a known website (e.g., google.com or bing.com)
   - If on Wi-Fi, try switching to a wired connection or a mobile hotspot temporarily
2. Test if the VPN server is reachable:
   - Open Command Prompt and type: ping [VPN server address]
   - Replace [VPN server address] with the actual VPN server hostname or IP
   - If ping fails, the VPN server may be unreachable from the user's network
3. Check if a firewall is blocking the VPN connection:
   - Corporate firewalls, hotel Wi-Fi, coffee shop networks, and some ISPs block VPN protocols
   - Try connecting from a different network (e.g., mobile hotspot) to isolate the issue
   - Check if the required VPN ports are open: PPTP (TCP 1723), L2TP/IPSec (UDP 500, UDP 4500), SSTP (TCP 443), OpenVPN (UDP 1194 or TCP 443), IKEv2 (UDP 500, UDP 4500)
4. Temporarily disable the Windows Firewall or third-party firewall to test:
   - Settings > Privacy & Security > Windows Security > Firewall & network protection
   - Turn off firewall temporarily, test VPN, then turn firewall back on immediately

**What to tell the user:** "Some networks — especially public Wi-Fi at hotels or coffee shops — actively block VPN connections. If you're traveling or on a guest network, that could be why your VPN worked yesterday but not today. Let's test by connecting through a mobile hotspot instead."

### Step 3: Check VPN Server Address and Configuration
1. Verify the VPN server address is correct in the VPN client settings:
   - In Windows built-in VPN: Settings > Network & Internet > VPN > Select connection > Advanced options > Edit
   - In third-party VPN clients: Look for "Server", "Gateway", or "Server URL" in the connection settings
2. Confirm the server address with your IT department or VPN documentation:
   - Server addresses can change after infrastructure updates or migrations
   - Test alternate server addresses if your organization has multiple VPN gateways
3. Check if the VPN type/protocol is set correctly:
   - Windows VPN supports: Automatic, PPTP, L2TP/IPSec with certificate, L2TP/IPSec with pre-shared key, SSTP, IKEv2
   - The protocol must match what the VPN server expects
   - If unsure, try "Automatic" (Windows VPN) or ask the network team for the correct protocol

**What to tell the user:** "The VPN server address or protocol might have changed, or it might be misconfigured in your client. This is like having the wrong phone number — even if you dial perfectly, you won't connect. Let's verify the server details are correct."

### Step 4: Flush DNS and Reset Network Stack
1. A corrupted DNS cache or network configuration can interfere with VPN authentication
2. Open Command Prompt as Administrator: Win + X > Terminal (Admin)
3. Run the following commands one by one, pressing Enter after each:
   ipconfig /flushdns
   netsh int ip reset
   netsh winsock reset
4. Also release and renew the IP address:
   ipconfig /release
   ipconfig /renew
5. Restart the computer after running these commands
6. After restart, try the VPN connection again before opening any other applications

**What to tell the user:** "Your computer stores network settings that can get corrupted over time. We're going to completely reset those settings, which clears out any conflicts that might be interfering with the VPN. It's a quick process — just a few commands and a restart."

### Step 5: Clear Saved VPN Credentials in Windows Credential Manager
1. VPN clients often store credentials in Windows Credential Manager, and these can become corrupted
2. Open Credential Manager:
   - Type "Credential Manager" in the Start menu search
   - Or Control Panel > User Accounts > Credential Manager
3. Click "Windows Credentials"
4. Scroll through the list and look for any entries related to your VPN:
   - Entries may be named with the VPN server address, VPN connection name, or "Microsoft VPN"
   - Look under both "Generic Credentials" and "Windows Credentials"
5. Click the arrow next to the VPN credential > "Remove"
6. Also check "Generic Credentials" for any saved VPN-related entries and remove them
7. Close Credential Manager and restart the computer
8. After restart, open the VPN client and enter credentials fresh

**What to tell the user:** "Windows saves your VPN password in a hidden credential vault. Sometimes that saved password gets corrupted — especially after a password change — and the VPN keeps trying the old, broken copy. We're going to delete the saved version so the VPN uses your fresh login."

### Step 6: Reinstall or Update the VPN Client
1. Check if there is a newer version of the VPN client available:
   - Third-party VPNs: Visit the vendor's download page (Cisco, Fortinet, Pulse Secure, Palo Alto, etc.)
   - Windows built-in VPN: Ensure Windows is fully updated via Settings > Windows Update
2. If an update is available, download and install it
3. If already on the latest version, perform a clean reinstall:
   - Uninstall the VPN client from Settings > Apps > Installed apps
   - Restart the computer
   - Delete any leftover folders in:
     - C:\Program Files\VPN Client Name
     - C:\Program Files (x86)\VPN Client Name
     - C:\ProgramData\VPN Client Name
   - Restart again
   - Download the latest installer from the official source and install fresh
4. After reinstallation, configure the VPN connection with the correct server address and protocol
5. Test the connection

**What to tell the user:** "The VPN client software itself might be corrupted or outdated. Even if your credentials are perfect, a broken client can't authenticate. We're going to do a clean reinstall — completely removing the old version and installing a fresh copy from scratch."

### Step 7: Check Multi-Factor Authentication (MFA/2FA)
1. If your organization uses MFA for VPN:
   - Verify the user receives the MFA prompt (push notification, SMS, phone call, or app notification)
   - If using Microsoft Authenticator, Duo, or similar: ensure the app is installed and notifications are enabled
   - If no prompt appears: check the user's mobile device has internet connectivity (Wi-Fi or cellular data)
2. Common MFA issues:
   - User changed phones and did not re-register MFA — needs IT admin to reset MFA methods
   - Time-based token out of sync (for hardware tokens or authenticator apps): ensure the device clock is set to automatic
   - SMS code not arriving: check mobile signal, try phone call verification as an alternative
   - Push notification not appearing: open the authenticator app manually and check for pending approvals
3. If the VPN client requires a specific format for MFA:
   - Some VPNs require the password and MFA code combined: password,token (e.g., MyPassword,123456)
   - Others prompt separately: first password, then MFA code in a second prompt
   - Confirm the correct format with your IT department

**What to tell the user:** "If your organization uses multi-factor authentication, the VPN might be waiting for a verification that isn't reaching your phone. This is often mistaken for a password problem. Let's check that your MFA app is working and your phone has an internet connection."

---

## Alternative Solutions

If the above steps do not resolve the issue, also try:

- Connecting from a completely different network (e.g., mobile hotspot) to rule out local network blocking
- Using the VPN provider's alternative connection method (e.g., SSL VPN instead of IPsec)
- Checking with your IT department if your VPN account is locked, disabled, or expired
- For certificate-based authentication: checking if the VPN certificate has expired on your computer or the server

---

## Prevention Tips

- Save your organization's VPN server address and correct protocol in a note for quick reconfiguration
- Update your VPN password in the client immediately after changing your domain password
- Keep your VPN client updated to the latest version for security and compatibility fixes
- Always have your MFA backup codes or alternate method accessible when traveling
- Test your VPN connection before critical remote work sessions to catch issues early

---

## Root Cause

Common causes of VPN authentication failures, in order of likelihood:

- Incorrect username format (wrong domain prefix or missing @domain.com suffix) — most common
- Recent domain password change not updated in the VPN client's saved credentials
- Caps Lock enabled during password entry
- Corrupted saved credentials in Windows Credential Manager
- VPN server address or protocol misconfiguration in the client settings
- Firewall or network blocking VPN ports (especially on public Wi-Fi, hotels, or restrictive corporate guest networks)
- Multi-Factor Authentication failure (no prompt, timed out, or user locked out of MFA)
- VPN client installation corrupted or outdated

---

## Escalation Decision Matrix

| Condition | Action |
|-----------|--------|
| All 7 steps completed, issue persists | Escalate to Tier 2 |
| VPN server is unreachable (ping fails from multiple networks) | Escalate — possible server outage |
| Multiple users report the same authentication failure simultaneously | Escalate — likely server-side issue |
| User's VPN account has been locked, disabled, or expired | Escalate — requires account administration |
| MFA reset needed (user got a new phone, lost access to authenticator app) | Escalate — requires Identity team |
| VPN certificate on the client or server may have expired | Escalate — requires certificate management |
| Clean reinstall and all steps do not resolve | Escalate — advanced investigation needed |

---

## Related Articles

- [VPN Connected but No Network Access](./vpn-no-network-access.md) — If VPN connects but internal resources are unreachable
- [VPN Connection Tips — Self-Service Guide](../Tier-0-Self-Service/vpn-connection-tips.md) — Tier 0: Self-service guide for users
- [Firewall Rule & VPN Gateway Configuration Analysis](../Tier-2-Technical-Support/firewall-vpn-gateway.md) — Tier 2: Advanced VPN diagnostics
- [VPN Split Tunnel Architecture & Routing Design](../Tier-3-Expert-Engineering/vpn-split-tunnel-architecture.md) — Tier 3: VPN architecture analysis

> **Note:** If you are looking for the Tier 0 self-service version of this article, see: [VPN Connection Tips — Self-Service Guide](../Tier-0-Self-Service/vpn-connection-tips.md) (to be created if not yet present).

---

## FAQ

**Q: Why does my VPN say my password is wrong when I know it's correct?**
**A:** This usually happens when your saved credentials are corrupted or your password recently changed. Clear the saved password (Step 5), type it fresh, and try again. Also check that Caps Lock is off and your username format is correct for your organization.

**Q: Can my home router block VPN connections?**
**A:** Yes. Some home routers have a feature called "VPN Passthrough" that must be enabled for certain VPN protocols (especially PPTP and L2TP/IPSec). Check your router's settings if VPN fails on your home network but works elsewhere.

**Q: What should I do if my MFA prompt never arrives?**
**A:** First, check your phone has internet (Wi-Fi or cellular data). Open the authenticator app manually — sometimes notifications are delayed, but pending approvals appear in the app. If using SMS, check that you have cellular signal. As a backup, use your saved recovery codes if available.

---

## Commands and Shortcuts Quick Reference

| Action | How To Access |
|--------|---------------|
| Open Windows VPN settings | Settings > Network & Internet > VPN |
| Open Network Connections | Win + R > ncpa.cpl |
| Open Credential Manager | Start menu > type "Credential Manager" |
| Flush DNS | Command Prompt (Admin): ipconfig /flushdns |
| Reset network stack | Command Prompt (Admin): netsh int ip reset and netsh winsock reset |
| Release/Renew IP | Command Prompt (Admin): ipconfig /release then ipconfig /renew |
| Test VPN server reachability | Command Prompt: ping [VPN server address] |
| Check Windows Firewall | Settings > Privacy & Security > Windows Security > Firewall & network protection |

---

## Was this article helpful?

If this article helped resolve your issue, great. If something was unclear, missing, or did not work, please open a GitHub Issue describing the problem so we can improve it.

Suggest improvements at: https://github.com/EzioLockhart/Tier-1-Support-Knowledge-Base/issues

---

## References

- CompTIA A+ Troubleshooting Methodology: Identify the problem, Establish a theory, Test the theory, Establish a plan of action, Verify functionality, Document findings
- ITIL Incident Management best practices: Prioritize based on impact and urgency; VPN access is critical for remote work
- Microsoft official documentation: Troubleshoot VPN connection errors in Windows

---

*Tier: Tier 1 (Help Desk) | Difficulty: L2 (Intermediate) | Estimated Resolution Time: 10-20 minutes | Required Access Level: Power User | Severity: P1 (Single User Critical)*

---

For internal use. Follow your organization's VPN and security policies.
