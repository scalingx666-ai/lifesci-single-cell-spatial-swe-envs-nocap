# Issue

**Title:** chore(deps): batch the #93/#94/#95 Dependabot rollup into one branch

## Description

## Summary

Batches the three open Dependabot PRs — #93, #94, #95 — into one branch so the
whole Monday rollup clears the ruleset once instead of three times.

Each of those PRs is individually green and individually `BLOCKED`: `main`
requires a code-owner review **and** strict up-to-date status checks, so merging
any one of them invalidates the other two and forces a rebase + a full CI
re-run. Three sequential rounds of that for three one-line version bumps is the
deadlock this PR exists to short-circuit.

The three upstream commits are cherry-picked unmodified, with Dependabot's
authorship and messages intact, so the diff here is byte-identical to the union
of the three PRs:

| PR | Bump | Files |
|----|------|-------|
| #93 | `astral-sh/ruff-pre-commit` v0.16.1 → v0.16.3 | `.pre-commit-config.yaml` |
| #94 | `pre-commit` 4.6.1 → 4.6.2 (development-dependencies group) | `uv.lock` |
| #95 | `astral-sh/setup-uv` v9.0.0 → v10.0.1 (×17), `github/codeql-action/upload-sarif` v4.37.6 → v4.37.7 | `.github/workflows/{ci,release,scorecard}.yml` |

The three touch disjoint files, so the merge is textual-conflict-free; the only
real interaction is pre-commit 4.6.2 running ruff 0.16.3, verified below.

### The one bump that is not inert on its face

`setup-uv` v9 → v10 is a **major** bump, and its sole breaking change is that
the default `enable-cache: auto` now disables the cache on `pull_request_target`,
`workflow_run`, and `release` events (astral-sh/setup-uv#992, cache-poisoning
hardening). That is a class of change PR CI cannot exercise, so it was checked
against the triggers rather than against a green run:

- `ci.yml` — `push`, `pull_request`, `schedule`, `workflow_dispatch`
- `release.yml` — `workflow_dispatch` only (**not** the `release` event)
- `scorecard.yml` — `push`, `schedule`; does not use `setup-uv` at all

None of the three newly-affected events is fired by any workflow here, and no
workflow sets `enable-cache` explicitly, so caching behaviour is unchanged.
v10.0.1 on top is one bug fix (tolerate transient manifest timeouts).

`ruff` 0.16.2 + 0.16.3 change only `flake8-pyi`, `pylint`, `pyupgrade`,
`flake8-bandit` and `numpy` rules — none of which are inside the
`select = ["E", "F"]` pinned in `pyproject.toml`, which is exactly the
insulation that block's comment describes. `pre-commit` 4.6.2 is a single fix
for `language: node` hooks, and this repo has none.

Both new action SHAs were verified to be the commits their comments claim,
rather than trusted from the comment:

- `astral-sh/setup-uv@20cfd1bf945f4377ade1205e4dbc17946fc9a30d` → tag `v10.0.1`
- `github/codeql-action/upload-sarif@ff2f1c621b7f889edc0d3c761ac2e6a3f8cdb0dd` → tag `v4.37.7` (annotated tag `faaa5d80` dereferenced)

`grep` over `.github/` confirms no `setup-uv` or `codeql-action` pin was left
behind at the old SHA.

## Area

- [x] Tests / harness / CI

## Change Type

- [x] Release / packaging

## Verification

Ran:

```text
uv lock --check                                        # Resolved 52 packages, exit 0
uv sync --extra science                                # pre-commit 4.6.1 -> 4.6.2 installed
uv run pre-commit run --all-files                      # all 9 hooks pass under ruff 0.16.3 + pre-commit 4.6.2, no file rewritten
uv run python scripts/check_directory_readmes.py       # 103 dirs, 820 files, complete bilingual coverage
uv run python -m harness.cli run --tier pr --offline   # 3/3 PASS, 0 failed
python scripts/source_secret_scan.py                   # 1056 files, passed
uv run python scripts/capture_response_contract.py --check  # contract up to date: 156/156 routes
uv run pytest                                          # 4802 passed, 11 skipped, 0 failed (macOS/arm64, exit 0)
gh api .../git/ref/tags/{v10.0.1,v4.37.7}              # SHA <-> tag verification above
```

Not run:

