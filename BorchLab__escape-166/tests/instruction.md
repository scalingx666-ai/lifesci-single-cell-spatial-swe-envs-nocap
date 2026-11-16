# Issue

**Title:** fix color.by bug and introduce summarise.by feature for geyserEnrichment

## Description

Hi @ncborcherding, 

This turned out to be a bigger adventure than originally expected. I'm sorry that this pull request now introduces a lot of changes. I am aware that this is not ideal to review. 

- color.by bug covered in issue 
- implement summarise.by argument to summarise/collapse data by meta data column proposed in issue 
- formatting of help section of two functions was not properly displayed, fixed with commit 
- Commit  moves summary helper function to utils.R since it's now used by two functions
- enables `scaling` if `color.by` is another feature (i.e. gene set) in `geyserEnrichment()`

Best wishes,
Tobi

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b013e248030f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.