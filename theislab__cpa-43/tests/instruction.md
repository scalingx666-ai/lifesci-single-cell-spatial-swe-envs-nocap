# Issue

**Title:** fix jax deps

## Description

# Issue

 Encountered by @erialc-cal

Importing cpa fails after following the installation tutorial due to the call to jax.random.KeyArray in ... which was already depracated in 0.4.16 and recently (Feb. 6th) removed in 0.4.24, see [here](https://jax.readthedocs.io/en/latest/changelog.html#jax-0-4-24-feb-6-2024) for more details.

`>>> import cpa`
`[rank: 0] Global seed set to 0`
`...[trace]...`
`AttributeError: module 'jax.random' has no attribute 'KeyArray'`


# How to  Reproduce

1. `conda create -n cpa python=3.9`
2. `conda activate cpa`
3. `pip install git+https://github.com/theislab/cpa`
4. `python`
5. `>>> import cpa`


# Fix/Changes

Added jax version upper bound in pyproject.toml, also added same for jaxlib to avoid consistency errors for jax.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7cda37e9cca2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.