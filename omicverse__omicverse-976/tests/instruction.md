# Issue

**Title:** fix(cellmatch): remove three byte-identical duplicate method definitions in CellOntologyMapper

## Description

### Problem

`CellOntologyMapper` in `omicverse/single/_cellmatch.py` defines three of its methods **twice**:

| method | first definition | duplicate |
|---|---|---|
| `map_cells_with_expansion` | L977 | L3092 |
| `download_model` | L2282 | L3231 |
| `browse_ontology_by_category` | L2165 | L3689 |

Each duplicate is **byte-for-byte identical** to the first definition. At class-body evaluation time the later definition simply rebinds the name to an identical function object, so the earlier copies are dead code that bloat the file (~190 lines) and make the class harder to read/maintain — and any future edit to one copy silently diverges from the other.

### Fix

Remove the three redundant (identical) duplicate definitions. Pure dead-code removal — **no behavior change** (verified each pair is byte-identical; after removal each method resolves to the exact same code that ran before).

- `+0 / −189`, one file touched.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `06735e883b69`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.