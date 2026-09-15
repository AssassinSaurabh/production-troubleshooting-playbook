# Troubleshooting Methodology

Every investigation in this playbook follows a single disciplined sequence. No exceptions.

```
Detect → Scope → Observe → Hypothesize → Test → Isolate → Mitigate → Verify → RCA → Prevent
```

---

## Step-by-Step

### 1. Detect
Something is wrong. An alert fired, a user reported an issue, or you observed anomalous behaviour.

**Do not act yet.** First confirm the symptom is real.

### 2. Scope
Determine the blast radius before touching anything.

- Is this one server or all servers?
- Is this one user, a region, or everyone?
- Which services, endpoints, or functions are affected?
- When did it start?
- What changed recently? (Deployments, config changes, infra changes)

### 3. Observe
Collect data from all available sources **without modifying system state**.

- Service health: `systemctl status`, `kubectl get pods`
- Ports and sockets: `ss -lntp`
- Logs: `journalctl`, application logs, LB access logs
- Metrics: CPU, memory, disk, network, error rates, latency
- Process table: `ps aux`, `top`

### 4. Hypothesize
Based on your observations, form a ranked list of possible causes.

Start with the most likely, most impactful hypothesis.

### 5. Test
Test **one hypothesis at a time**. Run a specific command or check that would confirm or deny it.

Do not change anything yet. Confirmation must precede action.

### 6. Isolate
Identify the single root component that is failing.

Stop when you can say: *"The failure is X, and here is the evidence."*

### 7. Mitigate
Apply the **safest, most reversible** action that restores service.

- Prefer `reload` over `restart`
- Prefer config rollback over patch
- Preserve evidence (logs, core dumps, process state) before acting

### 8. Verify
Recovery is not confirmed just because the process is running again.

Verify at every layer:
- Process state
- Socket/port listening
- Local HTTP probe
- External health check / synthetic monitor
- Metrics returned to baseline

### 9. Root Cause Analysis
After service is restored, determine the actual root cause.

Use **5 Whys** to get beyond the surface symptom. Write it down.

### 10. Prevent
What structural change would make this failure impossible or immediately detectable in the future?

- Pre-flight validation in CI/CD
- Automated rollback on canary failure
- Monitoring and alerting improvements
- Runbook updates
