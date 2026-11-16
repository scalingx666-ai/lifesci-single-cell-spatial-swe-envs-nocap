# Issue

**Title:** Update Python interoperability to use Miniconda, Conda, and reticulate

## Description

This PR updates and re-organizes the code examples in the Python interoperability chapter as follows:

- The first example section now uses Miniconda, Conda, and `reticulate` (instead of `basilisk`). This starts by installing Python with Miniconda, setting up a Conda environment with key dependencies, and then continues with the main example code using `reticulate` as previously. From there onwards, the code showing how to interact with the `anndata` object is the same as previously. Using Miniconda / Conda / `reticulate` for this first example (instead of `basilisk`) will hopefully make things simpler for readers who are new to R-Python interoperability, and may be working through this chapter interactively.

- The second example section then shows how to set up a virtual environment using `basilisk`, e.g. for enhanced reproducibility for more advanced users. This shows how to set up the environment, and then links back to the first example using `reticulate` once the environment is set up.

- However, in the second example, I am currently also getting an error from GitHub Actions when setting up the virtual environment using `basilisk`, so I have commented this out with `eval = FALSE` for now. Hopefully we can fix this at some point, but for now, I think it is still worth merging these updates for the upcoming Bioc release, since the first example using Miniconda / Conda / `reticulate` is working and should be easier for readers to follow.

- The Conda environment from the first example (Miniconda / Conda / `reticulate`) should also be possible to re-use in later chapters, e.g. the cell-cell communication chapter. The environment is named `py-interop` so you can access it.

@Artur-man and/or @HelenaLC could you please have a look at this and check that my updates make sense?

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bf2906a5deab`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.