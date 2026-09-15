# RUNBOOK-XXX — [Service / Failure Scenario]

**Service:** [e.g. Nginx / PostgreSQL / kube-dns]
**Owner:** [SRE / DevOps / Platform]
**Severity:** [SEV-1 / SEV-2 / SEV-3]
**Status:** [Draft / Active / Deprecated]

---

## 1. Purpose

What this runbook covers and what the engineer will achieve by following it.

> **Rule:** Do not restart first. Understand the failure first.

---

## 2. Symptoms

- Observable failures (HTTP errors, connection failures, health check status)
- Alerts that typically fire
- Client-facing error messages

---

## 3. Impact & Scope

Questions to determine blast radius before touching anything:
- Is this one instance or fleet-wide?
- Which users / traffic cohorts are affected?
- When did it start? What changed?

---

## 4. Investigation

### Step 1: Test the endpoint
```bash
curl -I http://localhost
```

### Step 2: Check service state
```bash
systemctl status <service>
systemctl is-active <service>
```

### Step 3: Check listening ports
```bash
ss -lntp | grep :<port>
```

### Step 4: Inspect logs
```bash
journalctl -u <service> --since "10 minutes ago"
tail -n 100 /var/log/<service>/error.log
```

### Step 5: Validate configuration
```bash
<service> -t
```

---

## 5. Decision Tree

```text
          Service Degraded / Down
                   │
                   ▼
            Triage Check
                   │
          ┌────────┴────────┐
        FAIL             SUCCESS
          │                 │
          ▼                 ▼
    Check Service     Locally healthy
       State         Check external path
          │          (LB / DNS / Firewall)
     ┌────┴────┐
  STOPPED   RUNNING
     │         │
     ▼         ▼
   Check     Check
   Logs     Ports / Config
```

---

## 6. Common Scenarios

### Scenario A: Service stopped
### Scenario B: Service failed to start
### Scenario C: Service running, port not listening
### Scenario D: Service healthy locally, users cannot reach it

---

## 7. Safe Mitigation

Apply only after identifying the cause.

```bash
# If service is stopped and config is valid
sudo systemctl start <service>

# If config changed
sudo <service> -t && sudo systemctl reload <service>
```

---

## 8. Verification

```bash
systemctl is-active <service>
ss -lntp | grep :<port>
curl -I http://localhost
journalctl -u <service> --since "5 minutes ago"
```

Also verify: health checks passing, error rate back to baseline, traffic flowing.

---

## 9. Root Cause Analysis

- What happened?
- Why did it happen?
- Why wasn't it detected earlier?
- How do we prevent it?

---

## 10. Key Commands

```bash
# Add the most useful commands for this scenario
```

---

## 11. Escalation

- Primary: SRE On-call
- Secondary: [App/Platform Team]

---

## 12. Interview Questions

**30-second answer:**
> [Fill in the concise, confident answer an engineer would give in an interview]

**Why not restart immediately?**
> [Explain evidence-first discipline]
