# Issue

**Title:** ord parameter from project_to_curve was removed from princurve 2.0.4

## Description

Hi Kelly,

In a recent chain of events, I've had to reimplement `princurve::project_to_curve` in Rcpp instead of Fortran. In doing so, I removed the `ord` parameter. I thought nobody was using it and it's trivial to call `project_to_curve(x, s[ord,])` instead of `project_to_curve(x, s, ord)`. Unfortunately, this caused Slingshot to fail starting from princurve 2.0.4. This pull request should solve the problem. I hope this is okay for you.

Robrecht

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5254e4ce5f62`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.