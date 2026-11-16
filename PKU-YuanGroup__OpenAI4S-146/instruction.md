# Issue

**Title:** fix(security): run keychain CLIs detached from the controlling terminal

## Description

## Summary

On macOS the keychain backend of `SecretBroker` shells out to the `security`
CLI through `_run()` in `openai4s/security/secret_broker.py`, and stores a
secret with `security add-generic-password -w`, passing the value on stdin.
`security -w` reads the password with readpassphrase(3), which opens
`/dev/tty` in preference to stdin whenever the process has a controlling
terminal. A daemon launched from a shell (`./start.sh`) inherits one, so the
CLI prints `password data for new item:` on the user's terminal, ignores the
value piped in, and blocks until `_CLI_TIMEOUT_S` (10 s). The round-trip
self-test then fails and, because `auto` fails closed by design, the daemon
refuses to handle credentials at all:

```text
SecretStoreUnavailable: refusing to handle credentials without a secure store
(macos-keychain present but unusable: Command ['security',
'add-generic-password', '-U', '-a', 'v2/<namespace>/__selftest__/probe', '-s',
'openai4s', '-D', 'OpenAI4S credential', '-w'] timed out after 10.0 seconds)
```

So a Mac with a perfectly good, unlocked login keychain cannot start the daemon
from a terminal in the default mode.

Fix: `_run()` now passes `start_new_session=True` to `subprocess.run`. A fresh
session has no controlling terminal, which is exactly the case
readpassphrase(3) handles by falling back to stdin. The Linux backend
(`secret-tool store/lookup/clear`) reads stdin unconditionally, so it is
unaffected; `find-generic-password` / `delete-generic-password` never read a
password interactively.

The keychain path dates from 6bf85f8c (`feat(secrets): put model/search
credentials behind a broker reference`). No existing issue tracks this; I hit
it on a fresh install.

## Area

- [ ] Web UI / frontend
- [ ] Agent / loop / delegation
- [ ] Kernel / host RPC / runtime
- [ ] Server / gateway / API
- [ ] Store / provenance / artifacts
- [ ] Skills / science runtime
- [ ] Compute / remote execution
- [x] CLI / config / packaging
- [x] Tests / harness / CI
- [ ] Docs

## Change Type

- [x] Bug fix
- [ ] Feature
- [ ] Refactor
- [ ] Test / harness
- [ ] Documentation
- [x] Security-related change
- [ ] Release / packaging

## Verification

Ran:

```text
uv run pytest                              # 5 failed, 8062 passed, 43 skipped, 4 deselected, 2 warnings in 1350.84s (0:22:30) — the 5 failures are pre-existing on this macOS host (note below)
uv run mypy                                # Success: no issues found in 8 source files
uv run pre-commit run --all-files          # 10 hooks passed, 0 skipped, 0 failed
uv run pytest tests/test_secret_broker.py  # 95 passed (includes the new regression test)
```

Note on the 5 `uv run pytest` failures: all are in
`tests/test_delegation_env_inheritance.py` and `tests/test_env_kernel_binding.py`,
none of which touch the secret broker. They assert that a kernel spawned through
a symlinked env `bin/python` reports that symlink as `sys.executable`; on this
host (macOS 27, Homebrew framework Python 3.12 behind a venv) a child started
through such a symlink reports the Homebrew binary instead. An untouched
`origin/main` checkout fails exactly the same 5 tests on this machine, and CI
runs the suite on `ubuntu-latest`, where the symlink path is preserved.

Manual, on macOS 27.0 (26A5416b), Apple silicon:

- Before the fix: `./start.sh` from Terminal.app leaves a `security
  add-generic-password … -w` child waiting on /dev/tty (visible in `ps`);
  after 10 s the daemon aborts with the `SecretStoreUnavailable` error above.
- After the fix: same launch, no prompt, keychain self-test passes, daemon
  listening on :8760. Also reproduced under a pseudo-terminal (pty) so the
  child provably had a controlling tty during the check.

Not run:

```text
Linux secret-tool path against a live Secret Service
```

Reason:

```text
secret-tool reads the secret from stdin unconditionally, so start_new_session
is a no-op for it; the existing stubbed-backend tests still pin the
argv/stdin contract. I had no Linux desktop with a Secret Service at hand.
```

## Risk and Reviewer Focus

- `openai4s/security/secret_broker.py::_run` is the single choke point for all
  six keychain CLI calls (macOS add/find/delete, Linux store/lookup/clear), so
  the flag applies to every one of them. I found no call that wants a
  controlling terminal; please double-check that reading.
- `start_new_session=True` also detaches the child from the terminal's
  foreground process group, so a Ctrl-C in the terminal no longer reaches it
  directly. The call is bounded by `timeout=_CLI_TIMEOUT_S` and
  `subprocess.run` kills the child on timeout, so it cannot outlive the call.
- setsid changes only the POSIX session; the Mach bootstrap/audit session is
  untouched, so keychain access and unlock prompts behave as before (the manual
  run above stored and read back a keychain item successfully).
- Regression test:
  `tests/test_secret_broker.py::test_cli_runs_detached_from_the_controlling_terminal`
  (offline, `stubbed_backend`; a synthetic secret is asserted to travel on
  stdin and never appear in argv).

## Checklist

### Diff Readiness

- [x] I reviewed and understand the full diff.
- [x] This PR is small and single-purpose.
- [x] No unrelated formatting, broad rewrite, or drive-by refactor is included.
- [x] Hotspot files were edited surgically if touched: `gateway.py`,
      `host_dispatch.py`, `store.py`, `worker.py`, `manager.py`. (none touched)
- [x] Workbench changes were made in `frontend/` (not legacy `app.js`)
      and `openai4s/server/webui/dist/` was rebuilt and committed with the
      source. (n/a — no UI change)
- [x] `openai4s/server/webui/vendor/` and `tests/fixtures/` were not
      reformatted.

### Tests

- [x] Relevant tests or manual checks were run and listed above.
- [x] No new test requires live LLM, network, GPU, SSH, Docker, lab hardware,
      or secrets in the default offline suite.
- [x] No tests were deleted without tracked replacements.
- [x] Kernel / host-RPC / gateway changes include focused contract coverage or
      a documented smoke test. (n/a — none touched)

### Core Dependency Policy

- [x] No hard third-party import was added to the core engine, LLM client, or
      stdlib web server.
- [x] Optional science imports are guarded by `try/except ImportError` at every
      in-tree use site. (n/a — none added)
- [x] New dependencies, if any, are documented and justified. (none)

### Public Disclosure and Security

- [x] No secrets, API keys, tokens, real credentials, private data, model
      weights, or local absolute paths are included.
- [x] No unpublished research roadmap, internal assignment, benchmark detail,
      or unreleased experimental result is disclosed.
- [x] Security-sensitive changes include appropriate synthetic tests or manual
      verification notes.
- [x] Docs do not overstate isolation, sandboxing, privacy, or security
      guarantees.

### Docs

- [x] Docs match actual code behavior. (no doc describes the previous fallback)
- [x] User-facing behavior changes are reflected in docs or release notes where
      appropriate. (behavior now matches what the docs already promise)
- [x] `README.md` and `README_zh.md` stay in sync where translated sections are
      affected. (n/a — untouched)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e91ae47c91ec`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.