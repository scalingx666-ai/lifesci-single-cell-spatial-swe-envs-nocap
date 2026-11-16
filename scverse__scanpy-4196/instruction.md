# Issue

**Title:** docs: document that variance/std use ddof=1 (sample correction)

## Description

<!--
Thanks for opening a PR to scanpy!
Please be sure to follow the guidelines in our contribution guide
(https://scanpy.readthedocs.io/en/latest/dev/index.html) to familiarize yourself with our
workflow and speed up review.
-->

<!-- Please check ("- [x]") and fill in the following boxes -->
- [ ] Closes #
- [x] [Tests][] included or not required because: docs-only change, no behavior is added or modified.
<!-- Only check the following box if you did not include release notes -->
- [ ] [Release notes][] not necessary because:

[tests]: https://scanpy.readthedocs.io/en/stable/dev/testing.html#writing-tests
[release notes]: https://scanpy.readthedocs.io/en/stable/dev/documentation.html#adding-to-the-docs

---

`sc.pp.scale` computes gene-wise variance and standard deviation with Bessel's correction (`ddof=1`), via `mean_var(x, axis=0, correction=1)` in `scale_array` and `scale_array_masked`. This convention isn't stated anywhere in the docstring, so a reimplementation using `numpy.std()` defaults (`ddof=0`, population variance) silently diverges from `sc.pp.scale`'s output - negligible for large `n_obs`, but non-negligible for small datasets (e.g. ~0.02% on a ~2700-cell PBMC3k-sized dataset, enough to shift where `max_value` clipping takes effect).

This PR adds a `.. note::` to the `scale` docstring stating the correction used. No behavior change.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c52da398956c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.