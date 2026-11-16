# Issue

**Title:** Docs update: recommend baysor/proseg installation via their bioconda recipes

## Description

Now, we suggest running the command below to install baysor and proseg:
```sh
conda install bioconda::rust-proseg
conda install bioconda::baysor-cpp
```

The error logs when the executable is not found are also updated to have clear instructions.

### Minor modifications
- Also removed `genes=500` in the main tutorial (was failing with the new proseg version)
- Renamed `long` test mark into `cellpose_v4` mark, since it was used only for cellpose

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `eae5842b60d2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.