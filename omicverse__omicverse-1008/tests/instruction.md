# Issue

**Title:** feat(single,space): add moscot temporal and spatial transport adapters

## Description

Adds temporal optimal transport, single-cell to spatial mapping, and slice coupling. Checks convergence by default and returns native moscot problems without overwriting physical coordinates.



Related to #989; this PR covers only moscot and does not close the full roadmap.



Original isolated-branch validation: 20 tests passed, 0 skipped, on the isolated branch, including the real backend tests in `tests/test_roadmap989_moscot.py` and common input validation. Commands and limitations are documented in `docs/roadmap989-moscot.md`. Real training uses small synthetic data; it is not a biological accuracy benchmark.



This is an independent PR against master. Shared validation code is identical across the nine backend PRs; no other backend API is included. Remote CI is re-running for the review follow-up.

## Review follow-up (2026-11-11)

Documented the optional backend's explicit minimum Python version, which can be higher than OmicVerse's base requirement.

On the final combined tree, the eight non-moscot backend suites plus common validation passed 33 tests with no skips using the existing Python 3.12 environment (scvi-tools 1.5.2, Novae 1.1.2, pertpy 1.4.0, pyLemur 0.3.1). The moscot suite plus common validation passed 20 tests with no skips in its separate environment. The common tests overlap; these counts are not additive unique coverage. Small synthetic runs validate execution/contracts, not biological accuracy. Diff whitespace checks passed. New remote checks are pending.



## Current-master validation (2026-11-13)

Merged upstream master at 19bfb26d (2.4.3), retaining both moscot and the upstream Scanpy optional dependency. Focused suite: 20 passed, no skips. The combined nine-PR tree passed 35 non-moscot/common and 20 moscot/common tests without skips; shared tests overlap. Base import did not eagerly load optional backends. Small-data execution and contract validation only. Remote checks on head b1f9c373 completed: 9 successful checks and 4 intentionally skipped checks, with no failures. Python 3.10/3.11/3.12 build and test jobs all passed.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `19bfb26d08e6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.