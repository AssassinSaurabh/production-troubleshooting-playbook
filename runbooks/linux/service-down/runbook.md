# RUNBOOK-001 — Web Service Down (Nginx)

**Service:** Nginx
**Owner:** SRE / DevOps
**Severity:** Based on customer impact
**Status:** Active

---

## 1. Purpose

Use this runbook when an Nginx web service is unavailable or not responding to HTTP/HTTPS requests.

The goal is to:

1. Establish the impact.
2. Identify where the failure is occurring.
3. Collect evidence before making changes.
4. Restore service safely.
5. Verify recovery.
6. Identify the root cause and prevent recurrence.

> **Rule:** Do not restart first. Understand the failure first.

---

## 2. Symptoms

Common symptoms:

* Website is unreachable.
* Health checks are failing.
* HTTP/HTTPS requests fail.
* Port `80` or `443` is not listening.
* Nginx is `inactive` or `failed`.
* Increased HTTP `5xx` errors.

Possible client errors:

```text
Connection refused
Connection timed out
502 Bad Gateway
503 Service Unavailable
```

Confirm the actual error before deciding on the cause.

---

## 3. Impact / Scope

Before making changes, determine:

* Is the entire website unavailable?
* Is only HTTP or HTTPS affected?
* Are all users affected?
* Is the problem limited to one server?
* When did the incident start?
* Was there a recent deployment or configuration change?

Record the incident start time and relevant monitoring information.

---

## 4. Investigation

### Step 1 — Test the service locally

```bash
curl -I http://localhost
```

Expected:

```text
HTTP/1.1 200 OK
```

For HTTPS:

```bash
curl -k -I https://localhost
```

If the local request fails, continue investigating on the server.

---

### Step 2 — Check Nginx service state

```bash
systemctl status nginx
```

Or:

```bash
systemctl is-active nginx
```

Expected:

```text
active
```

Possible states:

```text
active
inactive
failed
activating
deactivating
```

If Nginx is `inactive` or `failed`, investigate the reason before restarting.

---

### Step 3 — Check listening ports

HTTP:

```bash
ss -lntp | grep :80
```

HTTPS:

```bash
ss -lntp | grep :443
```

Expected:

```text
LISTEN ... :80 ...
```

If Nginx is active but the expected port is not listening, check the configuration and process state.

---

### Step 4 — Check logs

Nginx service logs:

```bash
sudo journalctl -u nginx --since "10 minutes ago"
```

Look for:

* startup failures
* configuration errors
* permission errors
* port conflicts
* unexpected termination
* dependency failures

Nginx error log:

```bash
sudo tail -n 100 /var/log/nginx/error.log
```

Nginx access log:

```bash
sudo tail -n 100 /var/log/nginx/access.log
```

---

### Step 5 — Validate configuration

```bash
sudo nginx -t
```

Expected:

```text
syntax is ok
test is successful
```

If validation fails, **do not repeatedly restart Nginx**.

Fix or roll back the configuration first.

---

## 5. Decision Tree

```text
                  Website unavailable
                           |
                           v
                    curl localhost
                           |
                  +--------+--------+
                  |                 |
                FAIL              SUCCESS
                  |                 |
                  v                 v
             Check Nginx       Nginx healthy
                state            locally
                  |                 |
             +----+----+            v
             |         |       Check external
          failed      active     connectivity
             |         |              |
             v         v              v
          Check      Check       DNS / Network /
           logs       port       Firewall / LB
             |
             v
        Check config
             |
             v
       Identify cause
             |
             v
       Safe mitigation
             |
             v
        Verify recovery
```

---

## 6. Common Failure Scenarios

### Scenario A — Nginx is stopped

Check:

```bash
systemctl is-active nginx
```

If `inactive` and port `80` is not listening, check logs first:

```bash
sudo journalctl -u nginx -n 100
```

Then validate configuration:

```bash
sudo nginx -t
```

If configuration is valid and no underlying issue is present:

```bash
sudo systemctl start nginx
```

Verify:

```bash
systemctl is-active nginx
curl -I http://localhost
```

---

### Scenario B — Nginx failed to start

Check:

```bash
systemctl status nginx
sudo journalctl -u nginx -n 100
sudo nginx -t
```

Find and fix the underlying problem before attempting another restart.

---

