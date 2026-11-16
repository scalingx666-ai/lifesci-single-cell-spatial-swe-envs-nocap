# Issue

**Title:** Add rsc support

## Description

This adds support for rapids-singlecell for the `over clustering` #110 . The results might differ a bit since rsc uses a brute-force knn approach and the leiden clustering is also slightly different. 

The overclustering step is now for 200k cells 15x faster (3min vs 12s). 

It's also set up in a way where when rsc fails to import it will default back to scanpy.

Please don't merge this yet since it uses the syntax that will be released with rapids-singlecell 0.10.0. This will come out shortly after scanpy 1.10.0

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `777f8e920854`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.