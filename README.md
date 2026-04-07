# Agent Second Brain

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=flat-square)](LICENSE)
[![claude-code](https://img.shields.io/badge/claude--code-black?style=flat-square)](https://claude.ai/code)
![ai-agents](https://img.shields.io/badge/ai--agents-5C6BC0?style=flat-square)
![knowledge-management](https://img.shields.io/badge/knowledge--management-2E7D32?style=flat-square)
![second-brain](https://img.shields.io/badge/second--brain-6D4C41?style=flat-square)

A starter kit for building a living knowledge system for Claude Code agents. Based on a production system running since early 2026.

Clone it. Fill in your identity. Start building.

---

## What This Is

Most people configure Claude Code by writing a CLAUDE.md that tells the agent what tools to use and what tone to take. That works for simple tasks.

This is a different architecture. It treats the agent's knowledge as a system that grows, is tested, and evolves — not a static config file that ages out of date.

The result is an agent that gets better at your specific work over time. Rules graduate from hypotheses. Failed beliefs get logged so you don't re-learn them. The agent loads only what it needs.

---

## Why CLAUDE.md Isn't Config — It's Memory Architecture

A config file tells software what to do. Memory tells an agent who it's working for, what it knows, and how to reason.

The difference matters because:

**Config decays.** You write a rule in month one. By month three, you've learned three exceptions and the rule is technically wrong but nobody's updated it. The agent enforces a rule that lost its validity.

**Memory evolves.** Hypotheses get tested. Rules graduate from evidence. The system has a mechanism for being wrong and correcting itself.

**Config loads everything.** The bigger your CLAUDE.md, the worse the signal-to-noise ratio. An agent reading 200 lines to do a 10-line task is working against itself.

**Memory loads on demand.** The agent reads the INDEX, identifies the task type, and loads only the files that matter. Knowledge scales without degrading context quality.

This repository gives you the architecture. You supply the knowledge.

---

## Four Cognitive Components

The system addresses four capabilities most agent setups are missing:

| Component | What it does | Key file |
|-----------|-------------|----------|
| **Perception** | Loads only what the task needs (3-4 files standard, 5-6 complex) | `INDEX.md` |
| **Reasoning** | Routes task types to the right knowledge files | `CLAUDE.md` routing table |
| **Learning** | Tests hypotheses, graduates them to rules with 3+ data points | `hypotheses/index.md` |
| **Immunity** | Logs rejected beliefs so the agent never re-tests them | `hypotheses/rejected.md` |

New evidence becomes a hypothesis first. Hypotheses graduate through evidence, not conviction. The false belief you've already tested is the most expensive one to re-test.

---

## Quick Start

```bash
# 1. Clone
git clone https://github.com/phuryn/agent-second-brain
cd agent-second-brain

# 2. Fill in your identity
# Open Claude Code in this directory. The agent will detect empty brackets
# and walk you through setup automatically (First Run onboarding).
# Or edit CLAUDE.md manually — replace all [BRACKETS] with your specifics.

# 3. Start using it
# Open Claude Code. The agent will load knowledge/INDEX.md at conversation start.
# Add knowledge files as your system grows. Update INDEX.md routing when you do.

```

See `examples/` for filled-in systems showing how different roles use this structure. Copy one as a starting point if it matches your role.

---

## File Structure

```
agent-second-brain/
├── README.md
├── CLAUDE.md                          # Identity, routing, procedures, constraints
├── knowledge/
│   ├── INDEX.md                       # Master routing file — always load first
│   ├── system-maintenance.md          # Diagnostic script + hygiene rules
│   └── hypotheses/
│       ├── index.md                   # Hypothesis tracking + graduation schema
│       ├── rejected.md                # Immune memory — beliefs proven wrong
│       └── EXAMPLE.md                 # Reference — shows schema at each lifecycle stage
└── examples/
    ├── software-engineer/             # Backend engineer: code review, architecture, bug analysis
    ├── researcher/                    # Research scientist: literature, experiments, methodology
    └── ops-engineer/                  # SRE: incident response, runbooks, system health
```

Each example contains a filled-in `CLAUDE.md` with role-specific procedures, domain knowledge files, populated hypotheses (active, graduated, and rejected), and routing — a complete working system you can copy as a starting point.

---

## What This Is Not

This is not a prompt library. It's not a collection of system prompts you paste into Claude. It's not a one-size-fits-all configuration.

It's a structure. You bring the knowledge. The system gives it somewhere to live, a mechanism for evolving, and a way to make sure the agent loads the right things at the right time.

---

## Full Article

**[Karpathy Built a Second Brain for Humans. Here's One for Your AI Agent.](https://x.com/PawelHuryn/status/2041519394254176581)**

---

## Credit

Built by Pawel Huryn (The Product Compass Newsletter). Based on a production system running since early 2026.

First published March 16, 2026. Link: https://www.productcompass.pm/p/self-improving-claude-system

---

## Contributing

Issues and PRs welcome. If you build an example for a new role, submit it.
