# Issue

**Title:** fix: eliminate zarr store flakiness

## Description

<!--
Thanks for opening a PR to scanpy!
Please be sure to follow the guidelines in our contribution guide (https://scanpy.readthedocs.io/en/latest/dev/index.html) to familiarize yourself with our workflow and speed up review.
-->

When not using a context manager, the store gets closed on GC which can happen whenever and warns.

<!-- Please check (“- [x]”) and fill in the following boxes -->
- [x] ,  
- [ ] [Tests][] included or not required because:
<!-- Only check the following box if you did not include release notes -->
- [x] [Release notes][] not necessary because: unreleased

[tests]: https://scanpy.readthedocs.io/en/stable/dev/testing.html#writing-tests
[release notes]: https://scanpy.readthedocs.io/en/stable/dev/documentation.html#adding-to-the-docs

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5f2accbe77cb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.