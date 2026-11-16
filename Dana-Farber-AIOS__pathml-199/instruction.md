# Issue

**Title:** Dataloader

## Description

This PR adds the `TileDataset` class to `pathml.ml` module. I ran some benchmarks and used the implementation based on the fastest one (see details in #131). I also added some documentation and tests for the new dataloader. I removed the old implementation of the dataloader and associated tests. 

I think this is a very important feature since it forms the bridge between digital pathology domain (i.e. pathml) and the broader domain of machine learning (everything built on top of PyTorch). There may still be room for performance improvements but I am using the best practices from [here](https://discuss.pytorch.org/t/dataloader-when-num-worker-0-there-is-bug/25643/16) and benchmarking allowed us to avoid a different implementation which was 3-4x slower.

This

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `58cbfd368c4d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.