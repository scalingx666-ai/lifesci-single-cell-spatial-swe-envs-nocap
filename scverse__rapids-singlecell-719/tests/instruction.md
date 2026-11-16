# Issue

**Title:** fix inplaces for log1p and scale

## Description

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **Bug Fixes**
  * `log1p` now preserves input data correctly when run without in-place updates, and no longer writes unnecessary metadata.
  * Scaling embeddings no longer adds summary statistics to feature metadata when the operation targets embedding data.
  * `scale` now updates feature statistics only when scaling the main matrix or a layer, improving consistency across data locations.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bd53304a84b6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.