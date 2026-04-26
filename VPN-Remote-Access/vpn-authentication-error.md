# VPN Connection Fails with Authentication Error

**Category:** VPN & Remote Access
**Last Updated:** April 27, 2026
**Applies To:** Windows 10, Windows 11, Built-in VPN Client, Cisco AnyConnect, FortiClient, Pulse Secure, GlobalProtect, OpenVPN, Microsoft 365 VPN

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

## Quick Checks (30 seconds)

1. Ask the user to confirm they are entering the correct username (check DOMAIN\username or username@domain.com format if required)
2. Verify the user has a working internet connection — open a browser and load any website
3. Try typing the password into Notepad first to see it clearly (prevent typos from hidden characters), then copy into the VPN client
4. Check if Caps Lock is on — this is a frequent cause of authentication failures
5. Ask if the user has recently changed their domain/network password and not updated it in the VPN client
6. Check if the user has an active VPN session on another device (some VPNs only allow one connection per user)

---

## Step-by-Step Resolution

### Step 1: Verify Username Format and Credentials

1. Confirm the exact username format required by your organization's VPN:
   - **Domain prefix:** DOMAIN\username (e.g., CONTOSO\john.doe)
   - **UPN format:** username@domain.com (e.g., john.doe@contoso.com)
   - **Username only:** john.doe (no domain prefix, common with third-party VPN clients)
2. Ask the user to type their password into Notepad to verify there are no typing errors:
   - Check for accidental spaces before or after the password
   - Verify special characters are being typed correctly on the keyboard layout (e.g., @ vs " on UK vs US keyboards)
3. If the user recently changed their domain password, the VPN client may still have the old password stored:
   - Open the VPN client and look for a saved password field
   - Delete the saved password and re-enter the new one
   - Some VPN clients have a "Forget Password" or "Clear Saved Credentials" option
4. Attempt to log in again with the verified credentials
   - Incorrect username format is one of the most common causes of VPN authentication failures, especially for new users or after account changes.

### Step 2: Verify Internet Connectivity and Firewall

1. Check the user has a working internet connection:
   - Open a browser and navigate to a known website (e.g., google.com or bing.com)
   - If on Wi-Fi, try switching to a wired connection or a mobile hotspot temporarily
2. Test if the VPN server is reachable:
   - Open **Command Prompt** and type:

ping [VPN server address]

   - Replace [VPN server address] with the actual VPN server hostname or IP (get this from your VPN documentation or ask your network team)
   - If ping fails, the VPN server may be unreachable from the user's network
3. Check if a firewall is blocking the VPN connection:
   - Corporate firewalls, hotel Wi-Fi, coffee shop networks, and some ISPs block VPN protocols
   - Try connecting from a different network (e.g., mobile hotspot) to isolate the issue
   - Check if the required VPN ports are open:
     - PPTP: TCP 1723
     - L2TP/IPSec: UDP 500, UDP 4500, ESP protocol
     - SSTP: TCP 443
     - OpenVPN: UDP 1194 or TCP 443
     - IKEv2: UDP 500, UDP 4500
4. Temporarily disable the Windows Firewall or third-party firewall to test:
   - Settings > Privacy & Security > Windows Security > Firewall & network protection
   - Turn off firewall temporarily, test VPN, then turn firewall back on immediately
   - If VPN works with firewall off, add a firewall exception for the VPN client

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
   - An incorrect VPN server address or protocol will result in authentication failures, often with misleading error messages about credentials.

### Step 4: Flush DNS and Reset Network Stack

1. A corrupted DNS cache or network configuration can interfere with VPN authentication
2. Open **Command Prompt as Administrator** (Win + X > Terminal (Admin))
3. Run the following commands one by one, pressing Enter after each:

ipconfig /flushdns
netsh int ip reset
netsh winsock reset

4. Also release and renew the IP address:

ipconfig /release
ipconfig /renew

5. Restart the computer after running these commands
6. After restart, try the VPN connection again before opening any other applications
   - This clears any DNS issues that might prevent the VPN client from reaching the authentication server, even though the internet appears to be working.

### Step 5: Clear Saved VPN Credentials in Windows Credential Manager

1. VPN clients often store credentials in Windows Credential Manager, and these can become corrupted
2. Open **Credential Manager**:
   - Type "Credential Manager" in the Start menu search
   - Or Control Panel > User Accounts > Credential Manager
3. Click **"Windows Credentials"**
4. Scroll through the list and look for any entries related to your VPN:
   - Entries may be named with the VPN server address, VPN connection name, or "Microsoft VPN"
   - Look under both "Generic Credentials" and "Windows Credentials"
5. Click the arrow next to the VPN credential > **"Remove"**
6. Also check "Generic Credentials" for any saved VPN-related entries and remove them
7. Close Credential Manager and restart the computer
8. After restart, open the VPN client and enter credentials fresh
9. When prompted, choose to save credentials if you want them stored again
   - Corrupted stored credentials are a common cause of repeated authentication failures after a password change.

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
   - A corrupted VPN client installation can cause authentication failures that are indistinguishable from credential errors; reinstallation is often quicker than extended troubleshooting.

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
4. If the user is locked out of MFA entirely, escalate to the Identity and Access Management team
   - MFA timeouts or missing prompts are often misinterpreted as credential errors; always verify the MFA flow.

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

## Escalation Criteria

Escalate to Tier 2 / Network Team if:

- VPN server is unreachable (ping fails from multiple networks) — possible server outage
- Multiple users report the same authentication failure simultaneously — likely server-side issue
- User's VPN account has been locked, disabled, or expired — requires account administration
- MFA reset needed (user got a new phone, lost access to authenticator app) — requires Identity team
- All troubleshooting steps above have been attempted and the issue persists
- VPN certificate on the client or server may have expired — requires certificate management
- User requires a new VPN account or access that must be provisioned by the network security team
- Suspicion of account compromise — follow security incident procedures

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

For internal use. Follow your organization's VPN and security policies.
