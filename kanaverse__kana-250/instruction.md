# Issue

**Title:** Protect against missing feature names in explore mode.

## Description

. This is occasionally useful to ensure that the app does something sensible when feature information is missing for, e.g., alternative experiments that no one cares about.

Note that it doesn't solve the case of missing names in analysis mode, which is trickier as **bakana** handles the intersection of features (via **scran.js**'s `cbindWithNames`). 

I suspect that the more general solution is to just ignore all modalities without feature information in **bakana**'s readers, as the lack of feature information will kill a few downstream steps. But this will do for now.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ddc665ff8485`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.