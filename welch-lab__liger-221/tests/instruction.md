# Issue

**Title:** U algorithm

## Description

Hello @Akriebs !

Thank you very much for the amazing UINMF algorithm. I really enjoyed reading the preprint!

I found a very small bug that generates an error when one of the modalities has no unshared features. I here provide the fix that helped me run the code on my data. I thought this might be useful to you too. The fix accounts for the fact that `is.null(logical(0))` returns `FALSE`. Using `length(...) == 0` fill return `TRUE` for both `NULL` and `logical(0)`

Good luck with the submission process!

Best, 
Chris

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b0b4deb70c89`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.