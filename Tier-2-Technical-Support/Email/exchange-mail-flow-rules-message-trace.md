# Exchange Mail Flow Rules & Message Trace

- **Category:** Email
- **Tier:** Tier 2 (Technical Support)
- **Version:** 1.0
- **Last Updated:** May 18, 2026
- **Last Reviewed:** May 18, 2026
- **Applies To:** Microsoft Exchange Online, Exchange Server 2016, 2019, Microsoft 365
- **Difficulty:** L2 (Intermediate)
- **Estimated Resolution Time:** 20-45 minutes
- **Required Access Level:** Administrator
- **Severity:** P1 (Multi-User, Critical — Email Delivery Failure)
- **Keywords:** Exchange, mail flow, transport rule, message trace, NDR, connector, queue, spam
- **Prerequisite Knowledge:** Exchange Admin Center, mail flow concepts, PowerShell basics, SMTP

---

## Symptoms

- Multiple users report emails not being delivered to specific recipients
- Emails from specific senders or domains consistently not arriving
- Non-Delivery Reports (NDRs) with error codes returned to senders
- Email delivery delays of 30+ minutes across the organization
- Messages stuck in submission queue or pending delivery
- External partners report not receiving emails from your organization
- Specific email subjects or attachment types consistently blocked

---

## Common Error Codes

| Code | Meaning |
|------|---------|
| 550 5.7.1 | Message rejected by transport rule or spam filter |
| 550 5.4.1 | Relay access denied — connector misconfiguration |
| 550 5.1.10 | Recipient not found — address does not exist |
| 451 4.7.500 | Server busy — throttling or back pressure |
| 550 5.7.511 | Access denied — message blocked by anti-spam policy |

---

## Symptom-to-Step Mapping

| If You See This | Skip To |
|-----------------|---------|
| Specific email missing for one user | Step 1 |
| Emails from a domain or sender blocked | Step 2 |
| NDR with specific error code | Step 3 |
| Messages stuck in queue | Step 4 |
| External email delivery failing | Step 5 |

---

## Triage Questions

Before starting troubleshooting, ask:

1. "Is this affecting one user, multiple users, or the entire organization?"
2. "Are emails failing to specific recipients, specific domains, or all external addresses?"
3. "When did this start? Was there a recent change to mail flow rules, connectors, or spam policies?"
4. "Do you have the NDR or bounce-back message with the error code?"

---

## Quick Checks (30 seconds)

1. Open Exchange Admin Center > Mail flow > Message trace
2. Search for the affected sender/recipient in the last 24 hours
3. Check the delivery status: Delivered, Failed, Pending, Quarantined
4. Review any active transport rules that may match the affected emails
5. Check connector status: Mail flow > Connectors — all should show "Enabled" and "Valid"

---

## Step-by-Step Resolution

### Step 1: Run a Message Trace to Find Missing Emails
1. Go to Exchange Admin Center > **Mail flow** > **Message trace**
2. Click "Start a trace"
3. Select date range (default is past 48 hours; extend to 7 days if needed)
4. Enter the sender or recipient email address
5. Click "Search"
6. Review results:
   - **Delivered:** Email was successfully delivered — check recipient's Junk folder or inbox rules
   - **Failed:** Email was blocked or rejected — click the entry for the failure reason and NDR code
   - **Pending:** Email is still being processed — may indicate queue backlog
   - **Quarantined:** Email was sent to quarantine — check Quarantine in Exchange Admin Center
   - **Unknown:** No record found — email may never have reached Exchange
7. If using PowerShell:
   ```powershell
   Get-MessageTrace -SenderAddress user@domain.com -StartDate (Get-Date).AddDays(-2) -EndDate (Get-Date)
