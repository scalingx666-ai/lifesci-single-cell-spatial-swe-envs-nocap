# Issue

**Title:** Add deprecation warnings for CellRank 3.0

## Description

Emit DeprecationWarning for features scheduled for removal in v3.0:

- CFLARE estimator: warn on instantiation, fit(), and predict(). Users should migrate to GPCCA.
- GPCCA.fit() / GPCCA.predict(): warn on call. Users should use compute_schur()/compute_macrostates() and predict_terminal_states() directly.
- VelocityKernel model="stochastic"/"monte_carlo": warn when model is not "deterministic". Paves the way for removing the JAX dependency.

All deprecated code paths remain fully functional.

**IMPORTANT: Please search among the [Pull requests](../pulls) before creating one.**

## Description
<!-- Clearly and concisely describe your changes. This section will be shown in the docs. -->

## How has this been tested?
<!-- Describe in detail how you've tested your changes. -->

## Closes
<!-- If applicable, type `closes #XXXX` in your comment to auto-close the issue that this PR fixes. -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c8f1975804a8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.