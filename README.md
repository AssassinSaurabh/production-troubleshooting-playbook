# Production Troubleshooting & Incident Response Playbook

> A hands-on collection of production-grade runbooks, reproducible failure labs, and incident postmortems across Linux, Networking, Docker, Kubernetes, AWS, CI/CD, and Databases.

---

## What This Repository Demonstrates

- **Hypothesis-driven troubleshooting** — never guess, always test
- **Evidence-first discipline** — collect before you act
- **Structured incident response** — triage → investigate → mitigate → verify → RCA
- **Production-safe mitigation** — reversible actions, prefer reload over restart
- **Root cause analysis** — 5 Whys, not just "it's fixed"
- **Reproducible failure labs** — break it safely, learn by doing
- **Postmortem culture** — timeline, hypothesis log, action items

---

## Troubleshooting Methodology

```
Detect → Scope → Observe → Hypothesize → Test → Isolate → Mitigate → Verify → RCA → Prevent
```

Every runbook in this repo follows this exact sequence.

---

## Repository Architecture — The 3-Pillar System

```
                 FAILURE SCENARIO
                       │
                       ▼
                    LAB (labs/)
             "How do we break it?"
                       │
                       ▼
                INVESTIGATION
             "How did we debug it?"
                       │
             ┌─────────┴─────────┐
             ▼                   ▼
         RUNBOOK              INCIDENT
    (runbooks/)              (incidents/)
 "How to respond?"       "What happened?"
             │                   │
             └─────────┬─────────┘
                       ▼
               PRODUCTION KNOWLEDGE
```

| Pillar | Path | Purpose |
|--------|------|---------|
| **Runbook** | `runbooks/<domain>/<scenario>/` | Operational playbook — usable at 2 AM during an incident |
| **Lab** | `labs/<domain>/<id>-<scenario>/` | Reproducible failure environment — break it safely |
| **Incident** | `incidents/<id>-<scenario>/` | Postmortem — timeline, hypotheses, RCA, action items |

---

## Repository Structure

```text
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
│   │   └── service-down/          ← RUNBOOK-001 ✅
│   ├── networking/
│   ├── docker/
│   ├── kubernetes/
│   ├── aws/
│   ├── database/
│   └── cicd/
│
├── labs/
│   └── linux/
│       └── 001-service-down/      ← LAB-001 (coming soon)
│
└── incidents/
    └── 001-nginx-service-down/    ← INCIDENT-001 (coming soon)
```

---

## Runbook Index

### 🐧 Linux

| # | Scenario | Runbook | Lab | Incident |
|---|----------|---------|-----|----------|
| 001 | [Nginx Web Service Down](runbooks/linux/service-down/runbook.md) | ✅ | 🔜 | 🔜 |
| 002 | High CPU | 🔜 | 🔜 | 🔜 |
| 003 | High Memory | 🔜 | 🔜 | 🔜 |
| 004 | Disk Full | 🔜 | 🔜 | 🔜 |

### 🌐 Networking

| # | Scenario | Runbook | Lab | Incident |
|---|----------|---------|-----|----------|
| 005 | DNS Failure | 🔜 | 🔜 | 🔜 |
| 006 | Connection Refused | 🔜 | 🔜 | 🔜 |
| 007 | HTTP 502 Bad Gateway | 🔜 | 🔜 | 🔜 |

### 🐳 Docker

| # | Scenario | Runbook | Lab | Incident |
|---|----------|---------|-----|----------|
| — | Container Crash | 🔜 | 🔜 | 🔜 |
| — | Image Pull Failure | 🔜 | 🔜 | 🔜 |

### ☸️ Kubernetes

| # | Scenario | Runbook | Lab | Incident |
|---|----------|---------|-----|----------|
| — | CrashLoopBackOff | 🔜 | 🔜 | 🔜 |
| — | Pod Pending | 🔜 | 🔜 | 🔜 |
| — | ImagePullBackOff | 🔜 | 🔜 | 🔜 |

### ☁️ AWS

| # | Scenario | Runbook | Lab | Incident |
|---|----------|---------|-----|----------|
| — | EC2 Unreachable | 🔜 | 🔜 | 🔜 |
| — | ALB 503 | 🔜 | 🔜 | 🔜 |

---

## Progress Tracker

| Domain | Runbooks | Labs | Incidents |
|--------|----------|------|-----------|
| Linux | 1 / 7 | 0 / 7 | 0 / 7 |
| Networking | 0 / 7 | 0 / 7 | 0 / 7 |
| Docker | 0 / 4 | 0 / 4 | 0 / 4 |
| Kubernetes | 0 / 7 | 0 / 7 | 0 / 7 |
| AWS | 0 / 4 | 0 / 4 | 0 / 4 |
| CI/CD | 0 / 4 | 0 / 4 | 0 / 4 |
| Database | 0 / 3 | 0 / 3 | 0 / 3 |

---

## Core Principle

> **Do not restart first. Understand first.**

```
SYMPTOM → SCOPE → EVIDENCE → HYPOTHESIS → TEST → ISOLATE → MITIGATE → VERIFY → RCA → PREVENT
```

---

## Resume Description

> **Production Troubleshooting & Incident Response Playbook** — Built a hands-on troubleshooting repository covering Linux, Networking, Docker, Kubernetes, AWS and CI/CD, with reproducible failure labs, operational runbooks, incident timelines, root cause analysis, and preventive action tracking. Designed to reflect real SRE/DevOps on-call discipline.

---

*Built by [Saurabh Pandey](https://github.com/AssassinSaurabh) — adding one scenario at a time.*
