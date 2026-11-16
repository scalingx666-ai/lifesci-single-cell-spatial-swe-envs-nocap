# Issue

**Title:** fix(preprocessing): keep duplicate var names apart in batched HVG selection

## Description

**LLM usage**

- [x] LLM or coding agent used: Claude Opus 5.5 via Claude Code
- [x] If one was used, I, a human, have reviewed, understood and tested every changed line
- [x] 
- [x] [Tests][] included: `test_batched_duplicate_var_names`
- [x] [Release notes][] added: `docs/release-notes/4439.fix.md`

[tests]: https://scanpy.readthedocs.io/page/dev/testing.html#writing-tests
[release notes]: https://scanpy.readthedocs.io/page/dev/documentation.html#adding-to-the-docs

### Problem

With `batch_key`, the `seurat` and `cell_ranger` flavors combine the per-batch results with `df.groupby(df.index)`, i.e. by gene name, and map them back with `df.loc[adata.var.index]`. Two genes that share a name are averaged into one row, and each occurrence of the name then selects that row again. So more than `n_top_genes` genes are flagged, and both genes report the pair's mean statistics.

`_highly_variable_genes_single_batch` has the same label problem when it re-inserts the genes it filtered out for a batch (`.loc[adata.var_names]`). That path always runs with `batch_key`.

### Fix

Keep genes apart by position:
- per-batch frames are concatenated on a positional index and grouped with `groupby(level=0)`;
- genes filtered out in a batch are put back in their original position with `iloc`;
- the result index is set to `adata.var_names` at the end.

With unique names the output is unchanged.

### Not changed

The `seurat_v3` path (#4405), which #4409 and #4417 already address.

### Tests

- New `test_batched_duplicate_var_names[seurat|cell_ranger]` runs the same matrix with unique and with duplicated names, including a gene that is unexpressed in one batch. On `main` it flags 42 / 40 genes instead of 30; with this change both runs return identical frames.
- `pytest tests/test_highly_variable_genes.py`: 223 passed, 1 xfailed (pre-existing).
- `pytest tests/test_normalization.py tests/test_scrublet.py tests/plotting/legacy/test_pbmc3k.py`: 349 passed.
- The reproducer from #4432 now prints 30 for every case.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d87c3a071ee8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.