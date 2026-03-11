# Memory Tiers — How Dex Learns

Dex uses a three-tier memory system to turn raw observations into stable, actionable patterns.

---

## The Tiers

```
HOT   → System/Session_Learnings/YYYY-MM-DD.md
          Raw daily captures. Status: pending.
          Added during /daily-review, /review.
          Reviewed: daily.

WARM  → System/Memory/Warm.md
          Promoted from Hot when a pattern starts forming (seen 2+ times).
          Status: validating. Being actively watched.
          Reviewed: weekly (during /week-review).

COLD  → 06-Resources/Learnings/Mistake_Patterns.md
         06-Resources/Learnings/Working_Preferences.md
          Validated, stable patterns. Status: stable.
          Surfaced at every session start.
          Reviewed: monthly or as needed.
```

---

## Promotion Rules

**Hot → Warm:** Promote during daily-review when you say "this feels like a pattern" or when the same thing appeared in 2+ sessions.

**Warm → Cold:** Promote during week-review when a Warm insight has 3+ instances or has been actively applied for 2 weeks.

**Demotion:** If a Cold pattern is resolved or no longer relevant, archive it (move to Resolved section). Don't delete — the history is useful.

---

## Signal Log

`System/Memory/Signals.md` tracks task outcomes. When a task goes differently than expected, a signal is captured. Repeated signals on the same theme create evidence for Hot → Warm promotion.

---

## Files

- `Warm.md` — Active Warm tier insights
- `Signals.md` — Task outcome signal log
- `README.md` — This file
