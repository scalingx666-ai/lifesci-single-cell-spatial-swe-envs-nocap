# Issue

**Title:** LRIC analytical

## Description

# LRIC: analytical closed-form null (replaces CSR / area-correction)

## Summary
This PR reworks the spatial normalization of LRIC and CrossPCF, from a
complete-spatial-randomness (CSR) null estimated with Monte-Carlo annulus area correction to an
analytical, closed-form random-labelling null conditioned on the observed tissue support.
The result is deterministic (no sampling, no permutations), faster and lower-memory, and, because
it conditions on the observed point pattern rather than an estimated effective area, it handles
non-convex boundaries, holes, and tissue fragmentation without any area/edge-correction step.
Builds on the merged LRIC work (#234, #245); this PR replaces the null and cleans up the module.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `705bcf9dd9fa`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.