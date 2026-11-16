# Issue

**Title:** Contents verification for save_monocle_objects

## Description

Adds safety around save_monocle_objects() by writing outputs to a temporary staging directory, repeatedly verifying file checksums for stability, and atomically swapping the final directory with rollback protection; new stability_attempts/stability_sleep parameters cover the retry behavior in io.R. New helpers wait_for_monocle_object_stability() and move_monocle_save_directory() support the checksum retry and atomic move flow. Test fixtures for save/load (monocle_objects.01.tar, transform_models.01.tar) and UMAP expectations in test-io.R are refreshed to match the stabilized outputs. Repository instructions for Codex are documented in AGENTS.md.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f50b920d61c1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.