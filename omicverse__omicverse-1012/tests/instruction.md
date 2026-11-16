# Issue

**Title:** feat(space): add Novae spatial domain learning adapter

## Description

Trains Novae or runs zero-shot inference using a caller-supplied pretrained model. Copies embeddings and domain labels back in cell order while preserving input expression and graphs. No checkpoint is downloaded implicitly.

Related to #989; this PR covers only Novae and does not close the full roadmap.

Original isolated-branch validation: 14 tests passed, 0 skipped, on the isolated branch, including the real backend tests in `tests/test_roadmap989_novae.py` and common input validation. Commands and limitations are documented in `docs/roadmap989-novae.md`. Real training uses small synthetic data; it is not a biological accuracy benchmark.

This is an independent PR against master. Shared validation code is identical across the nine backend PRs; no other backend API is included. Remote CI is re-running for the review follow-up.

## Review follow-up (2026-11-11)

Added a real-backend test that trains a synthetic model, saves and reloads a local checkpoint, and performs zero-shot inference on two slides with a smaller gene panel. Checks slide-isolated graph edges, preserved input graphs/expression/coordinates, finite representations, labels and cell order. No public model is downloaded. Focused suite: 14 passed, no skips.

On the final combined tree, the eight non-moscot backend suites plus common validation passed 33 tests with no skips using the existing Python 3.12 environment (scvi-tools 1.5.2, Novae 1.1.2, pertpy 1.4.0, pyLemur 0.3.1). The moscot suite plus common validation passed 20 tests with no skips in its separate environment. The common tests overlap; these counts are not additive unique coverage. Small synthetic runs validate execution/contracts, not biological accuracy. Diff whitespace checks passed. New remote checks are pending.

## Current-master combination validation (2026-11-13)

The current PR head was included in a local combined tree with all nine roadmap adapters on upstream master 19bfb26d (2.4.3). Non-moscot/common tests: 35 passed; moscot/common tests in its separate backend environment: 20 passed; no skips. Common tests overlap. Base import did not eagerly load optional backends. This is small-data execution and contract validation, not a biological accuracy benchmark. Remote checks on the current PR head are complete: 9 successful and 4 intentionally skipped, including successful Python 3.10/3.11/3.12 builds/tests. No further code changes were needed in this PR for this check.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `af354858bfb6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.