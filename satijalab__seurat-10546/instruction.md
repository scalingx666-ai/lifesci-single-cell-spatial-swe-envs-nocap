# Issue

**Title:** Submit 6.0.0 to CRAN

## Description

Final updates before submitting `Seurat` v6.0.0 to CRAN 🚀 

- [x] Bump version
- [x] Finalize changelog
- [x] [Pre-Release Checks](https://github.com/satijalab/seurat/actions/workflows/release_checks.yaml)
- [x] [Reverse Dependency Checks](https://github.com/satijalab/seurat/actions/workflows/reverse_dependency_checks.yaml)
- [x] [win-builder](https://win-builder.r-project.org/) (R-release, R-devel, R-oldrel)
- [x] ~[macOS builder](https://mac.r-project.org/macbuilder/submit.html)~ (R-release, R-devel) see note below - checked locally
- [x] Update CRAN comments

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ac3e96038065`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.