# Issue

**Title:** fix(mcp): put leidenalg in the mcp extra so the server can run the tool it advertises

## Description

`MCP Tests` has failed on every scheduled run since at least 2026-06-22 — six consecutive weeks — while every PR check stayed green. The workflow is path-filtered to `omicverse/mcp/**` and `tests/mcp/**`, so it only runs on its weekly schedule and never appears in a PR's checks.

```
tests/mcp/test_real_p0_pipeline.py::test_full_p0_pipeline
AssertionError: ov.pp.leiden failed: Please install the leiden algorithm
```

`leidenalg` is commented out of the core dependencies deliberately — C extension, not wheel-available everywhere — and survives only in `[full]`. But `scripts/ci/mcp-core-runtime.sh` installs `[tests,mcp]`, and `[mcp]` is a single line of `mcp>=1.0`.

So the MCP server advertises `ov.pp.leiden` as a tool that its own extra cannot install. That is not only a CI artefact: `pip install omicverse[mcp]` followed by a call to that tool meets the same wall.

Adding it to `[mcp]` rather than restoring it to core keeps the platform constraint that motivated commenting it out in the first place. `igraph` is already a core dependency.

Verified by running the test that has been failing: **6 passed**.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `dbdcf754d26c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.