# Issue

**Title:** chore: use scverse-misc for data downloading

## Description

<!--
Thanks for opening a PR to scanpy!
Please be sure to follow the guidelines in our contribution guide (https://scanpy.readthedocs.io/en/latest/dev/index.html) to familiarize yourself with our workflow and speed up review.
-->

Not using the `anndata` loader here since

1. we use `datasetdir` and not a global cache … maybe we should get rid of that.
2. we use the `fallback_urls` [inspired by SnapATAC2](https://github.com/scverse/SnapATAC2/blob/5230124bc7a61c329f91c9ce42033dd90f8ff8c8/snapatac2/datasets.yaml) – maybe that should be added to upstream @timtreis @ilia-kats? 


----

<!-- Please check (“- [x]”) and fill in the following boxes -->
- [x] 
- [x] [Tests][] included or not required because:
<!-- Only check the following box if you did not include release notes -->
- [ ] [Release notes][] not necessary because:

[tests]: https://scanpy.readthedocs.io/en/stable/dev/testing.html#writing-tests
[release notes]: https://scanpy.readthedocs.io/en/stable/dev/documentation.html#adding-to-the-docs

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `643dff34dc84`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.