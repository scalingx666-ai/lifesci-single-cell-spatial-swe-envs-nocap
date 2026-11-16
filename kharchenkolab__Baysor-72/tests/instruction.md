# Issue

**Title:** Fix issue loading prior segmentation from csv column.

## Description

I ran into a couple issues trying to run Baysor on some Xenium using the segmentation from 10x's software as prior segmentation in Baysor, which I've fixed here.

First was assigning a number to a String field, and second was `load_prior_segmentation!` not returning what it was assumed to return.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `455bdf824d55`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.