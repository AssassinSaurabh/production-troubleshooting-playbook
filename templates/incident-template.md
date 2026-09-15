# Incident Postmortem #XXX — [Title]

**Date:** YYYY-MM-DD
**Severity:** [SEV-1 / SEV-2 / SEV-3]
**Duration:** XX minutes (Detection → Mitigation)
**Impact:** [% users affected / service degraded]
**Incident Commander:** [Name]
**Associated Runbook:** [`runbooks/...`]()

---

## Executive Summary

2-3 sentences: what broke, who was affected, root cause, how it was fixed.

---

## Timeline (UTC)

| Time  | Event |
|-------|-------|
| HH:MM | Alert fired |
| HH:MM | Investigation started |
| HH:MM | Root cause identified |
| HH:MM | Mitigation applied |
| HH:MM | Service verified healthy |

---

## Symptoms Observed

- Client symptoms (what errors users saw)
- Internal metrics (what changed in graphs)
- Log entries (key error lines)

---

## Hypothesis Testing

### Hypothesis 1: [Theory]
- **Test:** What command/check was run
- **Evidence:** What it returned
- **Conclusion:** Confirmed / Rejected

### Hypothesis 2: [Theory]
- **Test:**
- **Evidence:**
- **Conclusion:**

---

## Root Cause (5 Whys)

1. Why did the service fail?
2. Why did that happen?
3. Why wasn't it caught earlier?
4. Why did alerting take X minutes?
5. Why does this failure mode exist at all?

---

## Mitigation

What was done to restore service, step by step.

---

## Lessons Learned

### What went well
-

### What went wrong
-

---

## Action Items

| Action | Type | Owner | Target Date |
|--------|------|-------|-------------|
| [Preventive action] | Prevention | [Team] | [Date] |
| [Monitoring improvement] | Observability | [Team] | [Date] |
