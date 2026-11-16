# Issue

**Title:** Add --skip_qc_report parameter to skip Quarto report rendering

## Description

## Summary
- Add a `--skip_qc_report` pipeline parameter (default: `false`) to optionally skip rendering the Quarto QC HTML report in `reports/`.
- Gate the `QC_REPORT` process in `SCDOWNSTREAM` so large runs can bypass the memory-heavy report step while keeping MultiQC and other pipeline outputs unchanged.

## Test plan
- [ ] Run the default test profile and confirm `reports/qc-report.html` is still produced
- [ ] Re-run with `--skip_qc_report` and confirm the pipeline completes without `reports/qc-report.html`
- [ ] Confirm MultiQC output is unchanged in both cases

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a27ce66eabb1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.