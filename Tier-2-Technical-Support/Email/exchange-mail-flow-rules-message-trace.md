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
1. Go to Exchange Admin Center > Mail flow > Message trace
2. Click "Start a trace"
3. Select date range (default is past 48 hours; extend to 7 days if needed)
4. Enter the sender or recipient email address
5. Click "Search"
6. Review results:
   - Delivered: Email was successfully delivered — check recipient's Junk folder or inbox rules
   - Failed: Email was blocked or rejected — click the entry for the failure reason and NDR code
   - Pending: Email is still being processed — may indicate queue backlog
   - Quarantined: Email was sent to quarantine — check Quarantine in Exchange Admin Center
   - Unknown: No record found — email may never have reached Exchange
7. If using PowerShell:
   Get-MessageTrace -SenderAddress user@domain.com -StartDate (Get-Date).AddDays(-2) -EndDate (Get-Date)
   For detailed trace with event information:
   Get-MessageTrace -SenderAddress user@domain.com | Get-MessageTraceDetail

**What to check:** Message trace shows exactly where an email went. If it shows "Delivered" but the user cannot find it, the issue is client-side (rules, Junk folder). If it shows "Failed", the reason code guides the next step.

### Step 2: Review and Troubleshoot Transport Rules (Mail Flow Rules)
1. Go to Exchange Admin Center > Mail flow > Rules
2. Review all enabled rules — pay special attention to rules that:
   - Block or reject messages based on sender, subject, or attachment
   - Redirect or forward messages to different recipients
   - Apply disclaimer text or modify message content
3. To test if a rule is causing the issue:
   - Temporarily disable the suspected rule
   - Send a test email that matches the rule's conditions
   - If the test email delivers, the rule was the cause
   - Modify the rule to add exceptions for legitimate senders
4. Check rule processing order:
   - Rules are processed in order (lowest priority number first)
   - A rule with priority 0 can block a message before it reaches rules with priority 1+
   - Review the rule priority numbers for conflicts
5. Use PowerShell to find rules affecting a specific sender:
   Get-TransportRule | Where-Object { $_.From -like "*domain.com*" -or $_.FromAddressContainsWords -like "*sender*" }

**What to check:** A single transport rule with overly broad conditions can block legitimate email across the organization. Rules created months ago may accidentally match new senders or domains.

### Step 3: Analyze Non-Delivery Reports (NDRs)
1. When an email fails, Exchange sends an NDR to the sender with diagnostic information
2. Key fields in the NDR:
   - Enhanced Status Code: e.g., 550 5.7.1 — identifies the exact failure reason
   - Diagnostic information: Technical details about which rule or policy blocked the message
   - Generating server: Which Exchange server generated the NDR
3. Common NDR codes and fixes:
   - 550 5.7.1 Unable to relay: Check connector authentication settings
   - 550 5.7.1 Sender denied: Sender is blocked by anti-spam policy or block list
   - 550 5.1.10 Recipient not found: Verify recipient address exists and is correct
   - 550 5.4.1 Relay access denied: Connector does not allow relaying for that sender
4. Use PowerShell to get detailed NDR information:
   Get-MessageTrace -RecipientAddress user@domain.com -Status Failed | Get-MessageTraceDetail | Format-List

**What to check:** The NDR's diagnostic information field often contains the specific transport rule name or policy that blocked the email. This is the fastest path to identifying the root cause.

### Step 4: Check and Resolve Mail Queue Backlogs
1. Go to Exchange Admin Center > Mail flow > Queues
2. Review queue status:
   - Submission queue: Messages being processed — high numbers indicate backlog
   - Active queues: Messages actively being delivered
   - Retry queues: Messages that failed and are scheduled for retry
   - Poison queues: Messages that caused transport service crashes
3. If queues show high message counts (thousands):
   - Check Exchange server resource usage (CPU, memory, disk)
   - Check back pressure status: Exchange throttles incoming mail when resources are low
   - Check for transport service errors in Event Viewer
4. Force queue processing:
   Get-Queue | Retry-Queue -Resubmit $true
5. Remove stuck messages from poison queue:
   Get-Message -Queue "Poison" | Remove-Message -Confirm:$false
6. Check queue database health:
   - Navigate to the queue database location (default: C:\Program Files\Microsoft\Exchange Server\V15\TransportRoles\data\Queue)
   - Check database size and disk free space

**What to check:** Queue backlogs are often caused by resource exhaustion (low disk space, high memory usage) or a downstream server that is offline. Check Event Viewer for transport service errors.

### Step 5: Validate Connectors and External Mail Flow
1. Go to Exchange Admin Center > Mail flow > Connectors
2. Review inbound and outbound connectors:
   - Verify connector status is "Enabled" and "Valid"
   - Check the connector's source and destination servers
   - Verify TLS/authentication settings match the partner's requirements
3. For outbound mail delivery issues:
   - Validate the outbound connector is selected for the affected domain
   - Check the connector's send connector smart host or MX record
   - Verify the sending IP is not on any external blocklists (mxtoolbox.com/blacklists)
4. For inbound mail delivery issues:
   - Validate your MX records are correct: nslookup -type=mx yourdomain.com
   - Verify your inbound connector is configured to accept mail from the expected sources
   - Check that your spam filter or gateway is not blocking the sender
5. Test mail flow using SMTP commands:
   telnet smtp.office365.com 25
   HELO yourdomain.com
   MAIL FROM: test@yourdomain.com
   RCPT TO: recipient@domain.com
   DATA
   Subject: Test
   This is a test.
   .
   QUIT

**What to check:** External mail delivery issues often trace back to connector misconfiguration, expired certificates, or your sending IP being blocklisted by the recipient's organization.

