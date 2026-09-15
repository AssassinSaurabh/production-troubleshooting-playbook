# Severity and Prioritization

---

## Triage Matrix

When multiple issues surface simultaneously, use this matrix to decide what to work on first.

| Impact ↓ / Urgency → | High Urgency | Low Urgency |
|----------------------|-------------|------------|
| **High Impact** | SEV-1 / SEV-2 — Act immediately | SEV-2 / SEV-3 — Schedule urgently |
| **Low Impact** | SEV-3 — Address soon | SEV-4 — Backlog |

---

## Determining Impact

Ask:
- How many users are affected? (All / Many / Few / None)
- Is the core user journey broken? (Checkout, Login, API, etc.)
- Is data at risk or being lost?
- Is there redundancy still in place?

---

## Determining Urgency

Ask:
- Is the situation getting worse over time?
- Is there a workaround available?
- Is a time-sensitive event running? (Traffic spike, marketing campaign, fiscal cutover)

---

## Priority Rules

1. **Mitigate first, investigate later** — for SEV-1, restore service, then do RCA.
2. **Do not over-escalate** — page only who is needed.
3. **Do not under-escalate** — if you have been stuck for 10 minutes with no clear path, escalate.
4. **Communicate more than you think is necessary** during SEV-1/SEV-2.
