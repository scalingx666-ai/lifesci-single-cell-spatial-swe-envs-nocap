# Issue

**Title:** Ccc aggregate + ligand-target subtask fix

## Description

<!-- You can erase any parts of this template not applicable to your Pull Request. -->

### Submission type
CCC task ligand-target random results fix & add types of aggregation.

* [ ] Set seed to random baseline
* [ ] Add specificity and magnitude rank-aggregate
* [ ] Revert odds ratio to `top_prop` param - reason for random performance in ligand-target task

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3d24e8f09520`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.