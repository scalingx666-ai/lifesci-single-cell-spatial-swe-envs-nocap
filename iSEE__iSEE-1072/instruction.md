# Issue

**Title:** Better code export

## Description

Going from

<img width="1828" height="246" alt="image" src="https://github.com/user-attachments/assets/35c69270-0ebd-4aeb-9036-77c4ff543169" />

to

<img width="380" height="478" alt="image" src="https://github.com/user-attachments/assets/b51d16e7-966b-471a-a6c4-421ff39a7741" />

(no modifications added to the exported code itself, just simply the corollary formatting)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9ce16f7f8556`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.