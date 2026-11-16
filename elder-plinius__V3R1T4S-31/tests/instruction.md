# Issue

**Title:** fix: honor requested checker timeout in workspace mode

## Description

## Upstream draft handoff and fresh local verification

Submitted from , branch `DmitrL-dev:fix/workspace-checker-timeout`.

- Exact tested HEAD: `02253de9721380c81ba75b7bbb6d7489e1b40473`.
- Parent and current upstream `main`: `9b1d444eb864a1475e092047d49612a7410a7c5a`.
- Exactly three changed files: `kit/check_run.py`, `kit/tests/test_workspace_timeout.py`, and `kit/tests/README_workspace_timeout.md`. No other toolkit fixes or upstream history are included in this patch.
- Open upstream PRs were checked for equivalent changes and changed-file overlap. PRs #1 and #30 touch different checker sections; neither duplicates this timeout propagation fix.

Fresh local checks on Python 3.9.6:

- `python3 kit/tests/test_check_run.py`: **39/39 tests passed**, exit 0. This direct command runs the original file only.
- `python3 -m unittest discover -s kit/tests -p 'test_*.py' -v`: **46/46 methods passed**, exit 0, including all seven new timeout regressions.
- The seven new tests run against the unmodified current-upstream checker reproduce four failures: workspace, setup, selected-run, and multiple-outbox-package timeout propagation. Direct-package, default-timeout, and no-exec controls pass. The corrected source passes all seven.
- `git diff --check` passed and the checkout stayed clean.

Package execution and the read-only Git probe were mocked in the focused tests. No third-party submission scripts or scientific computations ran. GitHub Actions has no runs for this fork HEAD; these are local tests, not GitHub CI.

**Before any future merge, the maintainer must coordinate regeneration and verification of root `SHA256SUMS` against the complete final integrated tree, including full path coverage and hashes for these three files and any preceding changes.** This draft intentionally does not change that manifest.

The original fork description and README limitations are preserved below as the original submission record. Its Linux/Python 3.12 verification is historical; the fresh handoff tests above used local Python 3.9.6.

---

## Fresh standalone base
Fork-only draft on an immutable snapshot of current upstream main:
- Base commit: `9b1d444eb864a1475e092047d49612a7410a7c5a`
- Fork review base: `review-base/upstream-9b1d444`
- The fork's `main` and frozen PRs #1–#6 are unchanged.

Upstream moved by two documentation/guide commits during preparation. The full comparison has no `kit/` changes; checker and original-test blobs remain `c2c0736697cb88afc49ff0e9f326d7a8f98cfdcf` and `5db97ffa377929f56a87abcdc5d1ecb389097f34`. The timeout bug is still present, and prior upstream toolkit PRs remain unmerged. This patch has no dependency on those PRs.

The snapshot base keeps this PR's diff to exactly three files: checker, focused regression tests and README. It avoids including the unrelated upstream guide changes or updating fork main.

## Reproduction and three-line runtime fix
The global CLI option says `--timeout N` is seconds allowed for run_checks.sh. A mocked CLI replay showed:
- `--package P --timeout 7`: clean/mutant invocations receive 7, 7.
- `WORKDIR --timeout 7` and `WORKDIR --setup --timeout 7`: receive 900, 900.

Forward the parsed timeout into check_workspace and then into each package check. Keep default 900, direct package behavior and --no-exec unchanged. This is per invocation, not a total-workspace deadline. No subprocess implementation or verifier acceptance policy changes.

## Exact HEAD and verification
HEAD: `02253de9721380c81ba75b7bbb6d7489e1b40473`.
Tree: `da0779b3f8e19ac9f514a260c300220a07535591`.

All three remote changed files and the original test file were read back and matched the verified bytes. Tests were rerun locally on those exact-HEAD files:
```sh
python3 -m unittest discover -s kit/tests -p 'test_*.py' -v
```
**46/46 methods passed** (39 original + 7 new). The new suite fails four cases before the change: workspace, setup, selected run and multiple outbox packages. Package/default/no-exec controls remain passing.

Independent review approved runtime, tests and README, independently reran 46/46 on corrected exact source bytes, and checked timeout 7 at the mocked subprocess boundary. Local compatibility replay atop the other proposed toolkit fixes passed 114/114 methods. Focused tests mock package execution and the read-only Git probe. No third-party submission scripts, scientific campaigns, descendant-process or resource-stress experiments ran. No remote CI is claimed.

## Explicit limits and integration requirement
This does not add output-byte limits, process-group/descendant termination, cleanup-failure reporting, sandboxing or infrastructure-error recovery. The related bounded lifecycle audit is a research report, not a security-exploit claim.

Root SHA256SUMS is intentionally unchanged. Before integration, maintainers must verify complete path coverage and hashes on the final tree, including the new test/README and any other landed changes. Recheck actual upstream and duplicate PRs before manual upstream handoff. No upstream submission, merge or release is performed.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9b1d444eb864`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.