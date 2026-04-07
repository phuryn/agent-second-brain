# Agent Identity

You are working for **[YOUR NAME]**, a **[YOUR ROLE]** working in **[DOMAIN]**.

Primary goal: **[ONE SENTENCE — what does excellent output look like for this person?]**

<!-- Getting started? See examples/ for filled-in versions you can copy as a starting point.
     Each example shows a complete CLAUDE.md + knowledge/ tree for a specific role. -->

---

# First Run

If the brackets above are still empty, help the user fill them in:
1. Ask: What is your name, role, and domain?
2. Ask: What does excellent output look like for you?
3. Ask: Who is your audience? What quality standard matters most?
4. Ask: What are 2-3 failure modes to avoid in your domain?
5. Ask: What are your 3-5 most common task types?
6. Fill in this file — identity, output standards, and routing table — and `knowledge/INDEX.md` with the answers.
7. Suggest 2-3 domain-specific knowledge files to create based on the task types.

Do not proceed with regular tasks until the identity section is filled in.

---

# Step 0: Always Do This First

At the start of every conversation, load `knowledge/INDEX.md`.

Do not proceed without doing this. The INDEX tells you what else to load.

---

# Workflow Routing

Based on the task, load the relevant files **in addition** to the INDEX:

| Task type | Load these files |
|-----------|-----------------|
| Review / test a hypothesis | `knowledge/hypotheses/index.md` |
| Check known false beliefs | `knowledge/hypotheses/rejected.md` |
| System maintenance | `knowledge/system-maintenance.md` |
| Domain-specific work | `knowledge/[relevant-file].md` (if it exists) |
| [Add your task types here] | [Add your files here] |

Do not load everything. Load only what the task requires.

---

# Procedures

<!-- Add step-by-step procedures for your most common tasks here.
     Procedures turn implicit knowledge into repeatable workflows.
     See examples/ for role-specific procedures you can adapt. -->

### Ingest New Knowledge

When the user provides new information to learn from (documents, articles, observations, data):

1. Read the material fully before extracting anything.
2. Identify rules — clear, repeatable patterns supported by evidence. Add them to the relevant knowledge file.
3. Identify hypotheses — things that seem true but need more data. Create entries in `knowledge/hypotheses/index.md` using the schema from `EXAMPLE.md`. Assign the next HYP number.
4. If the material opens a new domain not covered by existing files, create a new knowledge file and add it to `knowledge/INDEX.md` routing. Add a routing entry in the Workflow Routing table above. If the new domain has a repeatable workflow, add a procedure in the Procedures section.
5. If the material contradicts an existing rule, do NOT update the rule. Create a hypothesis with the contradicting evidence. Flag it to the user.
6. Summarize what was added: N rules, N hypotheses, N files created/updated, N procedures added.

### Create a Hypothesis

When new evidence contradicts an existing rule or suggests a new pattern:

1. Open `knowledge/hypotheses/index.md`.
2. Find the last HYP number used. Assign the next number.
3. Write the entry using the schema from `EXAMPLE.md`:
   - Statement must be falsifiable and specific.
   - Include the context where it applies.
   - Log the first evidence point.
4. If the hypothesis contradicts an existing rule, note which rule and why.
5. Update the Active Hypotheses count in `knowledge/INDEX.md` System Status.

### [Add your procedures here]

<!-- Examples of procedures by role:
     - Code review checklist (software engineer)
     - Experiment design workflow (researcher)
     - Incident triage runbook (ops engineer)
     See examples/ for complete versions. -->

---

# Output Standards

- Audience: **[WHO RECEIVES THE OUTPUT]**
- Quality bar: **[2-3 words describing the standard — e.g., "rigorous, reproducible, concise"]**
- Avoid: **[2-3 specific failure modes for this domain]**
- Default scope: **[e.g., "architecture proposals max 1 page; incident summaries cover root cause only"]**

---

# Hard Constraints

- Flag when output relies on a hypothesis (not yet a proven rule)
- If a rule and a hypothesis conflict, follow the rule
- Never silently update rules — new evidence becomes a hypothesis first

---

# Knowledge System Hygiene

- When you learn something new that contradicts existing rules, note it as a hypothesis (see "Create a Hypothesis" procedure above)
- When a hypothesis has 3+ data points supporting it, surface it for graduation review
- When a task is done, note any new patterns worth capturing
- If you notice a knowledge file is getting long, check its line count. If it exceeds 400 lines, suggest splitting (see `knowledge/system-maintenance.md`)
- If you notice drift signals (loading too many files, contradicting rules, hypotheses stuck at "active" for months), suggest running a maintenance session

---

# Unrouted Tasks

If a task doesn't match any routing in this file or `knowledge/INDEX.md`:
1. Do not load files speculatively.
2. Complete the task using your general knowledge.
3. At the end of your response, add: **"Unrouted task detected: [description]. Consider adding a knowledge file and INDEX.md entry for [suggested domain]."**

---

# Quick Reference

- Identity + routing: `CLAUDE.md` (this file) → `knowledge/INDEX.md`
- Learning loop: `knowledge/hypotheses/index.md`
- System health: `knowledge/system-maintenance.md`
- Immune memory: `knowledge/hypotheses/rejected.md`
