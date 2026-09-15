# Incident Response Guide

---

## Severity Levels

| Severity | Definition | Response Time | Example |
|----------|------------|---------------|---------|
| **SEV-1** | Complete outage. Core revenue or user path fully down. | Immediate, wake up on-call | Production API returning 0% success |
| **SEV-2** | Significant degradation or partial outage. Redundancy lost. | < 15 minutes | Single-AZ failure, 50% traffic affected |
| **SEV-3** | Minor impact. Degraded performance with workaround available. | < 1 hour | Increased latency, non-critical feature broken |
| **SEV-4** | Minimal impact. Internal tool, cosmetic, no user effect. | Next business day | Dashboard slow to load |

---

## Incident Lifecycle

```
Alert Fires
    │
    ▼
Acknowledge (stop the pager, own it)
    │
    ▼
Scope (who / what / when is affected?)
    │
    ▼
Investigate (evidence before action)
    │
    ▼
Mitigate (safest reversible action)
    │
    ▼
Verify (all layers confirmed healthy)
    │
    ▼
Declare Resolved
    │
    ▼
Postmortem (within 48-72 hours)
```

---

## On-Call Responsibilities

1. **Acknowledge** the alert within the SLA window.
2. **Communicate** in the incident channel. Post the first update within 5 minutes of joining.
3. **Scope before acting.** Never apply a fix without understanding the blast radius.
4. **Preserve evidence.** Capture logs, metrics, and process state before restarts.
5. **Escalate early.** It is better to page someone unnecessarily than to miss the window for recovery.
6. **Declare mitigation** clearly when the service is verified healthy — not just when the process is up.
7. **Write the postmortem.** Every SEV-1 and SEV-2 gets a postmortem.

---

## Communication Templates

### Initial incident broadcast
```
[INCIDENT-XXX] SEV-X | [Service Name] degraded / unavailable
Time detected: HH:MM UTC
Impact: [what and who is affected]
Current status: Investigating
IC: [Name]
Updates: every 10 minutes or on change
```

### Mitigation announcement
```
[INCIDENT-XXX] MITIGATED
Time of recovery: HH:MM UTC
Duration: XX minutes
Action taken: [brief description]
Monitoring: next 30 minutes
Postmortem: [link when published]
```

---

## Evidence Preservation

Before restarting or modifying anything, capture:

```bash
# System state
uptime && free -h && df -h

# Service state
systemctl status <service>
journalctl -u <service> --since "30 minutes ago" > /tmp/service-incident-$(date +%s).log

# Process table
ps aux > /tmp/ps-incident-$(date +%s).log

# Ports
ss -lntp > /tmp/ss-incident-$(date +%s).log
```

Evidence collected during the incident is the foundation of the postmortem.
