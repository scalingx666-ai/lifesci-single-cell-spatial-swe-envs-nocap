# Issue

**Title:** Effective length fix

## Description

This is a fix to do the "correct" calculation for effective length. What we had before was correct for targets near the tail end of the fragment length distribution, but wrong for short things. Often, this wasn't an issue, but even if you have some spurious alignments going to those things, the TPM would blow up.

Design:
- Compute the conditional mean fragment length up to the maximum length we store in the FLD (currently 1000bp)
- For each target, store it's 'conditional mean'. This vector get thrown around now instead of the 'mean'
- new eff_len_i = targ_len_i - mean_i + 1

On the cuffdiff2 dataset, it seems to fix some of the spurious big TPM values. Take a look at the short things around 2^6 - 2^7 length wise

Before:

![screen shot 2015-07-01 at 7 48 10 am](https://cloud.githubusercontent.com/assets/530217/8462126/63d84e92-1fe6-11e5-8f75-2d3649e68ccf.png)

After:

![screen shot 2015-07-01 at 7 48 37 am](https://cloud.githubusercontent.com/assets/530217/8462155/97076956-1fe6-11e5-88b5-bdd4f45503c6.png)

Simulations show a similar improvement.

Because we are now using a vector, for single-end data I just dump the user supplied frag len mean into every position. Maybe we should just throw a normal in there like everyone else? The tricky part will be the standard deviation. I think most people just pick something, but it might not be a bad idea to look at a few datasets and maybe cook together a table if it seems to be conditional on the mean.

**TODO**
- @pmelsted, the only thing I haven't done yet is to update the bias functions. I'm going to take a close look tomorrow, but it would be nice to have you look it over

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `32e02f647a5c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.