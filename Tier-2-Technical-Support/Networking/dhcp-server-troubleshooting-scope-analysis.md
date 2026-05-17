# DHCP Server Troubleshooting & Scope Analysis

- **Category:** Networking
- **Tier:** Tier 2 (Technical Support)
- **Version:** 1.0
- **Last Updated:** May 18, 2026
- **Last Reviewed:** May 18, 2026
- **Applies To:** Windows Server 2016, 2019, 2022, DHCP Server Role
- **Difficulty:** L2 (Intermediate)
- **Estimated Resolution Time:** 20-45 minutes
- **Required Access Level:** Administrator
- **Severity:** P1 (Multi-User, Critical — Network Access Failure)
- **Keywords:** DHCP, scope, lease, IP address, exhaustion, relay, failover, 169.254, APIPA
- **Prerequisite Knowledge:** Active Directory, DHCP Server management, PowerShell networking, basic network subnetting

---

## Symptoms

- Multiple users report inability to obtain IP addresses (169.254.x.x APIPA addresses)
- New devices cannot connect to the network but existing devices work normally
- DHCP scope shows "Full" or very few available addresses
- DHCP server event logs show errors (Event ID 1046, 1059, 20012)
- Intermittent IP address conflicts reported by users
- DHCP failover partnership shows "Communication interrupted" or "Conflict"
- Specific VLANs or subnets affected while others work normally

---

## Common Error Codes

| Code | Meaning |
|------|---------|
| Event ID 1046 | DHCP server not authorized in Active Directory |
| Event ID 1059 | DHCP service failed to initialize — database corruption |
| Event ID 20012 | Scope is 90% or more full — address pool nearly exhausted |
| Event ID 20291 | DHCP failover partnership lost — partner unreachable |
| 169.254.x.x | APIPA address — client failed to obtain DHCP lease |

---

## Symptom-to-Step Mapping

| If You See This | Skip To |
|-----------------|---------|
| Scope shows full or nearly full | Step 1 |
| DHCP server not handing out addresses | Step 2 |
| Failover partnership broken | Step 3 |
| Clients getting APIPA addresses on one subnet only | Step 4 |
| IP address conflicts occurring frequently | Step 5 |

---

## Triage Questions

Before starting troubleshooting, ask:

1. "How many users are affected? Is this one subnet, one building, or the entire organization?"
2. "When did the problem start? Was there a recent network change, server reboot, or maintenance?"
3. "Are existing devices still working, or is this affecting both new and existing connections?"
4. "Have you checked the DHCP console? What does the scope utilization show?"

---

## Quick Checks (30 seconds)

1. Open DHCP Management Console (dhcpmgmt.msc) — check if the DHCP server is authorized (green checkmark)
2. Check DHCP Server service status: Get-Service dhcpserver
3. Review scope statistics: right-click scope > "Display Statistics" — note % in use
4. Ping the DHCP server from an affected client — verify network connectivity
5. Check Event Viewer on the DHCP server for recent warnings or errors

---

## Step-by-Step Resolution

### Step 1: Analyze and Address Scope Exhaustion
1. Open DHCP Management Console > expand the server > expand IPv4
2. Right-click the affected scope > "Display Statistics"
3. Check "In Use" vs "Total" addresses — if usage exceeds 85%, the scope is nearly exhausted
4. Review lease duration: right-click scope > Properties > "Lease duration for DHCP clients"
   - Default is 8 days — if set too long, leases may not expire fast enough
   - For high-turnover networks (guest Wi-Fi), reduce to 1-4 hours
5. Check for BAD_ADDRESS entries: expand "Address Leases" > sort by Unique ID
   - BAD_ADDRESS indicates IP conflicts — these addresses are marked as unusable
   - Delete BAD_ADDRESS entries after resolving conflicts
6. If the scope is genuinely full, options:
   - Expand the scope: right-click scope > Properties > increase the IP address range
   - Create a new scope for additional capacity
   - Reduce lease duration for faster turnaround
7. Verify scope options: right-click scope > "Scope Options"
   - Ensure 003 Router and 006 DNS Servers are configured correctly

**What to check:** A scope at 90%+ utilization will cause intermittent failures. Increasing the address range or reducing lease duration provides immediate relief while a longer-term solution is planned.

### Step 2: Verify DHCP Server Authorization and Service Health
1. In DHCP Management Console, verify the server shows a green checkmark (authorized)
   - If the server shows a red X, it is not authorized in Active Directory
   - Right-click the server > "Authorize" (requires Enterprise Admin privileges)
2. Check DHCP Server service:
