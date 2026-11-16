# Issue

**Title:** Ts speed up stats

## Description

@IanSudbery After discussing with @MikeDMorgan I've implemented a two-stage random sampling since the original array of probabilities contains the same probability multiple times (e.g 1/n, 2/n, 3/n, ..., where n is the total umi counts) This speeds up the random sampling ~5-fold for the BAM from Roy Francis (see below) so the total run time decreased from ~28 minutes to ~10 minutes. This may be a particular case where the gains are larger since the distribution of UMIs is a long way off uniform. I'd expect the improvement to be marginal where the distribution of umis is more "random".

I've checked the stats output is consistent.

Can you think of any scenario where this method of sampling would be significantly less efficient?

previously...
ncalls  tottime  percall  cumtime  percall filename:lineno(function)
  4400216 1373.266    0.000 1426.919    0.000 {method 'choice' of 'mtrand.RandomState' objects}
  4400216   18.888    0.000 1445.807    0.000 dedup.py:776(getUmis)

two-stage sampling...
  8995437  219.319    0.000  268.225    0.000 {method 'choice' of 'mtrand.RandomState' objects}
  4400216   24.821    0.000  300.054    0.000 dedup.py:789(getUmis)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8b9443f74ce7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.