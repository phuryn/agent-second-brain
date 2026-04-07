# Agent Second Brain

A starter kit for building a living knowledge system for Claude Code agents. Based on a production system that has been running since early 2026.

Clone it. Fill in your identity. Run the diagnostic. Start building.

---

## What This Is

Most people configure Claude Code agents by writing a CLAUDE.md that tells the agent what tools to use and what tone to take. That works for simple tasks.

This is a different architecture. It treats the agent's knowledge as a system that grows, is tested, and evolves — not a static config file that ages out of date.

The result is an agent that gets better at your specific work over time. Rules graduate from hypotheses. Failed beliefs get logged so you don't re-learn them. Platform knowledge stays current. The agent loads only what it needs.

---

## Why CLAUDE.md Isn't Config — It's Memory Architecture

A config file tells software what to do. Memory tells an agent who it's working for, what it knows, and how to reason.

The difference matters because:

**Config decays.** You write a rule in month one. By month three, you've learned three exceptions and the rule is technically wrong but nobody's updated it. The agent enforces a rule that lost its validity.

**Memory evolves.** Hypotheses get tested. Rules graduate from evidence. False beliefs get documented. The system has a mechanism for being wrong and correcting itself.

**Config loads everything.** The bigger your CLAUDE.md, the worse the signal-to-noise ratio. An agent reading 200 lines to do a 10-line task is working against itself.

**Memory loads on demand.** The agent reads the INDEX, identifies the task type, and loads only the files that matter. Knowledge scales without degrading context quality.

This repository gives you the architecture. You supply the knowledge.

---

## The Four Cognitive Components

### 1. Perception — What the Agent Loads

**Files:** `CLAUDE.md` + `knowledge/INDEX.md`

The INDEX is the agent's routing layer. It maps task types to files, enforces load limits, and ensures the agent doesn't preload everything speculatively. Every conversation starts here.

The rule: never more than 4 files loaded for a standard task. Knowledge scales without context bloat.

### 2. Reasoning — How It Routes

**Files:** `knowledge/platforms/[platform]/rules.md`, `knowledge/craft/techniques.md`

Platform rules encode what you've learned about each output context. Craft files encode universal principles. The routing in CLAUDE.md connects task type to the right combination.

The rule: rules should have a source. Not "don't use links" but "don't use links — LinkedIn suppresses reach on posts with external links (confirmed across 12 tests)." Rules with reasons survive context changes. Rules without reasons don't.

### 3. Learning — Hypotheses That Graduate to Rules

**Files:** `knowledge/hypotheses/index.md`

Hypotheses are things you're testing — not yet rules, but not random guesses. They need three things: a precise statement, a falsification condition, and a data log.

When a hypothesis accumulates 3+ supporting data points with no strong counter-examples, it graduates to a rule in the relevant `rules.md`. When it gets 2+ counter-examples, it gets rejected and logged in `false-beliefs.md`.

The rule: no silent rule updates. New evidence becomes a hypothesis first. Hypotheses graduate through evidence, not conviction.

### 4. Immunity — Draft Gates and False Beliefs

**Files:** `knowledge/craft/draft-gate.md`, `knowledge/platforms/[platform]/false-beliefs.md`

Draft gates prevent the specific failure modes that are hardest to see from inside the work. False beliefs prevent you from re-enforcing rules that have already been proven wrong.

The false beliefs log is the system's immune system. When something surprises you — a post performs despite "breaking a rule" — that goes in the log. The rule gets examined. The system doesn't calcify.

---

## Quick Start

```bash
# 1. Clone and initialize
git clone https://github.com/pawelhuryn/agent-second-brain
cd agent-second-brain

# 2. Fill in your identity
# Edit CLAUDE.md — replace all [BRACKETS] with your specifics
# Takes ~10 minutes. Don't skip this.

# 3. Set up your first platform
# Copy knowledge/platforms/_PLATFORM_TEMPLATE/ to knowledge/platforms/[your-platform]/
# Fill in rules.md with what you know. Leave hypotheses for what you're not sure about.

# 4. Run the diagnostic
bash knowledge/system-maintenance.sh
# First run will show orphan files (expected) — they'll clear as you fill in the system

# 5. Start using it
# Open Claude Code. Load knowledge/INDEX.md at conversation start.
# Let the system grow from there.
```

See `examples/content-creator/` for a fully filled-in system across two platforms (LinkedIn + newsletter) with real rules, templates, hypotheses, and a topics file. Use it as a reference.

---

## File Structure

```
agent-second-brain/
├── README.md
├── CLAUDE.md                          # Starter template — fill in the brackets
├── knowledge/
│   ├── INDEX.md                       # Master routing file — always load first
│   ├── system-maintenance.md          # Diagnostic script + hygiene rules
│   ├── craft/
│   │   ├── draft-gate.md             # Two-stage quality gate
│   │   ├── voice-archetypes.md       # 9 voice archetypes reference
│   │   └── techniques.md             # Craft problems and techniques
│   ├── platforms/
│   │   └── _PLATFORM_TEMPLATE/       # Copy for each new platform
│   │       ├── rules.md
│   │       ├── templates.md
│   │       ├── hooks.md
│   │       └── false-beliefs.md
│   ├── hypotheses/
│   │   ├── index.md                  # Hypothesis tracking + graduation schema
│   │   └── EXAMPLE.md                # Example entries at each lifecycle stage
│   ├── posts/
│   │   └── db_YYYYMM.csv.example    # Performance log schema
│   └── topics/
│       └── _TOPIC_TEMPLATE.md        # Topic knowledge file template
└── examples/
    └── content-creator/              # Fully filled-in example system
        ├── CLAUDE.md
        └── knowledge/
            ├── INDEX.md
            ├── platforms/
            │   ├── linkedin/         # Rules, templates, hooks, false beliefs
            │   └── newsletter/       # Rules, templates
            ├── hypotheses/
            │   └── index.md          # 3 active hypotheses with real data
            ├── posts/
            │   └── db_202604.csv     # Sample performance log
            └── topics/
                └── product-strategy.md
```

---

## What This Is Not

This is not a prompt library. It's not a collection of system prompts you paste into Claude. It's not a one-size-fits-all configuration.

It's a structure. You bring the knowledge. The system gives it somewhere to live, a mechanism for evolving, and a way to make sure the agent loads the right things at the right time.

The blank templates are genuinely blank. The example system shows what a filled-in version looks like after six months of real use.

---

## Full Article

A detailed walkthrough of the architecture — why it's built this way, what problems it solves, and how to adapt it to domains beyond content creation — is published as a Substack article:

**[Link — coming soon]**

---

## Credit

Built by Pawel Huryn (Product Compass). Based on a production system running since early 2026.

First published as a Substack article in April 2026.

---

## Contributing

If you adapt this for a domain other than content creation (software engineering, research, customer success, etc.) and want to share your platform templates, open a PR. Domain-specific example folders are a natural extension.

Bugs, broken schemas, or confusing file names — open an issue.
