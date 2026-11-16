# Issue

**Title:** docs: describe parameters of filter_rank_genes_groups

## Description

Document the previously undescribed parameters of tl.filter_rank_genes_groups and when stored rank_genes_groups results are used instead of recomputed values.

<!--
Thanks for opening a PR to scanpy!
Please be sure to follow the guidelines in our contribution guide (https://scanpy.scverse.org/page/dev/) to familiarize yourself with our workflow and speed up review.
-->

**LLM usage**

<!-- See the scverse AI policy: https://scverse.org/about/ai_policy/ -->
<!-- Pull requests that skip this section are closed without review; undisclosed LLM use can lead to a ban. -->

- [x] LLM or coding agent used: Claude Opus 5.5 via Claude Code
- [x] If one was used, I, a human, have reviewed, understood and tested every changed line

<!-- Please check (“- [x]”) and fill in the following boxes -->
- [x]  
- [x] [Tests][] included or not required because: not required because: docstring-only, existing tests and doctest pass
<!-- Only check the following box if you did not include release notes -->
- [x] [Release notes][] not necessary because:docs-only


`sc.tl.filter_rank_genes_groups` only documented `compare_abs`; the other nine parameters had no description on the API page (#1930).
This adds a description for each of them, plus a short paragraph on when the stored `rank_genes_groups` results (`logfoldchanges`, `pts`, `pts_rest`) are used and when the values are recomputed from the expression matrix.

Each statement was derived from the function body in `src/scanpy/tools/_rank_genes_groups.py` and checked with a small script on `pbmc68k_reduced`:
- `key`, `groupby` and `use_raw` default to the values stored by `rank_genes_groups` (`use_raw` to `False` if `layer` is set); `layer` is not inherited from the stored params
- the thresholds are strict: in-group fraction `>`, log2 fold change `>`, out-group fraction `<`
- stored values are only used if `groupby` and `use_raw` match and `reference` was `"rest"`; otherwise they are recomputed against all other cells

Not checked: the full docs build (`hatch run docs:build`) does not run on Windows. Checked with Claude Code

[tests]: https://scanpy.readthedocs.io/page/dev/testing.html#writing-tests
[release notes]: https://scanpy.readthedocs.io/page/dev/documentation.html#adding-to-the-docs

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d87c3a071ee8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.