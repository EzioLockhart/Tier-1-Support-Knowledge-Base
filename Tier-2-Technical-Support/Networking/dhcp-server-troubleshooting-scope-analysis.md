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
   Get-Service dhcpserver | Format-List Name, Status, StartType
3. If the service is stopped, start it:
   Start-Service dhcpserver
   Set-Service dhcpserver -StartupType Automatic
4. Check for database corruption:
   - Navigate to C:\Windows\System32\dhcp
   - Verify dhcp.mdb file exists and is not 0 KB
   - Run DHCP database integrity check: jetpack dhcp.mdb temp.mdb
5. Restart the DHCP Server service after repairs:
   Restart-Service dhcpserver
6. Monitor event logs for 10-15 minutes after restart to confirm stability

**What to check:** An unauthorized or stopped DHCP server will not hand out addresses even if scopes are correctly configured. Database corruption can cause the service to fail silently.

### Step 3: Diagnose and Repair DHCP Failover Partnership
1. In DHCP Management Console, expand IPv4 > right-click the scope > "Properties" > "Failover" tab
2. Check partnership status:
   - "Normal" — partnership is healthy
   - "Communication interrupted" — servers cannot reach each other
   - "Conflict" — servers disagree on lease information
3. If "Communication interrupted":
   - Verify network connectivity between both DHCP servers (ping, tracert)
   - Check Windows Firewall: DHCP failover uses TCP port 647
   - Verify both servers are running the same DHCP Server version
4. If "Conflict":
   - Force replication: right-click scope > "Replicate Scope"
   - Or use PowerShell: Invoke-DhcpServerv4FailoverReplication -Name "FailoverPartnershipName" -Force
5. Review failover mode:
   - Load Balance (default) — both servers share the load
   - Hot Standby — one server is primary, the other is backup
6. If partnership cannot be repaired, delete and recreate:
   - Right-click scope > "Properties" > "Failover" > select partnership > "Delete"
   - Right-click scope > "Configure Failover" > follow the wizard

**What to check:** A broken failover partnership causes inconsistent lease information. Clients may receive IPs that conflict with other clients because the servers are not synchronizing.

### Step 4: Troubleshoot DHCP Relay and VLAN-Specific Issues
1. If only specific subnets or VLANs are affected, the DHCP relay agent is likely the issue
2. Verify DHCP relay configuration on the router or layer 3 switch for the affected VLAN:
   - Cisco: show ip helper-address
   - The helper address must point to the DHCP server's IP
3. Check that the DHCP relay is forwarding requests:
   - Run Wireshark on the DHCP server and filter for dhcp
   - Look for DHCP Discover packets from the affected subnet
   - If no Discover packets arrive, the relay agent is not forwarding
4. Verify the DHCP server has a scope configured for the affected subnet
   - The scope subnet must match the subnet of the VLAN
   - If there is no scope for that subnet, the server will ignore the relayed request
5. Check network ACLs or firewall rules between the affected VLAN and the DHCP server
   - DHCP uses UDP ports 67 (server) and 68 (client)
   - Ensure these ports are open bidirectionally

**What to check:** DHCP relay is often the culprit when a specific VLAN fails while others work. The relay agent must be correctly configured on the router or switch for each VLAN that needs DHCP.

### Step 5: Detect and Resolve IP Address Conflicts
1. IP conflicts cause BAD_ADDRESS entries in DHCP and prevent new leases
2. Identify conflicting devices:
   - Check DHCP server for BAD_ADDRESS entries
   - Review Event Viewer for Event ID 4199 (IP address conflict detected)
   - Use ping then arp -a to identify the conflicting MAC address
3. Common conflict causes:
   - Static IP assigned within DHCP scope range
   - Rogue DHCP server on the network
   - Device with cached IP from a different network
4. Detect rogue DHCP servers:
   Get-DhcpServerInDC
   - This lists all authorized DHCP servers in the domain
   - Any DHCP server not on this list is rogue
5. For static IP conflicts, either:
   - Move the static device outside the DHCP scope range
   - Add a reservation for the device in DHCP
6. Enable conflict detection on the DHCP server:
   - Right-click server > Properties > "Advanced" tab
   - Set "Conflict detection attempts" to 1 or 2
   - The server will ping an address before offering it to a client

**What to check:** A single static IP within the DHCP scope can cause cascading failures as the DHCP server keeps trying to assign that address and marking it as BAD_ADDRESS.

### Step 6: Verify DNS Dynamic Updates and Scavenging
1. DHCP can register DNS records on behalf of clients — failures here cause name resolution issues
2. Right-click scope > Properties > "DNS" tab
3. Verify "Enable DNS dynamic updates" is checked
4. Check the DHCP server's DNS registration credentials:
   - Right-click the server > "Properties" > "Advanced" tab > "Credentials"
   - The service account needs permissions to update DNS records
