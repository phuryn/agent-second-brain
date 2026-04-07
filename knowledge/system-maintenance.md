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
- [ ] Trim any file that has exceeded the 400-line threshold

---

## Signs the System Is Drifting

Watch for these failure modes:

**Over-accumulation:** Files keep getting added, nothing gets archived. The INDEX grows beyond 80 lines. Loading instructions start saying "load most files."

**Rule calcification:** Rules haven't been updated despite changed context. Hypotheses sit at "active" indefinitely. No hypotheses have been rejected in months.

**Knowledge fragmentation:** The same information exists in multiple files with slight differences. Contradictions appear between files.

**Agent confusion:** The agent frequently asks "which file should I load?" or loads too many files "just in case."

If you see these signs, run a maintenance session before the next task.
