# Issue

**Title:** docs: add inline example for pca_scatter

## Description

Adds an inline rendered example for `sc.pl.pca_scatter`, addressing part of #1664.

`pca_scatter` is a backwards-compatible alias for `pca`, so this PR replaces the plain alias with a small wrapper that keeps behavior unchanged while giving the alias its own docstring and plot example.

- [x] Addresses part of #1664 
- [x] [Tests][] included or not required because: this is a documentation-only change adding an inline example for `sc.pl.pca_scatter`.
- [x] [Release notes][] not necessary because: this only adds a documentation example and does not change user-facing behavior.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `39f12414fea9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.