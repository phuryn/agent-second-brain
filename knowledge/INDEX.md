# Knowledge INDEX

**How to use this file:** This is the routing layer. Read it completely at conversation start. Then load only the files relevant to the current task. Do not preload everything — token budgets matter.

---

## Directory Map

```
knowledge/
├── INDEX.md                    ← YOU ARE HERE (always load)
├── system-maintenance.md       ← Load when: managing/auditing the knowledge system itself
│
├── craft/
│   ├── draft-gate.md           ← Load when: creating or reviewing any output before publish
│   ├── voice-archetypes.md     ← Load when: unsure about tone, or calibrating voice for new context
│   └── techniques.md           ← Load when: editing, improving, or stuck on a specific craft problem
│
├── platforms/
│   └── _PLATFORM_TEMPLATE/     ← Copy this folder when adding a new platform
│       ├── rules.md            ← Load when: creating content for this platform
│       ├── templates.md        ← Load when: need a starting structure
│       ├── hooks.md            ← Load when: writing openers or closers
│       └── false-beliefs.md    ← Load when: questioning a rule or seeing unexpected results
│
├── hypotheses/
│   ├── index.md                ← Load when: reviewing what's being tested, or graduating a hypothesis
│   └── EXAMPLE.md              ← Reference only — shows schema
│
├── posts/
│   └── db_YYYYMM.csv           ← Load when: analyzing past performance or avoiding repetition
│
└── topics/
    └── _TOPIC_TEMPLATE.md      ← Copy when adding a new topic area
```

---

## What to Load Per Task

| Task | Files to load (beyond this INDEX) |
|------|-----------------------------------|
| Write new piece for [platform] | `platforms/[platform]/rules.md`, `platforms/[platform]/templates.md`, `craft/draft-gate.md` |
| Edit existing draft | `craft/draft-gate.md`, `craft/techniques.md` |
| Research a topic | `topics/[topic].md` (if exists) |
| Calibrate voice | `craft/voice-archetypes.md` |
| Test a hook style | `platforms/[platform]/hooks.md` |
| Review what's being tested | `hypotheses/index.md` |
| Audit system | `system-maintenance.md` |

---

## Load-on-Demand Rules

1. **Never load more than 4 knowledge files at once** unless the task explicitly requires it.
2. **Posts DB** (`posts/db_YYYYMM.csv`): Load only when asked to check for topic repetition or analyze performance. These files can be large.
3. **Voice archetypes**: Load once per conversation if voice is in question. Don't reload.
4. **False beliefs**: Load when a result surprises you or contradicts a rule. It's a debugging tool, not a reference.

---

## System Status

> **Last maintained:** [DATE]
> **Active hypotheses:** [N] — see `hypotheses/index.md`
> **Platforms covered:** [LIST]
> **Next maintenance due:** [DATE or trigger condition]

---

## Notes for the Agent

- If a task doesn't fit any routing above, note that and ask the user before loading speculatively.
- If you discover something this INDEX doesn't cover, flag it at end of task as a potential addition.
- This file should stay under 100 lines. If it grows beyond that, it needs to be split or trimmed.
