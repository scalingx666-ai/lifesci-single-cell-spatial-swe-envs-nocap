# Issue

**Title:** perf: speed up igraph RNG adapter for `rng` Generators

## Description

igraph calls `_RNGIgraph.getrandbits` → `Generator.integers(…)` once per random number.

This improves igraph Leiden on a 200k-cell graph with `rng=…` from 12.6s to 8.2s.

Changes results, but `rng` only guarantees minor version compatibility here.

- [ ] Closes #
- [ ] [Tests][] included or not required because:
<!-- Only check the following box if you did not include release notes -->
- [ ] [Release notes][] not necessary because:

[tests]: https://scanpy.readthedocs.io/page/dev/testing.html#writing-tests
[release notes]: https://scanpy.readthedocs.io/page/dev/documentation.html#adding-to-the-docs

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bc97bc01668f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.