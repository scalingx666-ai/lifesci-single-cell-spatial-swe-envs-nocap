# Issue

**Title:** fix: restore package startup information

## Description

Restore the Logo, package version, update date and website shown by `library(scop)`. Update the package date to 2026-10-16.

Startup messages continue to respect verbosity settings and `suppressPackageStartupMessages()`. Python initialization remains opt-in.

Validation: sourced startup-hook assertions passed using the updated DESCRIPTION as package metadata, covering Logo, version/date, website, both suppression paths and Python initialization gating. `git diff --check` passed. Full package installation and R CMD check were not run.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4086d6a4b88e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.