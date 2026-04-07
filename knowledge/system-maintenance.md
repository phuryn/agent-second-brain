# System Maintenance

This file governs how the knowledge system stays healthy. Load it when auditing the system, not during regular tasks.

---

## Progressive Disclosure Rules

The system is designed to load minimally. These rules enforce that.

### Token Budgets

| Context | Max files to load | Approximate token ceiling |
|---------|------------------|--------------------------|
| Standard task | 3-4 files | ~8,000 tokens of knowledge |
| Complex task (multi-step) | 5-6 files | ~12,000 tokens |
| System audit | All files | No ceiling — this is maintenance |

### When to Split a File

Split a file when any of these are true:
- It exceeds 400 lines
- It serves two distinct purposes (sign: two different task types both load it for different reasons)
- Loading it always requires reading less than 50% of its content

When you split, update INDEX.md immediately.

### When to Merge Files

Merge two files when all of these are true:
- They are always loaded together for the same task types
- Their combined size is under 200 lines
- They cover the same domain or context

When you merge, remove the old files and update INDEX.md routing to point to the merged file.

### When to Archive

Archive (move to an `archive/` subfolder) rather than delete when:
- A knowledge area is no longer active but may return
- A hypothesis is rejected but the evidence log is worth keeping
- A file hasn't been loaded in 60+ days

Never delete without archiving. The cost of archiving is near zero; the cost of losing institutional memory is high.

### When NOT to Add a File

Before adding any new file, ask:
1. Will this be loaded in at least 1 task per week?
2. Does INDEX.md have a clear routing entry for it?
3. Is this genuinely new knowledge, not already covered elsewhere?

If any answer is "no," don't add the file. Add a note to an existing file instead.

### When Hypotheses Outgrow a Single File

A single `hypotheses/index.md` works for the first 10-15 hypotheses. Beyond that, reorganize:

1. **Split by domain.** Create `hypotheses/[domain].md` files (e.g., `hypotheses/api-design.md`, `hypotheses/performance.md`). Each file holds hypotheses for one domain.
2. **Keep `hypotheses/index.md` as the router.** It becomes a table of contents linking to domain files, not a container for individual hypotheses.
3. **Update INDEX.md routing.** The main INDEX.md should route to specific hypothesis domain files, not load all of them.
4. **Split `rejected.md` the same way** if it grows beyond 20 entries.

The same pattern applies to rules: when `rules.md` serves multiple contexts, split it by domain. One file per context keeps loading efficient.

Update CLAUDE.md routing table whenever you split. The agent should never need to guess which hypothesis file to load.

### When to Reorganize the Directory Tree

Splitting and merging handle individual files. Sometimes the whole directory structure needs rethinking. Consider a tree reorganization when:

- You have 5+ knowledge files at the same level that naturally group into 2-3 categories
- The INDEX.md routing table has become a wall of entries with no grouping
- Two or more domains have grown their own sub-files (rules, templates, patterns) and deserve subdirectories
- The agent routinely loads files from unrelated areas because the structure doesn't match how work actually happens

How to reorganize:

1. Map current files by how they're actually used together (not by what they're about).
2. Group files into subdirectories by usage pattern. Create an INDEX.md inside each subdirectory if it has 3+ files.
3. Update the root `knowledge/INDEX.md` to route to subdirectory INDEX files, not individual leaf files.
4. Update `CLAUDE.md` routing table to match.
5. Run the diagnostic script to verify no orphans were created.

Example progression: flat → grouped → hierarchical:
```
# Flat (early, <8 files)
knowledge/
├── review-patterns.md
├── architecture-decisions.md
└── bug-patterns.md

# Grouped (growing, 8-15 files)
knowledge/
├── code-quality/
│   ├── review-patterns.md
│   └── bug-patterns.md
├── architecture/
│   └── decisions.md
└── hypotheses/

# Hierarchical (mature, 15+ files)
knowledge/
├── code-quality/
│   ├── INDEX.md
│   ├── review-patterns.md
│   ├── bug-patterns.md
│   └── anti-patterns.md
├── architecture/
│   ├── INDEX.md
│   ├── decisions.md
│   └── service-boundaries.md
└── hypotheses/
```

### Managing Graduated Hypothesis Stubs

Graduated and rejected hypotheses stay in `hypotheses/index.md` as one-line stubs for traceability (ID + pointer to where the rule now lives). Full evidence moves to the target knowledge file (for graduated) or `rejected.md` (for rejected).

Periodically clean up stubs:
- Archive graduated stubs older than 6 months to a `hypotheses/archive.md` file
- Keep rejected stubs indefinitely — they're the system's immune memory
- If the graduated section exceeds 20 entries, archive all but the 5 most recent

---

## Scheduled Tasks

If your workflow involves external data sources that the system should learn from regularly, set up scheduled tasks. These are scripts or prompts that run on a schedule to pull new data, surface relevant information, or trigger maintenance.

### When to Use Scheduled Tasks

- You have external data sources the agent should monitor (logs, feeds, APIs, databases)
- Pattern detection benefits from regular data pulls rather than ad-hoc analysis
- Maintenance should happen on a cadence, not only when someone remembers

### How to Set Up

1. Create a `tools/scheduled/` directory for scheduled task prompts or scripts.
2. Each task gets its own file: a script (`.sh`, `.py`) or a prompt file (`.md`) describing what the agent should do when triggered.
3. Document the schedule and purpose in each file's header.
4. Add deduplication logic — scheduled tasks that fetch data should track what's already been fetched to avoid duplicates.

