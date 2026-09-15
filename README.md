# Production Troubleshooting Playbook

A hands-on collection of production runbooks, failure labs, and incident postmortems.

Covers Linux, Networking, Docker, Kubernetes, AWS, CI/CD, and Databases.

---

## What This Is

This repository is built around real production failure scenarios. Each scenario produces three things:

1. **Runbook** — how to respond when the failure happens in production
2. **Lab** — how to reproduce the failure in a safe environment
3. **Incident** — a postmortem with timeline, investigation, root cause, and action items

---

## Troubleshooting Methodology

Every runbook follows the same sequence:

```
Detect > Scope > Observe > Hypothesize > Test > Isolate > Mitigate > Verify > RCA > Prevent
```

---

## Repository Structure

```
production-troubleshooting-playbook/
│
├── README.md
├── CONTRIBUTING.md
├── LICENSE
│
├── docs/
│   ├── troubleshooting-methodology.md
│   ├── incident-response.md
│   ├── severity-and-prioritization.md
│   └── observability-basics.md
│
├── templates/
│   ├── runbook-template.md
│   ├── lab-template.md
│   └── incident-template.md
│
├── runbooks/
│   ├── linux/
│   │   └── service-down/
│   │       └── runbook.md          ← RUNBOOK-001: Nginx Web Service Down
│   ├── networking/
│   ├── docker/
│   ├── kubernetes/
│   ├── aws/
│   ├── database/
│   └── cicd/
│
├── labs/
│   └── linux/
│       └── 001-service-down/       ← coming soon
│
├── incidents/
│   └── 001-nginx-service-down/     ← coming soon
│
├── diagrams/
└── scripts/
```

---

## Runbooks

### Linux

| ID  | Scenario | Runbook | Lab | Incident |
|-----|----------|---------|-----|----------|
| 001 | [Nginx Web Service Down](runbooks/linux/service-down/runbook.md) | Done | Pending | Pending |
| 002 | High CPU | Pending | Pending | Pending |
| 003 | High Memory | Pending | Pending | Pending |
| 004 | Disk Full | Pending | Pending | Pending |
| 005 | Filesystem Read-Only | Pending | Pending | Pending |
| 006 | Process Crash | Pending | Pending | Pending |
| 007 | Permission Denied | Pending | Pending | Pending |

### Networking

| ID  | Scenario | Runbook | Lab | Incident |
|-----|----------|---------|-----|----------|
| 008 | DNS Failure | Pending | Pending | Pending |
| 009 | Connection Refused | Pending | Pending | Pending |
| 010 | Connection Timeout | Pending | Pending | Pending |
| 011 | Packet Loss | Pending | Pending | Pending |
| 012 | HTTP 502 | Pending | Pending | Pending |
| 013 | HTTP 503 | Pending | Pending | Pending |
| 014 | HTTP 504 | Pending | Pending | Pending |

### Docker

| ID  | Scenario | Runbook | Lab | Incident |
|-----|----------|---------|-----|----------|
| 015 | Container Crash | Pending | Pending | Pending |
| 016 | Image Pull Failure | Pending | Pending | Pending |
| 017 | Container Networking | Pending | Pending | Pending |
| 018 | Volume Permission | Pending | Pending | Pending |

### Kubernetes

| ID  | Scenario | Runbook | Lab | Incident |
|-----|----------|---------|-----|----------|
| 019 | Pod Pending | Pending | Pending | Pending |
| 020 | CrashLoopBackOff | Pending | Pending | Pending |
| 021 | ImagePullBackOff | Pending | Pending | Pending |
| 022 | Service No Endpoints | Pending | Pending | Pending |
| 023 | DNS Failure | Pending | Pending | Pending |
| 024 | Ingress 502 | Pending | Pending | Pending |
| 025 | NetworkPolicy Block | Pending | Pending | Pending |

### AWS

| ID  | Scenario | Runbook | Lab | Incident |
|-----|----------|---------|-----|----------|
| 026 | EC2 Unreachable | Pending | Pending | Pending |
| 027 | ALB 503 | Pending | Pending | Pending |
| 028 | S3 Access Denied | Pending | Pending | Pending |
| 029 | Private Subnet Connectivity | Pending | Pending | Pending |

### Database

| ID  | Scenario | Runbook | Lab | Incident |
|-----|----------|---------|-----|----------|
| 030 | Connection Exhaustion | Pending | Pending | Pending |
| 031 | Slow Query | Pending | Pending | Pending |
| 032 | Replication Lag | Pending | Pending | Pending |

### CI/CD

| ID  | Scenario | Runbook | Lab | Incident |
|-----|----------|---------|-----|----------|
| 033 | Build Failure | Pending | Pending | Pending |
| 034 | Image Push Failure | Pending | Pending | Pending |
| 035 | Deployment Failure | Pending | Pending | Pending |
| 036 | Rollback | Pending | Pending | Pending |

---

## Coverage

| Domain | Runbooks | Labs | Incidents |
|--------|----------|------|-----------|
| Linux | 1 / 7 | 0 / 7 | 0 / 7 |
| Networking | 0 / 7 | 0 / 7 | 0 / 7 |
| Docker | 0 / 4 | 0 / 4 | 0 / 4 |
| Kubernetes | 0 / 7 | 0 / 7 | 0 / 7 |
| AWS | 0 / 4 | 0 / 4 | 0 / 4 |
| Database | 0 / 3 | 0 / 3 | 0 / 3 |
| CI/CD | 0 / 4 | 0 / 4 | 0 / 4 |

---

## Core Principle

Do not restart first. Understand the failure first.

---

## Docs

- [Troubleshooting Methodology](docs/troubleshooting-methodology.md)
- [Incident Response Guide](docs/incident-response.md)
- [Severity and Prioritization](docs/severity-and-prioritization.md)
- [Observability Basics](docs/observability-basics.md)
