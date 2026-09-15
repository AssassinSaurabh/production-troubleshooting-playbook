# Contributing

All contributions follow the **3-pillar rule**:

```
FAILURE SCENARIO
      │
      ▼
   LAB (labs/)
"How to break it?"
      │
      ▼
 INVESTIGATION
      │
 ┌────┴────┐
 ▼         ▼
RUNBOOK  INCIDENT
"Respond" "Postmortem"
```

Every scenario must produce:
1. `runbooks/<domain>/<scenario>/runbook.md` — operational playbook, usable at 2 AM
2. `labs/<domain>/<id>-<scenario>/` — reproducible failure environment
3. `incidents/<id>-<scenario>/incident.md` — real or simulated postmortem

**Golden Rule:** Every runbook must enforce evidence collection *before* any restart or mitigation.

Use the templates in `templates/` for consistency.