### Example Scheduled Tasks by Role

| Role | Task | Schedule | What it does |
|------|------|----------|--------------|
| Software engineer | PR pattern scanner | Weekly | Scan merged PRs for recurring review comments → surface as hypotheses |
| Researcher | Literature monitor | Weekly | Check RSS feeds or preprint servers for new papers in tracked topics |
| Ops engineer | Incident log scanner | Daily | Parse incident logs for recurring patterns → update `incident-patterns.md` |
| Any role | Maintenance diagnostic | Bi-weekly | Run the diagnostic script, surface drift signals |

Reference scheduled task files from `CLAUDE.md` or `knowledge/INDEX.md` so the agent knows they exist.

---

## Diagnostic Script

Run this script periodically to catch system drift. It checks file count, total size, orphan files, and broken INDEX references.

```bash
#!/bin/bash
# agent-second-brain diagnostic
# Run from the repo root: bash knowledge/system-maintenance.sh

set -euo pipefail
KNOWLEDGE_DIR="knowledge"
INDEX="$KNOWLEDGE_DIR/INDEX.md"

echo "=== Agent Second Brain Diagnostic ==="
echo "Run date: $(date '+%Y-%m-%d %H:%M')"
echo ""

# 1. File count
FILE_COUNT=$(find "$KNOWLEDGE_DIR" -name "*.md" | wc -l)
echo "Files in knowledge/: $FILE_COUNT"
if [ "$FILE_COUNT" -gt 30 ]; then
  echo "  ⚠ WARNING: Over 30 files. Consider archiving unused files."
fi

# 2. Total size
TOTAL_SIZE=$(du -sh "$KNOWLEDGE_DIR" 2>/dev/null | cut -f1)
echo "Total size: $TOTAL_SIZE"

# 3. Largest files (top 5)
echo ""
echo "Largest files:"
find "$KNOWLEDGE_DIR" -name "*.md" -exec wc -l {} \; | sort -rn | head -5 | while read lines file; do
  echo "  $lines lines — $file"
  if [ "$lines" -gt 400 ]; then
    echo "    ⚠ WARNING: Exceeds 400-line split threshold"
  fi
done

# 4. Orphan files (in knowledge/ but not referenced in INDEX.md)
echo ""
echo "Checking for orphan files (not referenced in INDEX.md)..."
ORPHANS=0
while IFS= read -r -d '' file; do
  filename=$(basename "$file" .md)
  if ! grep -q "$filename" "$INDEX" 2>/dev/null; then
    echo "  ⚠ ORPHAN: $file"
    ORPHANS=$((ORPHANS + 1))
  fi
done < <(find "$KNOWLEDGE_DIR" -name "*.md" -not -name "INDEX.md" -print0)

if [ "$ORPHANS" -eq 0 ]; then
  echo "  ✓ No orphans found"
fi

# 5. Hypotheses status
echo ""
ACTIVE_HYPS=$(grep -c "status: active" "$KNOWLEDGE_DIR/hypotheses/index.md" 2>/dev/null || echo "0")
GRADUATED=$(grep -c "status: graduated" "$KNOWLEDGE_DIR/hypotheses/index.md" 2>/dev/null || echo "0")
REJECTED=$(grep -c "status: rejected" "$KNOWLEDGE_DIR/hypotheses/index.md" 2>/dev/null || echo "0")
echo "Hypotheses: $ACTIVE_HYPS active, $GRADUATED graduated, $REJECTED rejected"
if [ "$ACTIVE_HYPS" -gt 10 ]; then
  echo "  ⚠ WARNING: Too many active hypotheses. Schedule a graduation review."
fi

echo ""
echo "=== Diagnostic complete ==="
```

Save this as `knowledge/system-maintenance.sh` and run with `bash knowledge/system-maintenance.sh` from the repo root.

---

## Maintenance Checklist

- [ ] Run the diagnostic script above
- [ ] Review active hypotheses — graduate or reject anything with 3+ data points
- [ ] Check INDEX.md routing is still accurate
- [ ] Archive any knowledge area that hasn't been used in 60+ days
- [ ] Update the "System Status" block in INDEX.md
- [ ] Check file sizes — split any file exceeding the 400-line threshold
- [ ] Check for merge candidates — files always loaded together and under 200 lines combined
- [ ] Archive graduated hypothesis stubs older than 6 months
- [ ] Review directory structure — does it still match how tasks are routed?
- [ ] Check procedures in CLAUDE.md — does every routed domain have a procedure? Are existing procedures still accurate?
- [ ] Check scheduled tasks (if any) — are they running, producing useful output?

---

## Signs the System Is Drifting

Watch for these failure modes:

**Over-accumulation:** Files keep getting added, nothing gets archived. The INDEX grows beyond 80 lines. Loading instructions start saying "load most files."

**Rule calcification:** Rules haven't been updated despite changed context. Hypotheses sit at "active" indefinitely. No hypotheses have been rejected in months.

**Knowledge fragmentation:** The same information exists in multiple files with slight differences. Contradictions appear between files.

**Agent confusion:** The agent frequently asks "which file should I load?" or loads too many files "just in case."

If you see these signs, run a maintenance session before the next task.