5. Check DNS scavenging is working:
   - Old DHCP leases may leave stale DNS records
   - In DNS Manager, verify scavenging is enabled on the zone
   - Stale records can cause name resolution to point to wrong IPs
6. Force DHCP to re-register DNS:
   Get-DhcpServerv4Lease -ScopeId <scope> | Register-DhcpServerv4Lease

---

## Alternative Solutions

If the above steps do not resolve the issue, also try:

- Restoring the DHCP database from backup: C:\Windows\System32\dhcp\backup\
- Migrating the DHCP role to a different server if the current server has persistent issues
- Increasing the number of conflict detection attempts to 3 for high-conflict environments
- Setting up SNMP monitoring for DHCP scope utilization to catch exhaustion before it happens

---

## Prevention Tips

- Monitor scope utilization weekly — set alerts at 70% and 85% thresholds
- Set lease durations appropriately for each network type (shorter for guest, longer for office)
- Document all static IP assignments outside DHCP scopes
- Regularly review and clean BAD_ADDRESS entries
- Test DHCP failover at least quarterly
- Keep DHCP database backed up — Windows backs up every 60 minutes by default

---

## Root Cause

Common causes of DHCP failures, in order of likelihood:

- Scope exhaustion — no available IP addresses for new clients (most common)
- DHCP server service stopped or unauthorized
- DHCP failover partnership broken or in conflict state
- DHCP relay agent misconfigured on router for specific VLANs
- IP address conflicts from static assignments within scope range
- Rogue DHCP server operating on the network
- DHCP database corruption
- DNS dynamic update failures causing stale records

---

## Escalation Decision Matrix

| Condition | Action |
|-----------|--------|
| All 6 steps completed, issue persists | Escalate to Tier 3 |
| Scope exhaustion requires network redesign | Escalate — architecture change |
| Rogue DHCP server detected and cannot be located | Escalate — network security incident |
| DHCP database corrupted and backup also fails | Escalate — requires database recovery |
| Failover partnership repeatedly breaks | Escalate — possible server hardware or OS issue |
| Multiple scopes across multiple servers affected | Escalate — possible domain-wide issue |
| Scope expanded or lease duration adjusted — issue resolved | Do not escalate — document change |

---

## Related Articles

- [No Internet Access (Limited Connectivity)](../../Tier-1-Help-Desk/Networking/no-internet-access.md) — Tier 1: End-user connectivity troubleshooting
- [Network Packet Capture & Analysis with Wireshark](../Tier-3-Expert-Engineering/network-packet-analysis-wireshark.md) — Tier 3: Expert packet analysis

> **Note:** The Tier 3 article is planned for future creation.

---

## FAQ

**Q: Why are clients getting 169.254.x.x addresses?**
**A:** This is an APIPA (Automatic Private IP Addressing) address. It means the client cannot reach the DHCP server. Check network connectivity, DHCP relay configuration, and that the DHCP server service is running.

**Q: How do I find which device has a static IP conflicting with DHCP?**
**A:** Ping the conflicting IP, then run arp -a to get the MAC address. Look up the MAC address in your switch's MAC table or use a MAC vendor lookup tool to identify the device manufacturer.

**Q: What is the difference between Load Balance and Hot Standby failover modes?**
**A:** Load Balance shares the DHCP load between two servers (each handles roughly 50% of clients). Hot Standby has one active server and one standby that takes over only if the primary fails. Choose Load Balance for redundancy with efficiency; Hot Standby for simpler failover.

---

## PowerShell Commands Quick Reference

| Command | Purpose |
|---------|---------|
| Get-Service dhcpserver | Check DHCP Server service status |
| Restart-Service dhcpserver | Restart DHCP Server service |
| Get-DhcpServerv4ScopeStatistics | Show scope utilization |
| Get-DhcpServerInDC | List all authorized DHCP servers |
| Invoke-DhcpServerv4FailoverReplication | Force failover replication |
| Get-DhcpServerv4Lease -ScopeId [scope] | View all leases in a scope |
| jetpack dhcp.mdb temp.mdb | Repair DHCP database |

---

## Was this article helpful?

If this article helped resolve your issue, great. If something was unclear, missing, or did not work, please open a GitHub Issue describing the problem so we can improve it.

Suggest improvements at: https://github.com/EzioLockhart/Complete-IT-Support-Knowledge-Base-Tier-0-to-Tier-3/issues

---

## References

- CompTIA A+ Troubleshooting Methodology: Identify the problem, Establish a theory, Test the theory, Establish a plan of action, Verify functionality, Document findings
- ITIL Incident Management best practices: Network services affecting multiple users require priority escalation
- Microsoft official documentation: DHCP Server troubleshooting

---

*Tier: Tier 2 (Technical Support) | Difficulty: L2 (Intermediate) | Estimated Resolution Time: 20-45 minutes | Required Access Level: Administrator | Severity: P1 (Multi-User Critical)*

---

For internal use. Follow your organization's network change management and DHCP administration policies.
