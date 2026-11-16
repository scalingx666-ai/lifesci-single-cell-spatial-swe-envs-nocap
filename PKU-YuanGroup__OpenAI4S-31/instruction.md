# Issue

**Title:** feat: improve scientific environment setup

## Description

## Summary

Improve the scientific environment setup flow so contributors can keep a lightweight control environment while optionally creating or synchronizing comprehensive Python and R kernel environments.

- add standard and full setup profiles plus non-pruning --update support
- add setup.sh --with-kernel-envs and --update-kernel-envs
- refresh the portable Python/R dependency manifests
- document the new workflow in English and Chinese
- add focused offline contracts for profiles, updates, manifests, and shell help

## Area

- [ ] Web UI / frontend
- [ ] Agent / loop / delegation
- [ ] Kernel / host RPC / runtime
- [ ] Server / gateway / API
- [ ] Store / provenance / artifacts
- [x] Skills / science runtime
- [ ] Compute / remote execution
- [x] CLI / config / packaging
- [x] Tests / harness / CI
- [x] Docs

## Change Type

- [ ] Bug fix
- [x] Feature
- [ ] Refactor
- [x] Test / harness
- [x] Documentation
- [x] Release / packaging

## Verification

Ran:

~~~text
.venv/bin/python -m pytest tests/test_setup_environments.py -q
# 9 passed

git diff --check
# passed

.venv/bin/pre-commit run --all-files
# passed: end-of-file fixer, mixed line endings, trailing whitespace,
# check-json, merge-conflict check, isort, and ruff
~~~

Not run:

~~~text
.venv/bin/python -m pytest
# collection stopped: ModuleNotFoundError: No module named 'pandas'

# The remaining pre-commit hooks could not complete locally:
# black: current hook is incompatible with Python 3.14 (ast.Str removed)
# mypy-core: uv cache is outside the writable sandbox
~~~

Reason:

~~~text
The local lightweight .venv does not contain the optional pandas dependency.
The Black and mypy failures are local tool/runtime constraints; ruff, isort,
focused tests, and diff checks passed.
~~~

## Risk and Reviewer Focus

The main behavior change is in openai4s/cli/main.py and setup.sh. Please verify:

- profile selection remains mutually exclusive with --only
- existing environments are skipped unless --update is explicit
- updates intentionally omit --prune
- the unpinned portable Conda dependencies resolve on supported macOS/Linux platforms
- pandoc=3.10 and pypdfium2==5.9.0 are available for the supported platforms

## Checklist

### Diff Readiness

- [x] I reviewed and understand the full diff.
- [x] This PR is small and single-purpose.
- [x] No unrelated formatting, broad rewrite, or drive-by refactor is included.
- [x] Hotspot files were edited surgically if touched: gateway.py, host_dispatch.py, store.py, app.js, worker.py, manager.py.
- [x] openai4s/server/webui/vendor/ and tests/fixtures/ were not reformatted.

### Tests

- [x] Relevant tests or manual checks were run and listed above.
- [x] No new test requires live LLM, network, GPU, SSH, Docker, lab hardware, or secrets in the default offline suite.
- [x] No tests were deleted without tracked replacements.
- [ ] Kernel / host-RPC / gateway changes include focused contract coverage or a documented smoke test.

### Core Dependency Policy

- [x] No hard third-party import was added to the core engine, LLM client, or stdlib web server.
- [x] Optional science imports are guarded by try/except ImportError at every in-tree use site.
- [x] New dependencies, if any, are documented and justified.

### Public Disclosure and Security

- [x] No secrets, API keys, tokens, real credentials, private data, model weights, or local absolute paths are included.
- [x] No unpublished research roadmap, internal assignment, benchmark detail, or unreleased experimental result is disclosed.
- [ ] Security-sensitive changes include appropriate synthetic tests or manual verification notes.
- [x] Docs do not overstate isolation, sandboxing, privacy, or security guarantees.

### Docs

- [x] Docs match actual code behavior.
- [x] User-facing behavior changes are reflected in docs or release notes where appropriate.
- [x] README.md and README_zh.md stay in sync where translated sections are affected.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `259a03d2c09b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.