# Issue

**Title:** Fix cell_velocities transition-gene selection with a boolean mask

## Description

## Summary
Fixes the bug that **#638** (by @Baschdl) documented with a failing test: passing `transition_genes` as a length-`n_vars` boolean mask to `dyn.tl.cell_velocities` crashes.

## Reproduction (current master)
```python
dyn.tl.cell_velocities(adata, transition_genes=[True] * adata.n_vars)
# IndexError: boolean index did not match indexed array along axis 0;
# size of axis is 1000 but size of corresponding boolean axis is 845
```

## Root cause
When some transition genes have NaN velocity, `cell_velocities` drops them and marks them `use_for_transition = False`:
```python
adata.var.loc[np.array(transition_genes)[~finite_inds], "use_for_transition"] = False
```
`finite_inds` (`= get_finite_inds(V)`) is aligned with **V's transition-gene columns** (845 = `use_for_dynamics`), but `transition_genes` here can be a length-`n_vars` boolean mask (1000). The `[~finite_inds]` index then mismatches. (This is the `dynamics_genes` / `transition_genes` interplay noted in #638.)

## Fix
Derive the transition-gene names from `use_for_transition` — which is set consistently for all input forms (name list, column name, boolean mask) earlier in the function — instead of indexing the raw `transition_genes`:
```python
transition_gene_names = adata.var_names[adata.var["use_for_transition"].values]
adata.var.loc[transition_gene_names[~finite_inds], "use_for_transition"] = False
```

## Validation
- Both #638 tests now pass (`test_cell_velocities`, `test_cell_velocities_selecting_transition_genes`).
- **Default path (`transition_genes=None`) is bit-identical** to master: `use_for_transition` identical and `velocity_umap` identical (`max|Δ| = 0`). In that path `transition_genes` already equals `adata.var_names[use_for_transition]`, so the derived names match exactly.
- No regression: storage/selection logic only.

. Tests contributed by @Baschdl.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01AD7gAdxa3Zt5uiQVDoANa5

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b91ff5a486bc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.