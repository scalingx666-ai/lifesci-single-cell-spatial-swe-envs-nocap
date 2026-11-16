# Issue

**Title:** chore: stale AnnData.concatenate references

## Description

This PR fixes stale references to `AnnData.concatenate`, which was removed from `anndata` (scverse/anndata#2370) and is no longer available in the hosted intersphinx inventory. These stale references were causing the Read the Docs build to fail.

Changes:

- Replace broken Sphinx `AnnData.concatenate` method links with plain literal text.
- Update the Harmony time-series example and test to use `anndata.concat`.
- Preserve the previous unique-index behavior with `index_unique="-"`.

<!-- Please check (“- [x]”) and fill in the following boxes -->
- [ ] Closes #
- [x] [Tests][] included or not required because:
<!-- Only check the following box if you did not include release notes -->
- [x] [Release notes][] not necessary because: this is just a fix for stale historical references caused by an upstream `anndata` API removal.

[tests]: https://scanpy.readthedocs.io/en/stable/dev/testing.html#writing-tests
[release notes]: https://scanpy.readthedocs.io/en/stable/dev/documentation.html#adding-to-the-docs

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `af6de2e90a36`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.