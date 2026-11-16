# Issue

**Title:** docs: switch to sphinx-exec-jupyter

## Description

It’s a bit slower (212 sec → 274 sec) but all docs pages are run in isolation and the docs logs aren’t spammed with warnings that happen during plot execution.

Also it locally caches the plot code execution, so things should be faster locally with a populated cache.

<!-- Please check (“- [x]”) and fill in the following boxes -->
- [ ] Closes #
- [x] [Tests][] included or not required because:
<!-- Only check the following box if you did not include release notes -->
- [x] [Release notes][] not necessary because: internal change


TODO:
- [x] add mode that only runs each page in isolation, not each code block

[tests]: https://scanpy.readthedocs.io/en/stable/dev/testing.html#writing-tests
[release notes]: https://scanpy.readthedocs.io/en/stable/dev/documentation.html#adding-to-the-docs

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `68eeb6a2ff35`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.