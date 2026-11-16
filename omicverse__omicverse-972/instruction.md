# Issue

**Title:** fix(space): correct SVG significance and independent-library statistics

## Description

Apply significance thresholds before the SVG gene-count cap for Moran, SOMDE and SpatialDE. Keep ranked top_n selection explicit, mark untestable autocorrelation inputs as NaN, return valid permutation probabilities, and preserve inputs under copy=True.

Align Moran/Geary statistics with Squidpy 1.8.3's serial convention: use the same Scanpy kernels, analytical smaller-tail probabilities, graph-row permutations and seed stream. As in that reference, two_tailed affects analytical probabilities, not empirical permutation tails. Moran SVG defaults to the analytical test; explicit n_perms enables permutation testing, whose minimum p-value is 1/(n_perms+1). SVG selection additionally requires positive Moran I.

Independent libraries retain their backend's separate q-values and selections; the global mask is their union. Do not introduce cross-library BH or replace SOMDE/SpatialDE native q-values. Require explicit library identity when ambiguous. Sepal validates actual graph degrees rather than prescribing construction metadata. Use the existing three-point finite-difference formula where scipy.misc.derivative was removed; the scientific optimizers are unchanged.

Accept dense, CSC and CSR connectivity inputs without changing the caller's graph. Compute graph moments in float64 and ignore stored zeros when validating cross-library connections.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `41531a627523`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.