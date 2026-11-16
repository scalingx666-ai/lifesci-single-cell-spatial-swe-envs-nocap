# Issue

**Title:** fix: allow ingest to handle older anndata

## Description

<!--
Thanks for opening a PR to scanpy!
Please be sure to follow the guidelines in our contribution guide (https://scanpy.scverse.org/page/dev/) to familiarize yourself with our workflow and speed up review.
-->

<!-- Please check (“- [x]”) and fill in the following boxes -->

- [x]
- [x] [Tests][] included or not required because:
  <!-- Only check the following box if you did not include release notes -->
- [ ] [Release notes][] not necessary because:
  <!-- See the scverse AI policy: https://scverse.org/about/ai_policy/
       Pull requests that skip this section are closed without review; undisclosed LLM use can lead to a ban. -->
- [x] LLM or coding agent used: Claude Opus 5.5 via Claude Code
- [x] If one was used, I, a human, have reviewed, understood and tested every changed line

[tests]: https://scanpy.readthedocs.io/page/dev/testing.html#writing-tests
[release notes]: https://scanpy.readthedocs.io/page/dev/documentation.html#adding-to-the-docs

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `50bb2b08b973`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.