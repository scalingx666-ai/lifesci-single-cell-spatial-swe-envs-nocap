# Issue

**Title:** fix: more accurate validation on geneset name

## Description

#### Reviewers
**Functional:** @tihuan @colinmegill 

---

## Changes

- modify
  -  rewrite parts of the validation code to be more accurate, also change some copy


https://user-images.githubusercontent.com/8716829/133507093-d63501bd-c2cb-4811-bf52-737de9c5fdc8.mov



#2414

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0634160c0c5b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.