# Issue

**Title:** feat: move hashsolo to `sc.pp`

## Description

<!--
Thanks for opening a PR to scanpy!
Please be sure to follow the guidelines in our contribution guide (https://scanpy.readthedocs.io/en/latest/dev/index.html) to familiarize yourself with our workflow and speed up review.
-->

Basically just moving the code over and adding an `anndata.acc` based version of the API on top.

People had issues with our old API since it only supported `obs` columns:

- https://www.biostars.org/p/9561534/
- https://discourse.scverse.org/t/how-to-install-solo-sc-or-use-hashsolo-from-scvi/1702

The new API of course supports everything! Yay accessors!

<!-- Please check (“- [x]”) and fill in the following boxes -->
- [x] 
- [x] [Tests][] included or not required because:
<!-- Only check the following box if you did not include release notes -->
- [ ] [Release notes][] not necessary because:

[tests]: https://scanpy.readthedocs.io/en/stable/dev/testing.html#writing-tests
[release notes]: https://scanpy.readthedocs.io/en/stable/dev/documentation.html#adding-to-the-docs

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6b5405d4b95f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.