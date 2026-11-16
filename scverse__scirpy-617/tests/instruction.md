# Issue

**Title:** Improved result matrix stacking for Hamming GPU implementation

## Description

@grst Recently I tried the GPU implementation of the Hamming distance metric with 8 million cells of the Omniscope Covid dataset, which is the largest dataset that is currently available. I noticed performance problems with stacking the blocks of the final result matrix that are computed by GPU. Therefore I implemented a numba function to stack the blocks efficiently - stacking only takes 6 seconds now for 8 million cells with 1 CPU. 
With the new stacking implementation I was able to run 8 million cells in ~210 seconds with an Nvidia A30 GPU at the cluster with the GPU hamming metric (~2000 seconds with 64 CPUs with the CPU hamming metric).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fbe2310cf865`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.