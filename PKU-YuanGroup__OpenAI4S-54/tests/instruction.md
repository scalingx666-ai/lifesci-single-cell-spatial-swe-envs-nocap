# Issue

**Title:** fix(ci,contract): exempt dependabot by branch, and unpin a raced response shape

## Description

Two independent gate defects found while reviewing the eight open PRs. Both redden **required** checks for reasons that have nothing to do with the change under review, so both were blocking the Dependabot queue rather than protecting it.

## 1. The branch-naming policy exempted Dependabot by *actor*, not by branch

`ci.yml` had:

```yaml
if: github.event_name == 'pull_request' && github.actor != 'dependabot[bot]'
```

directly under a comment that says *"dependabot branches (dependabot/...) are exempt"*. The comment describes the intent; the condition does not implement it.

`github.actor` is whoever triggered the **latest** run, not who opened the PR. The moment a maintainer clicks "Update branch" on a Dependabot PR, the actor becomes the maintainer, the job stops being skipped, and it fails a `dependabot/uv/...` branch name it was never meant to judge.

That would be a curiosity except that `protect-main` sets `strict_required_status_checks_policy: true`, so **every Dependabot PR after the first merge must be updated before it can merge**. The exemption reliably stopped applying exactly when it was needed. Observed live on #49: `Branch naming policy` went `SKIPPED` → `FAILURE` on nothing but a branch update.

Net effect: no Dependabot PR could be merged through the front door without an admin bypass — consistent with the fact that this repository has never merged one.

The condition now keys on the head ref, which is what the policy is actually about, and `tests/test_governance.py` pins the actor/ref distinction so the regression cannot come back quietly.

## 2. `POST /example/session [ok].error` was frozen as a type the route does not guarantee

`_ExampleSeedState.start()` holds `self._lock` across `thread.start()`, and the handler re-acquires it to read `last_error()` — so whether the captured value is `null` or a string is decided by GIL scheduling. The frozen shape said `string`, so `scripts/capture_response_schemas.py --check` failed at random, taking the **required** `Offline tests (py3.12)` check down with it on PRs that touch nothing related. Commit `120af6a` flipped it on an unchanged tree: green 03:05, red 03:26.

The `GET` entry for the same field of the same state object is already `["null", "string"]`. This makes `POST` agree. `check_compatible` passes an observation whose type set is a subset of the frozen one, so both scheduling outcomes now pass — without weakening any guarantee the route actually makes.

This is deliberately a one-field edit rather than a regeneration: the same check run also reports two additive `/compute/*` drifts, and regenerating here would freeze two runner-specific shapes into a file whose entire claim is that it was captured from real responses.

## Verification

- `uv run pytest` — 3517 passed, 9 skipped, 1 deselected. (One further failure, `test_byoc_confinement_scope.py::test_a_confined_process_cannot_read_the_repository`, is an artifact of running the suite from a linked git worktree, where `.git` is a file rather than a directory; the test is `@macos_only` so Linux CI skips it. Unrelated to this diff — filed separately.)
- `uv run pre-commit run --all-files` — all hooks pass.
- `uv run mypy` — via the `mypy-core` hook, passes.
- YAML re-parsed after the edit to confirm the `!` in `!startsWith(...)` is not read as a tag indicator; the `if` value parses as the intended plain string.

## Follow-ups not in this PR

- `.gitleaks.toml` path/value allowlist, so the already-triaged fixture findings stop re-staling every time a squash to `main` rewrites their commit SHA. Kept separate because a mis-declared `[extend] useDefault` silently disables the scanner — 0 leaks and "fixed" look identical — so it needs its own two-step CI verification.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7facf20a2b0d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.