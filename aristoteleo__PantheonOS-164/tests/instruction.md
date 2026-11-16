# Issue

**Title:** fix(sandbox): remember the channels, so bioconda packages install

## Description

`conda install samtools` in a sandbox answers:

```
samtools =* * does not exist (perhaps a typo or a missing channel)
```

samtools is on **bioconda**. `micromamba create -c conda-forge` applies that channel to *that command only* — it is not written into the environment — so every later install searched the defaults and nothing else.

For a workspace whose users install bioinformatics tools, that is most of what they will reach for: samtools, bwa, STAR, salmon and the rest are all bioconda.

The `.condarc` goes at the root prefix on the Volume, so it covers every environment there including ones the user creates themselves, and it is left alone if it already exists — a workspace that has set its own channel order keeps it.

Reported from a real sandbox, not found by review.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01BhPiGNfkhLZ89Sqhoz9ebP

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `864fb3171150`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.