# Dashboard Spec

This file is a handoff for any coding agent that creates a polished learning-progress webpage.

## Source of truth

Do **not** maintain progress separately inside the webpage.

Canonical sources:
- `LEARNING_STATE.md` — current state, checks, takeaways
- `COURSE_MAP.md` — dependency graph and homework mapping
- `TUTORING_PROTOCOL.md` — interpretation rules

The webpage is a renderer / view layer.

## Primary UI

The dashboard should show:

1. **North Star**
   - Independent Homework 1 completion
   - Understand -> Reconstruct -> Transfer -> Independent Homework

2. **Current Gate**
   - one large current-module card
   - current mastery level 0-4
   - exact closed-book checks still unresolved

3. **Dependency Path**
   - M0-M13 as a connected graph rather than a flat checklist
   - locked modules visually de-emphasized
   - current module obvious
   - milestone visual markers at M2, M5, M9, M12, M13

4. **Homework Coverage**
   - map HW1 Problems 1-4 to the modules needed
   - do not display solutions or target answers

5. **Takeaway Vault**
   - durable, append-only rules parsed from tracker takeaways

6. **Milestone Gallery**
   - slots for future generated heroine teaching art
   - image shown only after milestone is actually cleared

## Visual direction

Desired page feeling:
- refined research notebook × cinematic training journey;
- clean typography and generous spacing;
- dark/light mode acceptable;
- avoid generic SaaS dashboard aesthetics;
- subtle probability-distribution / graph / privacy-wall motifs;
- visually beautiful but learning state must remain instantly readable.

## Tracker parser contract

Inside `LEARNING_STATE.md`:

```
<!-- tracker:begin -->
asof: YYYY-MM-DD
goal: ...
M0 | status | level | note
...
check: M0 | todo/done | text
takeaway: M0 | text
<!-- tracker:end -->
```

The parser should tolerate new `check:` and `takeaway:` rows without requiring code changes.

## State semantics

Status:
- current
- locked
- held
- partial
- cleared

Level:
- 0 = not cleared
- 1 = understand
- 2 = reconstruct
- 3 = transfer
- 4 = independent-homework ready

The UI must never infer a higher level merely because a lesson exists.
Evidence in `LEARNING_STATE.md` controls progress.
