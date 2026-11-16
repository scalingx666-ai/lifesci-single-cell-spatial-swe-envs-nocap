# Issue

**Title:** Account for tissue cavities in section ordering

## Description

## Summary
- add scale-independent significant-cavity distance to semi-automatic section ordering
- ignore tiny lumina and mask holes below the topology threshold
- rebalance registration, area, outer-shape, and cavity evidence
- add regression coverage for solid, insignificant-hole, and substantial-cavity masks

## Validation
- 210 pytest tests passed
- Ruff lint and formatting checks passed
- visually validated the topology-aware proposal on the 33-slide 4269 cohort

Raw slides, generated reviews, fixed cohort anchors, and local paths are not included.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `da4469c133e1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.