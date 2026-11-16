# Issue

**Title:** fix: handle scalar string groups in ranked-gene plots

## Description

<!--
Thanks for opening a PR to scanpy!
Please be sure to follow the guidelines in our contribution guide (https://scanpy.readthedocs.io/en/latest/dev/index.html) to familiarize yourself with our workflow and speed up review.
-->

## Description

`groups` accepts either a single string or a sequence of strings in the ranked-gene plotting APIs. However, `sc.pl.rank_genes_groups` and the shared plotting path iterated a scalar string character by character.

For example, passing `groups="Dendritic"` attempted to look up the group `"D"` and raised an error instead of plotting `"Dendritic"`.

This PR normalizes scalar string group names to one-element lists before iteration, consistent with the existing behavior in `sc.pl.rank_genes_groups_violin` and `sc.get.rank_genes_groups_df`.

<!-- Please check (“- [x]”) and fill in the following boxes -->
- [ ] Closes # — no existing issue
- [x] [Tests][] included: added regression coverage for both the standalone and shared plotting paths
<!-- Only check the following box if you did not include release notes -->
- [x] [Release notes][] not necessary because: it's just a simple fix.

## Tests

- add related test.

[tests]: https://scanpy.readthedocs.io/en/stable/dev/testing.html#writing-tests
[release notes]: https://scanpy.readthedocs.io/en/stable/dev/documentation.html#adding-to-the-docs

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a656a33b080a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.