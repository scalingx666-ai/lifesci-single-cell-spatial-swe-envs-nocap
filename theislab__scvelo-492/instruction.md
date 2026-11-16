# Issue

**Title:** Extend `pl.velocity_embedding_stream` with new arguments

## Description

Adding new streamplot arguments:

- arrow_size: Scaling factor for the arrow size, addressing 
- arrow_style: Arrow style specification, '-|>' or '->'.
- max_length: Maximum length of streamline in axes coordinates.
- integration_direction: Integration in 'forward', 'backward' or 'both' directions.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `599bf65cbb0b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.