# Issue

**Title:** Metric odds ratio fix

## Description

<!-- You can erase any parts of this template not applicable to your Pull Request. -->

### Submission type

* [ ] This submission fixes a bug (link to related issue: )

* Inverts `rank_aggregate` - ascending, hence relevant when we aggregate via max/sum

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `17b6f681e4ec`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.