# Issue

**Title:** ci: reuse dependency builds and streamline backend checks

## Description

Dependency setup rebuilt large libraries under run-specific cache keys, repeated optional backend preflights across platforms, and installed article environments even when no article changed. Use dependency-aware caches, two installation workers, an early article change check, and a single Linux contract job that reuses the compiled package. Optional backend caches now follow the resolved dependency plan rather than stale installation specifications.

Reference builds install hard and website dependencies and render without examples. Publishing workflows share a concurrency group and queue all complementary publication jobs; mixed README, NEWS and help changes rebuild all affected outputs. Remove the redundant weekly cache warmer while preserving the three main check platforms, all twelve R-hub platforms, full article builds and the existing no-examples package-check policy.

Document SingleR marker and reference aggregation parameters explicitly, require thisutils 0.5.3 for the existing verbosity API, and repair the CCCDB and Presto test setup so source-mode tests do not accidentally call Ensembl or replace scop S3 methods. Production analysis function bodies are unchanged.

Validation:
- Full local source-mode testthat suite: 10,635 passes, zero failures/errors, 257 existing warnings and 21 unchanged skips. No new warning signatures; the existing parallel shutdown message did not leave processes from the test group.
- Documentation/static checks: zero errors/warnings and three existing metadata/Makevars notes. All 354 reference pages, home, NEWS and search built without warnings.
- Changed workflow syntax, incremental scope cases, actual backend checks, and a resolved-plan external cache/install roundtrip passed locally. R-hub and package Version/Date are unchanged. The renv-generated thisutils record is synchronized to 0.5.3; all other 499 dependency records and R metadata are preserved.
- The local dependency-load stack imbalance was independently reproduced in SparseArray 1.10.10 and cleared with the official fixed release in an isolated validation library. This PR adds no native patch, warning suppression or package SHA pin.

Local validation ran on macOS. Optional backend dependency plans were resolved, but all four complete optional backend installations and Python training were not repeated. The local actionlint version predates the supported `concurrency.queue` field; remaining workflow syntax passed with that field isolated, and its value was checked against current GitHub documentation. New-head GitHub CI validates the full configuration and provides the platform checks; no Linux speedup is claimed before observing the new jobs.

Follow-up validation: the first pushed head passed macOS, Windows and Linux package checks, the Linux backend contracts, reference build and all four actual optional backend installations/tests. It retained the same existing notes about utils::tail visibility, unused C flags and uv temporary lock files seen in the baseline CI. The automatically generated thisutils lock record was then updated to satisfy the new minimum; isolated renv restore and scop source namespace load passed. Keep Presto and speckle installed in the three main check environments to preserve platform test coverage, while avoiding their duplicate source preflights. Final-head CI is repeated after these two follow-ups.

Final head `1f46cd6c60b11766cc8564c687301060d7da10fe` passed all three platform package checks, the Linux contract job and reference build. macOS: 7,357 passes / 230 existing test warnings / 234 optional skips; Windows: 7,221 / 230 / 247; Linux: 7,356 / 231 / 231. All had zero failures and compiled code checks passed, with no stack imbalance. macOS and Windows had no package-check warnings. Linux retained one baseline warning from SummarizedExperiment's duplicate upstream import, which checkDocFiles labels under missing documentation despite listing no missing scop entries. Existing utils::tail visibility, unused C flags and uv temporary-file notes are unchanged. The automatic review's dependency-lock finding was fixed and resolved after an actual isolated restore/load check; all other 499 records are unchanged.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f089f714c42a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.