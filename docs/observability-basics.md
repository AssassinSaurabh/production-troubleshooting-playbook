# Observability Basics

Good troubleshooting depends on good observability. This document covers the mental models and signals used throughout this playbook.

---

## The Three Pillars of Observability

| Pillar | What it tells you | Tools |
|--------|------------------|-------|
| **Metrics** | What is happening (numbers over time) | Prometheus, Datadog, CloudWatch |
| **Logs** | What happened (event records) | Loki, ELK, journalctl, CloudWatch Logs |
| **Traces** | Where time was spent (request path) | Jaeger, Zipkin, AWS X-Ray |

Use all three. Metrics alert you, logs explain the event, traces show the path.

---

## The USE Method (Infrastructure / Resources)

For every resource (CPU, memory, disk, network), ask:

- **U**tilization — how busy is it? (%)
- **S**aturation — is it queueing work it can't process? (queue depth, wait time)
- **E**rrors — is it failing? (error count)

```bash
# CPU
top -bn1 | grep "Cpu(s)"
mpstat 1 5

# Memory
free -h
vmstat 1 5

# Disk
iostat -xz 1 5
df -h

# Network
ss -s
netstat -s
```

---

## The RED Method (Services / APIs)

For every service or endpoint, ask:

- **R**ate — how many requests per second?
- **E**rrors — what is the error rate? (%)
- **D**uration — what is the latency distribution? (p50, p95, p99)

---

## Signals to Check During Triage

| Signal | Command | What to look for |
|--------|---------|-----------------|
| Service state | `systemctl status <svc>` | `active (running)` vs `failed` |
| Port listening | `ss -lntp \| grep :<port>` | Socket bound and listening |
| HTTP probe | `curl -I http://localhost` | HTTP 200 OK |
| Recent logs | `journalctl -u <svc> --since "10 min ago"` | Errors, OOM kills, segfaults |
| System load | `uptime` | Load average vs CPU count |
| Memory pressure | `free -h` | Available memory, swap usage |
| Disk space | `df -h` | `/var/log`, `/tmp`, application paths |
| Process table | `ps aux --sort=-%cpu` | Runaway processes |

---

## Log Reading Strategy

1. Start with the **most recent errors** — `tail -n 100` or `--since "10 minutes ago"`.
2. Look for **ERROR**, **FATAL**, **CRITICAL**, **OOM**, **SIGSEGV**, **Connection refused**, **No space left**.
3. Establish a **timeline** — when did the first error appear?
4. Correlate with the **deployment and change window**.
