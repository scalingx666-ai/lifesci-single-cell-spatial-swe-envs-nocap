# Issue

**Title:** feat(tl): channel QC and ERP helpers for multichannel electrophysiology

## Description

## Summary
Channel quality control and ERP helpers for multichannel electrophysiology in `ov.tl` (`channel_qc_table`, `bridged_channel_pairs`, `erp_channel_outliers`, `repair_reject_epochs`, `channel_erps`, `trigger_onsets`, `bandpass_filter`).

- Dropout / saturation / sustained in-band noise / partial-recording noise segments scored per window against each channel's own typical level and the other channels (no exact-zero tests, no montage needed).
- Windowed bridging detection; event-locked screen that predicts each channel's evoked response from its most correlated neighbours.
- Repair / rejection after bad-channel exclusion; trigger-onset recovery (first edge after each nominal time, never past the next event, interpolation for missing pulses).
- All thresholds are keyword arguments with physical or relative defaults; no channel names, montage or dataset constants.

## Validation
- Came from the terminal-bench-science task `eeg-erp-recovery`, run with omicos 0.5.4: 43/43, reward 1 on three runs.
- Blind held-out task built from a different real dataset (ERP CORE P3, 28 channels, injected defects with recorded truth): 21/21, reward 1.
- Synthetic tests in `tests/tl/` (not re-run for this PR branch).

Companion omicos-admin PR:

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `af354858bfb6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.