# Issue

**Title:** fix(compute): read the run's GPU host registry, never the process default

## Description

## Summary

Runs with an explicit `Config(data_dir=...)` previously read the process-default GPU registry in their prompts, Settings routes, and remote-science services. That could expose another registry's hosts and select them for remote work. The prompt, Settings API, and dispatcher services now use the owning run's data directory, consistently with `host.compute`. This builds on merged #222 and targets `main`.

Ordinary registry reads and the Guardian fallback no longer initialize the process-default directory. Registry writes preserve owner-only directory permissions for both new and existing directories. The regression test reproduced the previous `0755` result for existing directories before the fix and passes with `0700` afterward. Legacy `OPENAI4S_FOLD_SSH` seeding remains supported and writes only to the selected registry.

## Area

- [ ] Web UI / frontend
- [ ] Agent / loop / delegation
- [x] Kernel / host RPC / runtime
- [x] Server / gateway / API
- [ ] Store / provenance / artifacts
- [ ] Skills / science runtime
- [x] Compute / remote execution
- [ ] CLI / config / packaging
- [x] Tests / harness / CI
- [x] Docs

## Change Type

- [x] Bug fix
- [ ] Feature
- [ ] Refactor
- [ ] Test / harness
- [ ] Documentation
- [x] Security-related change
- [ ] Release / packaging

## Verification

Local commands use a disposable `OPENAI4S_DATA_DIR` and `OPENAI4S_SKIP_DOTENV=1`.

```text
uv run pytest -n auto --maxprocesses=4 --dist loadfile \
  tests/test_kernel.py tests/test_agent.py tests/test_gateway.py \
  tests/test_process_default_data_dir.py \
  tests/test_host_remote_capability_service.py tests/test_host_remote_science_service.py \
  tests/test_host_accelerators.py tests/test_remote_capability_probe.py
# 581 passed

uv run python scripts/capture_response_schemas.py --check
# 11382 passed, 34 skipped; 1198 captured route/status shapes;
# 215/215 routes; no breaking response-shape changes.
# Run outside the command sandbox: the earlier attempt hit denied macOS
# process/Seatbelt and R /dev/fd operations. No application policy changed.

uv run python scripts/capture_response_contract.py --check
# 215/215 routes; contract up to date

uv run pre-commit run --all-files
# All hooks pass, including strict mypy and CSS token checks

uv run python -m harness.cli run --tier pr --offline
# 38/38 passed
uv run python -m harness.cli characterize
# MATCH r5_prechange.json

uv run python scripts/check_directory_readmes.py
# Complete bilingual coverage
uv run python scripts/source_secret_scan.py
# Passed

node tests/browser_smoke.mjs
# Passed against ./start.sh, isolated data/home, Chromium and the science extra
```

An additional real-browser Settings → Compute check added, displayed, and removed an SSH alias, checked the selected registry on disk, and confirmed no default-home registry was created. Its SSH executable was a local fixture; no remote GPU or real SSH host was contacted. Chromium required execution outside the command sandbox because macOS denied its Mach port registration inside it.

Hosted validation at `c2db6e3a8692e86388be213376e816addad8665c`: [CI passed](https://github.com/PKU-YuanGroup/OpenAI4S/actions/runs/38218844339), with 26 successful jobs and 3 intentionally skipped nightly jobs. Python 3.10/3.12/3.13/3.14, frozen response shapes, all three browser engines, container, and both Linux sandbox checks passed. [Protocol fuzzing](https://github.com/PKU-YuanGroup/OpenAI4S/actions/runs/38218844287), CodeQL, and the external security check also passed. Bugbot returned neutral because its usage limit was reached; it did not complete a review. The branch contains current `main`, has no conflicts or review threads, and still requires Code Owner approval before merge.

Not run locally: Docker/container and Linux bubblewrap checks (macOS host), Firefox/WebKit, or frontend tests/build (no frontend source or dist changes). Hosted CI covers those gates. No live LLM, SSH, GPU, or hardware validation is claimed.

## Risk and Reviewer Focus

- `host_dispatch.py`: both remote services resolve `DataDirRegistry` from the current dispatcher Config for each call.
- `server/gateway.py`: both prompt-note call sites and all remote-GPU registry routes explicitly pass the owning data directory; response shapes are unchanged.
- `compute/registry.py`: ordinary reads neither create nor chmod directories. Writes, including legacy environment seeding, harden the selected directory. POSIX hardening remains best effort on unsupported filesystems/platforms.
- `permissions.py`: fallback flags/budgets still come from the process Config without initializing its directories.
- `tests/test_process_default_data_dir.py`: distinct default/run registries, Settings CRUD, remote-service routing, daemon compatibility, directory modes, and legacy seeding. Regression coverage already merged through #222 is preserved.
- Code Owner approval remains required by repository policy; passing automation is not a human approval.

## Checklist

### Diff Readiness

- [x] I reviewed and understand the full diff.
- [x] This PR is small and single-purpose.
- [x] No unrelated formatting, broad rewrite, or drive-by refactor is included.
- [x] Hotspot files were edited surgically: `gateway.py` and `host_dispatch.py`.
- [x] No workbench source or dist changes; no legacy `app.js` changes.
- [x] Vendored assets and captured fixtures were not reformatted.

### Tests

- [x] Relevant tests and manual checks are listed above.
- [x] No new default-suite test requires live resources or secrets.
- [x] No tests were deleted without tracked replacements.
- [x] Host/gateway changes include focused tests and a real-browser smoke check.

### Core Dependency Policy

- [x] No hard third-party core import was added.
- [x] No optional science import was added.
- [x] No dependency was added.

### Public Disclosure and Security

- [x] No secrets, real credentials, private data, model weights, or local absolute paths are included.
- [x] No unpublished research roadmap or unreleased experimental result is disclosed.
- [x] Security-sensitive changes include synthetic regression coverage.
- [x] Docs distinguish ordinary reads, legacy seeding, and platform-dependent permission hardening.

### Docs

- [x] Docs match actual behavior.
- [x] Compute and test directory documentation describe the changed behavior.
- [x] English and Chinese documentation remain aligned.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7a031aa866e6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.