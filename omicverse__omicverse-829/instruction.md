# Issue

**Title:** fix(pyscenic): avoid removed NumPy msort

## Description

Summary:
- Remove np.msort usage from the pySCENIC binarization path for NumPy 2 compatibility.
- Keep diptest behavior aligned with the previous implementation while replacing the removed NumPy API.
- Fix the AttributeError reported in #826.

Validation:
- Confirmed no np.msort references remain.
- Simulated NumPy 2 behavior by removing np.msort at runtime and verified dip_fn, diptst, and derive_threshold still return successfully.
- Compared diptest outputs against the previous implementation under fixed seeds.

.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `dbca54e27e24`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.