# Issue

**Title:** Add parallel velocity dynamics PoC

## Description

Hi, @VolkerBergen ,
I hope you're doing well. Since the `tl.velocity_dynamics` is can be easily parallelized, I figured I'd be a good idea to make it so.
This PR is just a proof of concept and not meant to be merged (I've just copy-pasted a function we use in CellRank + I think you will want to handle things differently). On pancreas, I achieve speedup from ~10mins to ~3:45 (8 cores), just for free.

. .

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9f610d72ada2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.