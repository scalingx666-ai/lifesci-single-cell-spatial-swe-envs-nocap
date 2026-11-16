# Issue

**Title:** Feature/hestbench flexibility

## Description

**This PR**
* Makes some changes to integrate HestBench more easily into an evaluation pipeline without being restricted to the CLI to run it
* Removes redundant `benchmark_eval` function (everything is in `benchmark`)
* Minor fix to `CustomInferenceEncoder` in the `inf_encoder_factory` 

**Run instructions** 
* Run HestBench evaluation as given in `tutorials/4-Running-HEST-Benchmark.ipynb`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c8bef8c60069`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.