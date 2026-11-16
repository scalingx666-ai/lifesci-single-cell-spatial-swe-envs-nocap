# Issue

**Title:** Add `single-cell-rna-qc` skill

## Description

Added skill for performing quality control on single-cell RNA-seq data.

The skill folder itself was directly copied over from https://github.com/anthropics/agent-skills/tree/main/tmp-examples/skills/single-cell-rna-qc

Tested loading the plugin locally via the following commands in Claude code:
- `/plugin marketplace add /Users/jwei/code/life-sciences`
- `/plugin install single-cell-rna-qc@life-sciences`

After which:
<img width="1400" height="518" alt="CleanShot 2025-10-19 at 22 07 53@2x" src="https://github.com/user-attachments/assets/4a0cb809-70f2-4044-82aa-bb7a2e7bcef0" />

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8e69e621380c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.