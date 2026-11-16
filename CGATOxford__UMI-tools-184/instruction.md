# Issue

**Title:** {ts} speed up stats

## Description

This pull request significantly improves the run time for `dedup --output-stats`. By way of an example, for a file containing ~4M read to be deduped, with ~1M 10bp UMIs observed, on the master branch running with stats takes ~17h to complete! Without stats the run time is a mere 147s. With the changes herein, the run time with stats is now 380s.

Currently, we are selecting random UMIs for each position separately, taking into account the frequency with which each UMI is observed in the input BAM. Since `np.random.choice` takes essentially the same amount of time to return 100,000 elements at random (with replacement) as it does for 1, the change here is use `np.random.choice` to create an array of 100,000 random UMIs from which we select each in turn when we need a random UMI, re-creating the array when we have used each element.

@IanSudbery - Would you mind reviewing this when you have a moment. The test file had to be updated since the random selection is not consistent with the previous method but this is unavoidable as far as I can see.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4bd1f235db80`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.