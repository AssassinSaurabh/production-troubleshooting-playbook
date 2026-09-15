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

#R RunBooks
| ID  | Scenario | Runbook | Lab | Incident |
|-----|----------|---------|-----|----------|
| 001 | [Nginx Web Service Down](runbooks/linux/service-down/runbook.md) | Done |

## Core Principle

Do not restart first. Understand the failure first.

---

## Docs

- [Troubleshooting Methodology](docs/troubleshooting-methodology.md)
- [Incident Response Guide](docs/incident-response.md)
- [Severity and Prioritization](docs/severity-and-prioritization.md)
- [Observability Basics](docs/observability-basics.md)
