# Issue

**Title:** Submit 5.3.1 to CRAN

## Description

Final updates before submitting `Seurat` v5.3.1 to CRAN 🚀 

- [x] Bump version
- [x] Finalize changelog
- [x] [Pre-Release Checks](https://github.com/satijalab/seurat/actions/workflows/release_checks.yaml)
- [x] Reverse Dependency Checks (checked with `revdepcheck`)
- [x] [win-builder](https://win-builder.r-project.org/) (R-release, R-devel, R-oldrel)
- [x] [macOS builder](https://mac.r-project.org/macbuilder/submit.html) (R-release, R-devel)
- [x] Update CRAN comments

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `296df42be05a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.