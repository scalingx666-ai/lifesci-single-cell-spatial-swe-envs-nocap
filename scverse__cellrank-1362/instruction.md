# Issue

**Title:** Support pip install of PETSc/SLEPc; drop mpi4py from petsc extra

## Description

## Changes

* **Drop `mpi4py` from the `petsc` extra** (`optional-dependencies.petsc = [ "petsc4py", "slepc4py" ]`). pyGPCCA runs serially and never needs `mpi4py`; pinning it forced a system-MPI source build that made `pip install "cellrank[petsc]"` fail on any machine without a system MPI library (e.g. stock macOS, minimal Linux). Users who genuinely want a distributed MPI build can still install a system MPI and add `mpi4py` themselves.
* **Document the pip install path for PETSc/SLEPc** in `docs/installation.md`: a new "PETSc and SLEPc (faster large-scale solvers)" subsection covering `pip install "cellrank[petsc]"`, the from-source compilation caveat, and the C-only `PETSC_CONFIGURE_OPTIONS` recipe for systems without a Fortran/MPI toolchain.

## Bug fixes

* **Correct the inaccurate "conda-only" framing.** The docs previously called PETSc/SLEPc "conda-only packages" and implied conda was the only way to get them. They are pip-installable from PyPI sdists; the conda section is reframed as the *pre-built, no-compilation* option, cross-linked with the new pip instructions.

## Context

`petsc4py`/`slepc4py` enable pyGPCCA's fast `method='krylov'` solver for macrostates and fate probabilities. Without them, pyGPCCA falls back to `method='brandts'`, which densifies the transition matrix and emits warnings (`Unable to import petsc4py or slepc4py ...` / `Densifying`). conda ships prebuilt binaries, but pip-from-source is viable and only needs a C compiler — no Fortran or MPI — once `mpi4py` is out of the way.

### Verified

- `petsc` 3.25.2 + `slepc` 3.25.1 compile from PyPI sdists on macOS arm64 with a C compiler only, using `PETSC_CONFIGURE_OPTIONS="--with-fc=0 --with-mpi=0 --with-debugging=0 --with-shared-libraries=1"` (no Fortran, MPI, or system libs).
- `petsc4py`/`slepc4py` import and report versions.
- pyGPCCA `GPCCA(..., method='krylov').optimize()` runs under `warnings.simplefilter('error')` — i.e. the `brandts`/densify fallback is gone — **without** `mpi4py` installed.
- `cellrank[petsc]` resolves to `petsc`/`petsc4py`/`slepc`/`slepc4py` with no `mpi4py`.
- `pre-commit` passes on the changed files.

## Notes for reviewers

- The from-source build was validated on **macOS arm64**; the configure flags are platform-agnostic, but a Linux CI confirmation would be a nice follow-up. The Windows note in `installation.md` is intentionally unchanged (PETSc on Windows remains hard; WSL is still the recommendation).
- No `mpi4py` is bundled anymore — if any downstream tooling assumed `cellrank[petsc]` pulled in `mpi4py`, that is the one behavior change here.

## Related issues

Closes #

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4ab38230c771`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.