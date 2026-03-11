---
name: telos
description: Review and update your TELOS deep goal files — mission, long-term goals, beliefs, strategies, and more
---

## Purpose

Review and update the TELOS deep goal documentation system. TELOS captures your "why" — the layer above quarterly goals that keeps your planning anchored to what actually matters.

## Usage

- `/telos` — Dashboard view: completion status + what needs updating
- `/telos mission` — Review/update MISSION.md
- `/telos goals` — Review/update GOALS.md
- `/telos challenges` — Review/update CHALLENGES.md
- `/telos [file]` — Open any TELOS file by name (beliefs, models, strategies, narratives, learned, ideas, projects)

---

## Step 1: Load TELOS Directory

Check `01-Quarter_Goals/TELOS/` exists.

**If missing:**
> "TELOS hasn't been set up yet. It's a 10-file goal documentation system — your professional 'why' layer.
> Want me to set it up? It takes about 10 minutes to fill in the essentials."
>
> If yes → Create folder and files, then start guided fill-in from Step 3.

---

## Step 2: Dashboard (default view)

Scan all 10 TELOS files and assess fill-in status:

**Check each file for actual content** (vs just template placeholders):
- Has real text beyond template comments/bullets → ✅ Filled
- Only has `<!--` comments or empty `-` bullets → ⚪ Empty
- Has some content but looks thin → ⚠️ Sparse

Display dashboard:

```
--- TELOS Status ---

Core (fill these first):
  ✅ MISSION — Your north star
  ⚪ GOALS — 1-3 year goals (empty)
  ⚠️  CHALLENGES — Active blockers (sparse)

Context:
  ⚪ BELIEFS — Core principles (empty)
  ⚪ MODELS — Mental frameworks (empty)
  ⚪ STRATEGIES — Current playbook (empty)

Story:
  ⚪ NARRATIVES — Your professional story (empty)
  ⚪ LEARNED — Hard-won lessons (empty)

Future:
  ✅ PROJECTS — Strategic initiatives
  ⚪ IDEAS — Possibilities (empty)

Last updated: MISSION (2026-01-15), PROJECTS (2026-02-03)

What would you like to update? Or say "guide me" to fill in the high-priority ones.
---
```

---

## Step 3: Guided Fill-In (when user says "guide me" or opens empty files)

Work through high-priority files in order: MISSION → GOALS → CHALLENGES → STRATEGIES

For each file, ask 2-3 focused questions rather than showing the full template:

**MISSION:**
> "What's the core purpose behind what you do professionally? Try to capture it in one or two sentences — not your job title, but the impact you're trying to have."

**GOALS (1-year):**
> "What do you want to be true 12 months from now? Think across: your role, your skills, your impact, your finances, your team."

**GOALS (3-year):**
> "If things go well, where are you in 3 years? What role, what kind of work, what kind of life?"

**CHALLENGES:**
> "What's blocking you most right now — professionally or personally? What feels stuck?"

**STRATEGIES:**
> "Given your goals and challenges — what's your current playbook? How are you actually trying to get there?"

After each answer, write it to the appropriate file and confirm.

---

## Step 4: Single File Update (when user specifies a file)

Open the requested file, show current content, then ask:

> "Here's what you have in [FILENAME]. What do you want to update, add, or rethink?"

Take their input and update the file, preserving existing content unless they explicitly want to replace it.

After updating, write the new `*Last updated: YYYY-MM-DD*` at the bottom.

---

## Step 5: TELOS ↔ Planning Alignment Check (optional)

When user has both TELOS and Quarter Goals filled in, offer:

> "Want me to check how well your quarterly goals map to your TELOS?
> I can show you: which goals advance your mission, which 1-year goals have no quarterly work planned, and any challenges that aren't being addressed."

If yes:
1. Read `01-Quarter_Goals/Quarter_Goals.md`
2. Read `TELOS/GOALS.md` and `TELOS/CHALLENGES.md`
3. Surface gaps and misalignments
4. Suggest quarterly goal additions or adjustments

---

## Graceful Degradation

- TELOS files don't exist → Offer setup
- Files exist but empty → Dashboard shows gaps, offer guided fill-in
- Partially filled → Show what's there, suggest what to fill next
- Fully filled → Dashboard + alignment check option

---

## Notes

- TELOS is optional but makes quarterly planning much more intentional
- The minimum viable TELOS is: MISSION + GOALS + CHALLENGES (15-20 min)
- Update CHALLENGES monthly — it becomes stale fastest
- MISSION and BELIEFS rarely need updating (yearly at most)
- LEARNED should grow over time — add to it, never rewrite it
