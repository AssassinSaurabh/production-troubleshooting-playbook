# LAB-XXX — [Lab Title]

**Domain:** [Linux / Networking / Docker / Kubernetes / AWS]
**Scenario:** [e.g. Service Crash, Port Conflict, DNS Failure]
**Target Runbook:** [`runbooks/<domain>/<scenario>/runbook.md`]()

---

## Objective

What this lab reproduces and what you will learn by completing it.

---

## Prerequisites

- Environment: Docker / Linux VM (Ubuntu 22.04)
- Tools: `curl`, `ss`, `journalctl`
- Estimated time: ~20 minutes

---

## Setup — Bring Up Healthy Baseline

```bash
# Commands to start the healthy environment
```

Verify healthy state:
```bash
curl -I http://localhost:8080
```

---

## Break It — Inject the Failure

```bash
# Command to inject the failure
```

---

## Expected Symptoms

- What `curl` returns after breaking
- What logs show
- What service state reports

---

## Investigation Exercise

Work through the failure using the associated runbook. Answer:
1. What does the local probe tell you?
2. Is the service running?
3. Is the port listening?
4. What do the logs say?
5. What is the root cause?

---

## Solution

Step-by-step recovery commands.

---

## Cleanup

```bash
# Tear down the lab environment
```
