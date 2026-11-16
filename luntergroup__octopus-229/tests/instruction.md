# Issue

**Title:** fix buffer overrun

## Description

.

Tested an error is thrown now rather than segfaulting:

```
[2022-01-20 02:08:17] <EROR>     In sample l-ovary, calls at chr10:133069535-133069536 &
[2022-01-20 02:08:17] <EROR>     chr10:133069535-133069538 were called in the same phase set but have
[2022-01-20 02:08:17] <EROR>     different genotype ploidies (2 & 3).
﻿```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4b334d5987b4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.