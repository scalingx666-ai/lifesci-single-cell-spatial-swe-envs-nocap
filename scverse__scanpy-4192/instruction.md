# Issue

**Title:** fix: aggregate dask multifunc

## Description

@ilan-gold there was a pre-existing bug in aggregate's dask code that causes a failure when calling with multiple function types. it works for just mean and var, but if adding anything else it failed. simple fix. this is a blocker for the stats PR

<!-- Please check (“- [x]”) and fill in the following boxes -->
- [ ] Closes #
- [x] [Tests][] included or not required because:
<!-- Only check the following box if you did not include release notes -->
- [ ] [Release notes][] not necessary because:

[tests]: https://scanpy.readthedocs.io/en/stable/dev/testing.html#writing-tests
[release notes]: https://scanpy.readthedocs.io/en/stable/dev/documentation.html#adding-to-the-docs

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c71485f33309`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.