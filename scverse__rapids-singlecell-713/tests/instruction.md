# Issue

**Title:** Update notebooks submodule: Mixscape & Mixscale pertpy tutorial

## Description

Bumps the `notebooks` submodule to pull in the extended pertpy-GPU tutorial.

Companion to scverse/rapids_singlecell-notebooks#11, which adds a **perturbation-efficacy** section to `05_pertpy.ipynb` demonstrating the new GPU tools shipped in 0.16.0:

- `rsc.ptg.Mixscape` — `perturbation_signature`, `mixscape`, `lda`
- `rsc.ptg.Mixscale` — `mixscale`

on the Papalexi 2021 ECCITE-seq screen, mirroring pertpy's [perturbation efficacy tutorial](https://pertpy.readthedocs.io/en/latest/tutorials/notebooks/perturbation_efficacy.html). The notebook was executed end-to-end on GPU (no errors; top knocked-out genes recover the IFN-γ pathway).

Submodule bump: `4970cf0 → 342313a`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `48377be34054`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.