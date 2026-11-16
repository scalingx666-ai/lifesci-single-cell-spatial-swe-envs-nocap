# Issue

**Title:** Fix startup metadata lookup during development loading

## Description

The restored startup hook looks up metadata under libname as though it were always an installed library. Under pkgload, that path need not contain an installed scop package, so load_all() fails with "there is no package called scop" before development tests or documentation can run.

Read Version, Date and URL from the loaded namespace's DESCRIPTION instead. Preserve the Logo, version/date/site output, verbosity, suppressPackageStartupMessages() behavior and existing opt-in Python initialization.

Validation: pkgload::load_all(..., quiet=TRUE, compile=FALSE) succeeds in a source worktree without an installed package under its parent. Six startup assertions pass with no failures/errors/warnings/skips, including a nonexistent libname and both suppression modes. Scoped formatting and diff checks pass. Final combined ATAC package checks are tracked in #511; hosted checks for this new head are pending. No version or date bump is introduced by this repair.

This follows upstream #512 and is included in the open ATAC branches so their development/documentation loading remains usable.

Final combined acceptance in #511 at 07c4147836aed27c6892108b2657bd06c595863a: 37 WNN/startup assertions passed; the complete required as-cran check reached DONE with 0 errors, 0 warnings, 4 notes and process status 0. This is combined-branch evidence, not a separate full local check of this standalone PR. This PR's hosted checks remain independently visible.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `483e2e569e59`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.