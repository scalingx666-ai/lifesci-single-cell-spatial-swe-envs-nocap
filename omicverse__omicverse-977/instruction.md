# Issue

**Title:** fix(cpdbviz): remove the dead first netAnalysis_contribution definition (shadowed, different API)

## Description

### What

`CellChatVizPlus` in `omicverse/pl/_cpdbviz_plus.py` defines `netAnalysis_contribution` **twice**. Python binds the later one, so the first definition (L2756–2920) is dead code that can never execute.

### Why this is worth removing rather than harmless duplication

The two definitions are *not* the same function — they take different parameters and return differently shaped results:

| | parameters | returns |
|---|---|---|
| **dead** (L2756) | `signaling, group_celltype=None, sources=None, targets=None, pvalue_threshold=0.05, top_pairs=10, figsize=(12, 8), font_size=10, title=None, save=None` | `(fig, lr_contrib)` |
| **live** (L3555) | `signaling, pvalue_threshold=0.05, mean_threshold=0.1, top_pairs=10, figsize=(10, 6), save=None` | `(contribution_df, fig, (ax1, ax2))` |

The **live** signature is the one the codebase depends on:

- `omicverse/pl/_ccc.py` calls `viz.netAnalysis_contribution(signaling=..., pvalue_threshold=..., top_pairs=..., figsize=..., save=None)` and then unpacks a 3-tuple (`_, fig, axes = contribution_result`).
- The documented usage in `.claude/skills/single-cellphone-db/reference.md` uses the same keyword set.
- `tests/pl/test_ccc_plots.py` stubs it returning `None, fig, (ax,)` — again the 3-tuple form.

Nothing in the repository passes `group_celltype`, `sources`, `targets`, `font_size` or `title`. The dead copy only advertises an API that does not exist at runtime — a reader of the source sees per-celltype / source / target filtering options that silently do not work.

### Verification

Removing the dead definition is a **pure no-op**:

- Built the patched file, re-parsed both versions with `ast`, and compared `ast.dump` of the **final** binding for every name in the `CellChatVizPlus` class body. All bindings are byte-identical; the set of names is identical (32 → 31 `FunctionDef` nodes, 31 unique names both before and after).
- No remaining duplicate method names in the class.
- Module-level top-level names unchanged; the file still `ast.parse`s.

`+0 / −166`, single file, no behaviour change.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `06735e883b69`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.