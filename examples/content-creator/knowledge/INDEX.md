# Knowledge INDEX — Content Creator Example

**How to use this file:** This is the routing layer. Read it completely at conversation start. Then load only the files relevant to the current task. Do not preload everything.

---

## Directory Map

```
knowledge/
├── INDEX.md                           ← YOU ARE HERE (always load)
├── system-maintenance.md              ← Load when: auditing the system
│
├── craft/
│   ├── draft-gate.md                  ← Load when: publishing any piece
│   ├── voice-archetypes.md            ← Load when: calibrating tone
│   └── techniques.md                  ← Load when: editing or stuck
│
├── platforms/
│   ├── linkedin/
│   │   ├── rules.md                   ← Load when: writing LinkedIn content
│   │   ├── templates.md               ← Load when: need structure
│   │   ├── hooks.md                   ← Load when: writing openers/closers
│   │   └── false-beliefs.md           ← Load when: questioning a LinkedIn rule
│   └── newsletter/
│       ├── rules.md                   ← Load when: writing newsletter issues
│       ├── templates.md               ← Load when: need issue structure
│       ├── hooks.md                   ← Load when: writing subject lines / intros
│       └── false-beliefs.md           ← Load when: questioning a newsletter rule
│
├── hypotheses/
│   ├── index.md                       ← Load when: reviewing experiments
│   └── EXAMPLE.md                     ← Reference only
│
├── posts/
│   └── db_202604.csv                  ← Load when: checking for topic repetition
│
└── topics/
    ├── product-strategy.md            ← Load when: writing about strategy topics
    └── ai-in-product.md               ← Load when: writing about AI in product
```

---

## What to Load Per Task

| Task | Load these |
|------|------------|
| Write LinkedIn long-form | `platforms/linkedin/rules.md`, `platforms/linkedin/templates.md`, `craft/draft-gate.md` |
| Write LinkedIn short post | `platforms/linkedin/rules.md`, `craft/draft-gate.md` |
| Write newsletter issue | `platforms/newsletter/rules.md`, `platforms/newsletter/templates.md`, `craft/draft-gate.md` |
| Edit any draft | `craft/draft-gate.md`, `craft/techniques.md` |
| Calibrate voice | `craft/voice-archetypes.md` |
| Check hook options | `platforms/[platform]/hooks.md` |
| Cover a topic | `topics/[topic].md` if it exists |
| Check for repetition | `posts/db_202604.csv` |
| Review active tests | `hypotheses/index.md` |

---

## Load-on-Demand Rules

1. **Never load more than 4 knowledge files at once** unless the task requires it.
2. **Posts DB**: Load only for repetition checks or performance analysis. These files grow large.
3. **Voice archetypes**: Load once per conversation. Don't reload.
4. **False beliefs**: Load when a result is surprising or contradicts a rule.

---

## System Status

> **Last maintained:** 2026-04-01
> **Active hypotheses:** 3 — see `hypotheses/index.md`
> **Platforms covered:** LinkedIn, Newsletter
> **Topics documented:** product-strategy, ai-in-product
> **Next maintenance due:** 2026-05-01 or when file count exceeds 25

---

## Notes for the Agent

- This is the example system for the agent-second-brain starter kit. The platform files below (linkedin/, newsletter/) show what a filled-in system looks like.
- Real rules and examples are included — use them as a model when filling in the blank templates.
- If Alex mentions a new platform (Twitter/X, YouTube), copy `_PLATFORM_TEMPLATE/` and fill it in.
