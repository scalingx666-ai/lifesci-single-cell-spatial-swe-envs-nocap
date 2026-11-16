# Issue

**Title:** docs: document the `adata.uns['hvg']` output of `pp.highly_variable_genes`

## Description

- [x]
- [x] [Tests][] included or not required because: docstring-only change, no behaviour is added or modified
<!-- Only check the following box if you did not include release notes -->
- [x] [Release notes][] not necessary because: documentation-only change to an existing docstring

[tests]: https://scanpy.readthedocs.io/en/stable/dev/testing.html#writing-tests
[release notes]: https://scanpy.readthedocs.io/en/stable/dev/documentation.html#adding-to-the-docs

---

`pp.highly_variable_genes` writes `adata.uns['hvg'] = {'flavor': flavor}` when `inplace=True`, but the `Returns` section documents only the `adata.var` columns. `pl.highly_variable_genes` reads that entry to pick which metrics to plot, so deleting it raises `KeyError: 'hvg'`.

Adds one entry to `Returns`. No behaviour change.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ec374022343e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.