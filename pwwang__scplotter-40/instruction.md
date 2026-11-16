# Issue

**Title:** Resolve R 4.5 dependency installation failure

## Description

The R 4.5 Actions job failed while resolving dependencies: the scRepertoire requirement pulled in `immApex >= 1.7.1`, and `pak` could not solve the resulting dependency set.

- **Pin compatible dependencies:** Use scRepertoire v2.7.3 and immApex 1.4.0; remove the separate immReferent remote.
- **Align the declared minimum:** Lower scRepertoire’s Imports constraint to `>= 2.7.3`.

```diff
- scRepertoire (>= 2.9.1)
+ scRepertoire (>= 2.7.3)

- BorchLab/scRepertoire
- BorchLab/immApex
- BorchLab/immReferent
+ BorchLab/scRepertoire@v2.7.3
+ BorchLab/immApex@1.4.0
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8ac4d380c65d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.