# Issue

**Title:** Backport categorical ComBat reference coding to 1.12.x

## Description

. Targets **1.12.x**, not main.

Backport the categorical-covariate reference coding already accepted in #4389. The current 1.12 maintenance branch still constructs a full set of categorical dummy columns alongside all batch indicators, introducing a redundant column. Use the same treatment coding as main and remove its intercept before combining the matrices.

This is a targeted backport of the existing correction, with new regression coverage. No solver, numerical threshold, dependency or unrelated function changes are included. Main and 1.11.x are not changed. Designs confounded for other reasons are outside this fix.

### Validation

- All seven new cases fail against the original maintenance-branch implementation.
- The corrected branch passes all 12 tests: seven new cases and all five existing ComBat tests, with no errors or skips.
- Coverage includes one or two categorical covariates alongside a numeric covariate, full-rank design, dense/CSR input, in-place and returned results, and a single-level categorical covariate.
- Corrected output matches explicit numeric reference coding to rtol=atol=1e-10; returned-result calls preserve the input expression matrix.
- The new tests pass Ruff and formatting checks; git diff --check passes.

Validation ran on the exact pinned source in the contributor fork's Linux/Python 3.12 workflow. The validation helpers and workflow are on a separate branch and are not included in this proposed diff. This is not upstream CI. The full repository suite, documentation build, other platforms and the reporter's dataset were not tested.

Fork evidence: https://github.com/sylvesterkaczmarek/scanpy/actions/runs/42367545452

### Post-submission verification

The release-note fragment has been renamed to 4496.fix.md. The targeted tests were independently rerun after the filename change and passed: 12 tests. Human review of the latest changes remains pending.

**LLM usage**

- [ ] LLM or coding agent used: GPT-6 via ChatGPT and Codex CLI v0.166.0 assisted with code, tests, documentation, and review. The Codex model version used for the original implementation was not independently recorded.
- [ ] If one was used, I, a human, have reviewed, understood and tested every changed line.

- [x] Tests included.
- [x] Issue reference included above; this change is limited to the 1.12 maintenance branch.
- [ ] Release notes not necessary because:

A release note is included as `4496.fix.md`, matching the assigned PR number.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f044749be194`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.