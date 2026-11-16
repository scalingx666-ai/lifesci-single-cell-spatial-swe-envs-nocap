# Issue

**Title:** logging improvements and version bump

## Description

**Version bump:** 0.19.3 → 0.19.4

**API URL migration:** `prod.cytetype.nygen.io` → `cytetype.nygen.io` (across `main.py`, `README.md`, and integration tests)

**Progress display rewrite (`cytetype/api/progress.py`):**
- Replaced the per-cluster progress bar (individual cluster status with colored symbols) with a simpler single-line job-level status (queued / running / waiting)
- Added **Jupyter notebook support** — detects `ZMQInteractiveShell` and uses an IPython `DisplayHandle` to update a single output cell in-place instead of printing repeated lines
- Added elapsed time display (`MM:SS`) in interactive terminals
- Spinner animation still updates in TTY mode; plain/non-TTY mode deduplicates repeated status lines
- `finalize()` now accepts an explicit `final_status` string (`completed`, `failed`, `timed_out`) and only shows failed cluster details on failure
- Constructor accepts an optional `stream` parameter for testability

**Polling loop improvements (`cytetype/api/client.py`):**
- `_sleep_with_spinner` now receives `job_status: str` instead of the full `cluster_status` dict, matching the simplified progress display
- New `_log_report_cta()` helper that logs the report URL prominently under a `[TRACK PROGRESS]` heading
- Report URL is logged **before** the initial polling delay (so users see it immediately)
- Log messages simplified: removed the job ID from the "submitted" message, rewrote the disconnect recovery hint
- Report URL is also logged on failure and timeout paths

**Post-annotation report link (`cytetype/main.py`):**
- After `annotate()` completes, the report URL is logged from `adata.uns["{prefix}_jobDetails"]["report_url"]`
- Minor formatting fix in `validate_adata` call arguments

**Tests:**
- New `tests/test_api_client.py` — unit tests for `ProgressDisplay` (plain output dedup, notebook display handle updates) and `wait_for_completion` (verifies report CTA is logged before polling begins)
- `tests/test_cytetype_integration.py` — updated default API URL assertion
- `tests/test_validation.py` — reformatted `@pytest.mark.parametrize` calls (style-only, no logic changes)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f1b0d099940f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.