# Issue

**Title:** Fix scaling of phi in line with empirical bayes approach

## Description

- scaling of `mu.mu` in `.EmpiricalBayesMu` to match the scale given by spike-ins
- scaling of `mu0` in `.BASiCS_MCMC_Start` to match the scale given by spike-ins
when using an EB prior for mu
- lower minimum tolerance `mintol_mu` (1e-5 instead of 1e-3) as a default value
in `.BASiCS_MCMC_ExtraArgs`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `75577c4ad34d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.