### Scenario C — Nginx is active but port 80 is not listening

Check:

```bash
ss -lntp
sudo nginx -T
```

Check whether Nginx is configured to listen on the expected address and port.

Check for another process using the port:

```bash
sudo ss -lntp | grep :80
```

---

### Scenario D — Nginx works locally but users cannot access it

If `curl -I http://localhost` succeeds but users cannot connect, the failure is outside Nginx:

```text
Client
  ↓
DNS
  ↓
Network
  ↓
Firewall / Security Group
  ↓
Load Balancer
  ↓
Server
  ↓
Nginx
```

Do not restart Nginx without evidence that Nginx is the problem.

---

## 7. Safe Mitigation

If Nginx is confirmed stopped:

```bash
sudo systemctl start nginx
```

If configuration changed:

```bash
sudo nginx -t
sudo systemctl reload nginx
```

Prefer `reload` over `restart` when applying a valid configuration change.

If Nginx repeatedly crashes, stop treating restart as the fix. Investigate the underlying cause.

---

## 8. Verification

Recovery is not confirmed just because the Nginx process is running.

### Service

```bash
systemctl is-active nginx
```

### Port

```bash
ss -lntp | grep :80
```

### HTTP response

```bash
curl -I http://localhost
```

### Logs

```bash
sudo journalctl -u nginx --since "5 minutes ago"
```

### Monitoring

Confirm:

* Health checks are passing.
* HTTP error rate has returned to normal.
* Latency has returned to normal.
* Traffic is reaching the service.

---

## 9. Root Cause Analysis

After recovery, determine:

### What happened?

> Nginx was inactive, so nothing was accepting connections on port 80.

### Why did it happen?

Check whether Nginx:

* was manually stopped
* crashed
* failed during startup
* had a configuration error
* experienced a resource problem (OOM kill, disk full)
* encountered a port conflict
* was affected by a deployment or configuration change

### Why wasn't it detected earlier?

Check:

* service monitoring coverage
* HTTP health check interval
* alerting thresholds
* log monitoring

### How do we prevent it?

* HTTP health checks with short intervals.
* Systemd service restart policy (`Restart=on-failure`).
* Configuration validation (`nginx -t`) in CI/CD pipelines.
* Automated rollback on deployment health check failure.
* Resource monitoring (disk, memory) with pre-emptive alerts.

---

## 10. Evidence Preservation

Collect before making any changes:

```bash
systemctl status nginx
systemctl is-active nginx
ss -lntp
sudo journalctl -u nginx --since "30 minutes ago"
sudo nginx -t
sudo tail -n 100 /var/log/nginx/error.log
```

---

## 11. Interview Explanation

### 30-second answer

> "If a web service is reported as down, I establish scope and impact first rather than immediately restarting. I test locally with curl, check the service state and listening ports, and inspect logs. If Nginx is confirmed stopped and the evidence supports it, I start the service and then verify at every layer: process, port, HTTP response, and user-facing health checks. After recovery, I investigate root cause and put preventive measures in place."

### Would you restart the service?

> "Only after establishing that Nginx is the actual failure point and I understand why it stopped. A restart may restore availability but can hide the underlying problem and destroy evidence. I would use the safest reversible action while preserving logs and state for the postmortem."

---

## 12. Key Commands

```bash
# Test HTTP
curl -I http://localhost
curl -k -I https://localhost

# Service state
systemctl status nginx
systemctl is-active nginx

# Listening ports
ss -lntp
ss -lntp | grep :80
ss -lntp | grep :443

# Service logs
sudo journalctl -u nginx --since "10 minutes ago"
sudo journalctl -u nginx -n 100

# Configuration validation
sudo nginx -t

# Full configuration dump
sudo nginx -T

# Error log
sudo tail -n 100 /var/log/nginx/error.log

# Access log
sudo tail -n 100 /var/log/nginx/access.log

# Start service
sudo systemctl start nginx

# Reload configuration (preferred over restart)
sudo systemctl reload nginx
```

---

## 13. Troubleshooting Principle

> **Don't restart first. Understand first.**

```text
SYMPTOM → SCOPE → EVIDENCE → HYPOTHESIS → TEST → ISOLATE → MITIGATE → VERIFY → RCA → PREVENT
```

Keep this runbook updated when new failure modes are discovered.