### Step 6: Review Anti-Spam Policies and Quarantine
1. Go to Exchange Admin Center > Email & collaboration > Policies & rules > Threat policies
2. Review Anti-spam policies:
   - Check spam confidence level (SCL) thresholds — if set too low, legitimate email may be marked as spam
   - Check allowed and blocked sender lists — verify the affected sender is not on the block list
   - Check international spam settings — some policies block email from specific countries
3. Review quarantine:
   - Go to Exchange Admin Center > Email & collaboration > Review > Quarantine
   - Search for the affected email by sender or recipient
   - If found, release the message and add the sender to the allowed list
4. Review tenant-level block lists:
   - Check if the sender's domain is on the tenant block list
   - Check if the sender's IP is on the connection filter block list
5. Check for third-party spam filters or gateways in front of Exchange that may be blocking the email

**What to check:** Anti-spam policies are the most common cause of "missing" external emails. Messages may be silently quarantined without sending an NDR to the sender.

---

## Alternative Solutions

If the above steps do not resolve the issue, also try:

- Enabling verbose logging on the affected connector for detailed SMTP logs
- Using Microsoft Remote Connectivity Analyzer (testconnectivity.microsoft.com) for inbound/outbound SMTP tests
- Checking for service health incidents in Microsoft 365 Admin Center
- Creating a bypass transport rule for the affected sender (temporary workaround while root cause is investigated)

---

## Prevention Tips

- Document all transport rules and their business purpose — review quarterly
- Set up alerts for queue growth and transport rule matches on unexpected patterns
- Regularly review connector configurations, especially after certificate renewals
- Maintain an allowed sender list for critical business partners to avoid anti-spam blocks
- Test mail flow to key external partners monthly using message trace
- Monitor NDR rates — a sudden increase indicates a configuration problem

---

## Root Cause

Common causes of mail flow issues, in order of likelihood:

- Transport rule blocking or redirecting legitimate email (most common)
- Anti-spam policy marking legitimate email as spam and quarantining it
- Recipient address typo or mailbox does not exist
- Connector misconfiguration or expired TLS certificate
- Sender's IP or domain on a block list
- Exchange server resource exhaustion causing queue backlog
- Third-party spam filter or gateway blocking email before Exchange

---

## Escalation Decision Matrix

| Condition | Action |
|-----------|--------|
| All 6 steps completed, issue persists | Escalate to Tier 3 |
| Email blocked by a rule created by another department | Escalate — coordinate rule modification with owner |
| Sending IP on external blocklist and cannot be delisted | Escalate — may require IP address change |
| Connector TLS certificate expired | Escalate — requires certificate renewal |
| Multiple tenants or organizations affected | Escalate — possible Microsoft 365 service incident |
| Anti-spam policy change resolves the issue | Do not escalate — document policy change |
| Transport rule identified and modified | Do not escalate — document rule change |

---

## Related Articles

- [Outlook Not Receiving New Emails](../../Tier-1-Help-Desk/Email/outlook-not-receiving-emails.md) — Tier 1: Client-side email troubleshooting
- [Unable to Send Emails (Stuck in Outbox)](../../Tier-1-Help-Desk/Email/unable-to-send-emails.md) — Tier 1: Client-side sending issues
- [SMTP Relay Architecture & Connector Diagnostics](../Tier-3-Expert-Engineering/smtp-relay-architecture.md) — Tier 3: Expert mail flow architecture

> **Note:** The Tier 3 article is planned for future creation.

---

## FAQ

**Q: How do I know if an email was actually delivered to the recipient's inbox?**
**A:** A "Delivered" status in message trace means Exchange handed the email to the recipient's mailbox. It does not guarantee the recipient saw it — the email could still be in Junk, moved by an inbox rule, or deleted by the user.

**Q: What is the difference between a transport rule and an anti-spam policy?**
**A:** Transport rules apply to messages based on conditions you define (sender, subject, attachment). Anti-spam policies use Microsoft's spam filtering algorithms to score and filter messages automatically. Transport rules are deterministic; anti-spam is probabilistic.

**Q: Can I recover an email that was blocked by a transport rule?**
**A:** No. If a rule is set to "Reject" or "Delete without notifying", the email is discarded and cannot be recovered. Use "Redirect" or "Quarantine" actions instead for scenarios where you may need to review blocked messages.

---

## PowerShell Commands Quick Reference

| Command | Purpose |
|---------|---------|
| Get-MessageTrace | Search for message delivery records |
| Get-MessageTraceDetail | Get detailed delivery event information |
| Get-TransportRule | List all mail flow rules |
| Disable-TransportRule "Rule Name" | Temporarily disable a rule |
| Get-Queue | View mail queue status |
| Retry-Queue -Resubmit $true | Force retry of queued messages |
| Get-QuarantineMessage | View quarantined messages |

---

## Was this article helpful?

If this article helped resolve your issue, great. If something was unclear, missing, or did not work, please open a GitHub Issue describing the problem so we can improve it.

Suggest improvements at: https://github.com/EzioLockhart/Complete-IT-Support-Knowledge-Base-Tier-0-to-Tier-3/issues

---

## References

- Microsoft official documentation: Message trace in Exchange Online
- Microsoft official documentation: Mail flow rules (transport rules)
- ITIL Incident Management: Email delivery is a critical business service

---

*Tier: Tier 2 (Technical Support) | Difficulty: L2 (Intermediate) | Estimated Resolution Time: 20-45 minutes | Required Access Level: Administrator | Severity: P1 (Multi-User Critical)*

---

For internal use. Follow your organization's Exchange administration and change management policies.
