# Issue

**Title:** fix(release): unblock the v0.2.0 PyPI dispatch — twine dist hygiene + the gateway-test port race

## Description

Two independent failures stand between v0.2.0 and PyPI; this PR removes both.

## 1. `pypi` job: twine refuses the build receipt (run 32835188788)

The first complete `pypi_only` dispatch reached **Publish to PyPI with OIDC** and died in twine's check phase:

```
Checking dist/openai4s-0.2.0-py3-none-any.whl: PASSED
InvalidDistribution: Unknown distribution format: 'build-receipt-dist.json'
```

The `python-package-distributions` artifact deliberately carries `build-receipt-dist.json` — staging verifies against it — but `gh-action-pypi-publish` hands twine the whole `dist/` directory, and twine refuses anything that is not a wheel or an sdist.

**Fix:** a `Keep only index-distributable files` step between download and publish deletes everything but `*.whl` / `*.tar.gz` from this job's own workspace. The artifact and every other consumer stay untouched.

Verified: `twine check` passes both the wheel and the sdist built from this tree (`PASSED` × 2), so nothing else in the check phase is waiting behind the receipt.

## 2. `Frozen response shapes`: port-allocation race under xdist (run 32834796854)

PR #126's CI lost the Frozen-shapes job to one red test:

```
FAILED tests/test_team_auth_routes.py::test_proxy_mode_never_mints_service_identity_from_machine_token[X-OpenAI4S-Token]
  OSError: [Errno 98] Address already in use
the suite failed (pytest exited 1); the capture would be incomplete ...
```

Not schema drift — `_free_port()` probes a port, closes it, and the daemon rebinds it later. Under `pytest -n 4` any concurrent worker can take the port in that gap, and one red test makes the capture refuse to report, by design. The same probe-then-rebind pattern existed at **eight gateway binds across six test files**; this job happened to lose `test_team_auth_routes` first.

**Fix:** `tests/_ports.bound_gateway_server()` binds `("127.0.0.1", 0)` once with a placeholder handler and keeps the socket; the caller hands the real port to `Config`/`make_handler` (which snapshots `cfg.port` for the Host allowlist — the reason the fixtures were stuck on probe-then-rebind) and then attaches the real handler class. `socketserver` resolves `RequestHandlerClass` per accepted request and accepts nothing before `serve_forever`, so the placeholder never handles anything. All eight binds now go through it; the auth-exit `restart()` keeps its same-port rebind because the cookie under test is bound to that port; config-only `_free_port` uses stay (an unbound number has no race to lose).

`tests/test_ports_helper.py` pins the contract by recording the bind sequence — **mutation-checked**: a probe-then-rebind helper fails it with the recorded double bind (`[('127.0.0.1', 0), ('127.0.0.1', 59698)]`), and the naïve "port is held after the call returns" assertion was proven unable to tell the two implementations apart (a rebinder also holds the port by then).

## Verification

- Full offline suite, CI parallelism (`-n auto --maxprocesses=4 --dist loadfile`): green
- 5 × stress rounds of the four race-prone files under `-n 4`: green
- Mutation cycle on the new contract test: genuine green → probe-mutant red → restored green
- `check_directory_readmes.py`: 120 directories, complete bilingual coverage (both READMEs list the new files)
- `pre-commit` on all touched files: passed
- Local `twine check` on the 0.2.0 wheel + sdist: PASSED × 2

After merging: re-dispatch `release.yml` with `tag=v0.2.0`, `pypi_only=true`. The only step that remains unproven is the OIDC↔PyPI trusted-publisher exchange itself, which nothing but a real run can exercise.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ed037385bb3a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.