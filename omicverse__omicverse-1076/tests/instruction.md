# Issue

**Title:** space.CMAP: document the return value it actually has

## Description

#1073 shipped a docstring describing a two-tuple:

```python
>>> adata_sc, cell_spot_map = ov.space.CMAP(adata_sc, adata_st, spatial_genes=svg_list)
```

`pycmap.run_cmap` returns `cell_spot_map` **alone** and writes the placement
into `adata_sc` in place, so that call raises `ValueError: too many values to
unpack`. The patch was checked for syntax and for contract completeness, not
for behaviour — nobody had run it.

Measured on real Array-seq colon sections (600 spots → 800 cells, two
domains, 109 s end to end):

```
返回类型: DataFrame | 是 tuple 吗: False
  DataFrame 列: ['Single_cell', 'Spot', 'Probability', 'Second_prob', 'Entropy', 'Norm_entropy']
调用者对象是否被原地写入:
   新增 obs: ['CMAP_domain', 'CMAP_entropy', 'CMAP_norm_entropy', 'CMAP_quality',
             'CMAP_spot', 'CMAP_spot_prob', 'CMAP_svm_prob']
   新增 obsm: ['spatial_CMAP']
```

So the `register_function` contract was already correct — `produces` names
those keys and in-place is how they arrive. Only the prose was wrong.

## Changes

- `Returns` now names the DataFrame and its columns, and says it is the only
  return value.
- A `Side effects` section states the in-place write on `adata_sc`, because
  that is *where the placement lands* rather than an incidental mutation, and
  no copy is made.
- It names the asymmetry with `space.CellMap`, whose `assign_coord()` returns a
  copy and leaves the input untouched. Two placement methods in the same
  namespace with opposite conventions is worth saying out loud, and it is the
  mistake a caller moving between them will make.
- The example no longer unpacks.

No behaviour change.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e70ef79382e3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.