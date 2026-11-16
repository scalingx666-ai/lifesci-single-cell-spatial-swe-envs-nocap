# Issue

**Title:** ov.read: storage='disk' by default; anndataoom + dask become core deps

## Description

- `ov.read(path)` defaults to `storage='disk'`: AnnDataOOM in cpu / cpu-gpu-mixed mode, Dask row blocks in GPU mode. `storage='memory'` returns a plain AnnData.
- `anndataoom>=0.1.9,<1.0` and `dask[array]` are now dependencies (wheels for Linux x86_64, macOS x86_64/arm64, Windows, py3.9–3.14); the `[rust]` extra stays for old install commands.
- Error messages for a missing anndataoom or an unsorted CSR X suggest `storage='memory'`.
- Tests updated for the new default; `test_qc_sccomposite_oom_copies_results_back` (needs torch) removed.
- omicverse_guide bumped (t_storage_mode marks disk as default).

Local: tests/pp/test_dask_mode.py, tests/others/test_oom_backend.py, tests/mcp/test_docs_examples.py, tests/pp/test_inmemory_cpp.py — 37 passed, 3 skipped (anndataoom 0.1.9, anndataoom-fast 0.1.5, dask 2026.8.0).

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `88f34b86e404`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.