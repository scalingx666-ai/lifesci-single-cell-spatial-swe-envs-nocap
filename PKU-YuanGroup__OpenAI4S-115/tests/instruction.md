# Issue

**Title:** fix: MCP tools discovery crash, false-ready env steps, uv fallback

## Description

## Summary

Three independent user-reported defects around connector discovery and environment setup, each reproduced by a new test before the fix:

### 1. `host.mcp.tools(server)` crashed with `'str' object has no attribute 'get'`

`host.mcp.list()` and `host.mcp.call(...)` worked, but every discovery call failed — the exact triple reported against `volcengine-datapro`. The kernel SDK sends the server as a bare positional string (`["<server>"]`, the one MCP SDK method that does), and when `mcp_tools` grew a control tool the dispatcher began handing that string to `ListMCPToolsTool.execute()`/`resource_keys()`, which read it as a spec dict. Both methods now accept the dual shape — the same contract `LineageGetTool` already implements. The `resource_keys` half also stops audit rows degrading to `mcp:*` for every discovery.

Existing connector tests drove `dispatcher._m_mcp_tools(...)` directly and never crossed the control-tool adaptation; the new tests all go through `dispatcher.__call__`, the path the worker RPC takes.

### 2. A failed `host.env.create` rendered as "Setting up the <name> environment — ready"

`preinstall.install` reports failure as a structured `{"ok": false, "failed": [...]}` result, not the dispatcher's single-key `{"error"}` soft-fail, so the activity-step projection fell through to the success branch and — with nothing installed — summarized "ready" over an install that never happened. `_step_end` now reads the declared `ok` flag via `_declared_failure_reason`, carries the real reason (the `failed` entry's error, e.g. `No module named pip`, or the log tail) onto the card, and the step status ends `error` instead of `done`. The structured result the model sees is unchanged.

### 3. `host.env.create` hard-coded `python -m pip`, unusable in a pip-less uv venv

Including the daemon's own `.venv` that `setup.sh` builds with uv (verified on this machine: `_has_pip()` is False, uv on PATH). `_pip_install` now probes for the pip module and falls back to `uv pip install --python <sys.executable>`, targeting the same interpreter; with neither present it fails with a message naming both remedies. Only tool *selection* falls back — a failed install under a present pip is reported as-is rather than retried with uv, which would blur attribution.

## Validation

- 17 new tests across `tests/test_mcp_tools_positional_server.py`, `tests/test_env_setup_failure_projection.py`, `tests/test_preinstall_uv_fallback.py` — each written red against the defect first
- `uv run mypy` (strict set includes `host_dispatch.py`) clean
- 98 existing tests around the touched surfaces (connector allowlist, artifact control tools, MCP service, native tools, startup no-implicit-install, preinstall confinement) pass
- `harness.cli run --tier pr --offline`: 38/38 pass
- `pre-commit run --all-files` clean
- Real end-to-end: `preinstall.install(["six"])` inside a fresh pip-less uv venv succeeds via the uv fallback and the package imports

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a3b12f5eb159`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.