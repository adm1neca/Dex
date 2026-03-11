# TELOS — Deep Goal Understanding

> Adapted from Daniel Miessler's [Personal AI Infrastructure](https://github.com/danielmiessler/Personal_AI_Infrastructure)

TELOS is a 10-file goal documentation system. It sits *above* quarterly goals and pillars in the planning hierarchy — providing the "why" that makes quarterly planning meaningful.

---

## The Files

| File | Purpose | Update Frequency |
|------|---------|-----------------|
| [MISSION.md](MISSION.md) | Core purpose — your north star | Rarely (yearly) |
| [GOALS.md](GOALS.md) | 1-3 year goals by domain | Quarterly |
| [PROJECTS.md](PROJECTS.md) | Strategic projects you're driving | Monthly |
| [BELIEFS.md](BELIEFS.md) | Core principles that guide decisions | Rarely |
| [MODELS.md](MODELS.md) | Mental frameworks you use | As learned |
| [STRATEGIES.md](STRATEGIES.md) | Current playbook for achieving goals | Quarterly |
| [NARRATIVES.md](NARRATIVES.md) | Stories you tell about yourself | Quarterly |
| [LEARNED.md](LEARNED.md) | Durable lessons from experience | As earned |
| [CHALLENGES.md](CHALLENGES.md) | Active obstacles and blockers | Monthly |
| [IDEAS.md](IDEAS.md) | Future possibilities to explore | Ongoing |

---

## Planning Hierarchy

```
TELOS (why)
  └── Pillars (strategic focus areas)
        └── Quarter Goals (90-day outcomes)
              └── Week Priorities (this week's bets)
                    └── Daily Plans (today's actions)
                          └── Tasks (specific work)
```

---

## How to Use TELOS

**Start here if you're new:**
1. Fill in `MISSION.md` first — just 1-2 sentences
2. Fill in `GOALS.md` — what do you want in 1 year? 3 years?
3. Fill in `CHALLENGES.md` — what's blocking you right now?
4. The rest can be filled in over time

**During `/quarter-plan`:**
- Dex reads MISSION + GOALS to suggest direction
- Your quarterly goals should advance at least one item in GOALS.md

**During `/week-plan`:**
- MISSION appears as a brief reminder of what you're building toward

**Anytime:**
- Run `/telos` to review and update these files
- Update CHALLENGES.md when blockers resolve or emerge
- Add to LEARNED.md when you earn a hard lesson

---

*TELOS integration added to Dex: 2026-03-11*