```text
uv run python scripts/capture_response_schemas.py --check
bash scripts/container_smoke.sh
node tests/browser_smoke.mjs / browser_admission_fault.mjs / browser_matrix.mjs
```

Reason:

```text
The diff touches no route, serializer, Dockerfile, or frontend file, and CI
already ran every one of these green on #93, #94 and #95 individually and runs
them again here. The schemas check additionally re-runs the whole suite and is
known to report machine-local drift on the /environments routes, where
regenerating would bake this machine's conda env list into the frozen contract.
```

## CI note: the two cancelled Browser E2E checks are not from this PR

`Browser workbench E2E (chromium)` and `(webkit)` show as CANCELLED here. Both
hung for exactly 45 minutes and were killed by the job's `timeout-minutes: 45`;
GitHub reports a timed-out job as cancelled. The chromium log puts the stall
inside `npx playwright install --with-deps`, in `apt-get update`: the Azure
Ubuntu mirror `Ign`s out, apt falls back to `archive.ubuntu.com`, fetches
`noble-security InRelease`, and then goes silent for 44 minutes.

This is pre-existing and repo-wide, not introduced here:

| Run | Branch | Timed-out job |
|-----|--------|---------------|
| 32230729966 (Aug 19) | `next` (push) | Browser E2E (webkit) |
| 32174247550 (Aug 18) | `main` (schedule) | Browser E2E (chromium) |
| 32155083198 (Aug 18) | `fix/doubao-search-retired-socket-read` | Offline tests (py3.13) |
| 32058049231 (Aug 17) | `main` (schedule) | Offline tests (py3.13) |

`main`'s own scheduled runs hit the identical 45-minute timeout. Within this
PR's run, `firefox` used the same step and the same `setup-uv@v10` and passed in
1m56s, and the `setup-uv` step itself succeeded in the two jobs that hung — so
the bump is not implicated. It was re-run once; both hung again the same way.

All four **required** checks — `Lint (pre-commit)`, `Offline tests (py3.10)`,
`Offline tests (py3.12)`, `Branch naming policy` — are green. Browser E2E is not
a required check. Fixing the apt stall belongs in its own PR, not in a
dependency rollup.

## Risk and Reviewer Focus

Low, and concentrated in one place: `setup-uv` v9 → v10 is the only
non-patch bump. Reviewers should sanity-check the trigger argument above — if a
workflow later gains a `release`, `workflow_run`, or `pull_request_target`
trigger, that workflow silently loses its uv cache until `enable-cache: true`
is set explicitly.

Nothing in this diff reaches runtime code: it is three workflow files, one hook
pin, and one lockfile entry.

## Checklist

### Diff Readiness

- [x] I reviewed and understand the full diff.
- [x] This PR is small and single-purpose.
- [x] No unrelated formatting, broad rewrite, or drive-by refactor is included.
- [x] Hotspot files were edited surgically if touched — none are touched.
- [x] `openai4s/server/webui/vendor/` and `tests/fixtures/` were not reformatted.

### Tests

- [x] Relevant tests or manual checks were run and listed above.
- [x] No new test requires live LLM, network, GPU, SSH, Docker, lab hardware, or secrets in the default offline suite.
- [x] No tests were deleted without tracked replacements.
- [x] Kernel / host-RPC / gateway changes include focused contract coverage — none are touched.

### Core Dependency Policy

- [x] No hard third-party import was added to the core engine, LLM client, or stdlib web server.
- [x] Optional science imports are guarded — unchanged.
- [x] New dependencies, if any, are documented and justified — no new dependency, only version bumps.

### Public Disclosure and Security

- [x] No secrets, API keys, tokens, real credentials, private data, model weights, or local absolute paths are included.
- [x] No unpublished research roadmap, internal assignment, benchmark detail, or unreleased experimental result is disclosed.
- [x] Security-sensitive changes include verification notes — the two action SHAs are pinned and verified against their tags above.
- [x] Docs do not overstate isolation, sandboxing, privacy, or security guarantees.

### Docs

- [x] Docs match actual code behavior.
- [x] User-facing behavior changes are reflected in docs or release notes where appropriate — none.
- [x] `README.md` and `README_zh.md` stay in sync where translated sections are affected — untouched.

---

Supersedes #93, #94 and #95 — once this merges those three carry no remaining
delta and should be closed with their branches deleted. GitHub's `Closes`
keyword does not apply to pull requests, so that is a manual step, not an
automatic one.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bd7a6a89b63c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.