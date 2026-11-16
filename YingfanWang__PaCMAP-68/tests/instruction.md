# Issue

**Title:** Support changing number of iterations for each optimization stage

## Description

Hello.

I've been using PaCMAP for some time by now, and recently started wondering why the user can specify the number of iterations essentially only to the third and final optimization stage. As far as I understand, these values are derived from empirical evidence, and I'm not convinced that the hard-coded values work best for all scenarios.

In this PR, I propose changing the `num_iters` argument from a single `int` to a `tuple[int, int, int]`, so that the user can specify the number of iterations in each optimization stage.

I would like to know your thoughts about it.

**EDIT**: I also added backward compatibility for `num_inters` as a single integer. If a single integer is provided, the proposed implementation in this PR falls back to the original values: `num_inters = (100, 100, num_inters)`, preventing change of behavior in pre-existing code.

Best regards.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1274eb01d5fe`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.