# Issue

**Title:** Fix deprecation GUI warnings for private napari attribute access

## Description

Replace `Window._dock_widgets` with the public `dock_widgets` property (removing now-redundant `.widget()` calls since the public API returns the inner widget directly). Remove dead-code assignments to `DataModel._region_key` and `DataModel._instance_key`, whose backing fields are never read — the public properties derive both values from `get_table_keys(self.adata)` — and drop the unused dataclass fields.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3dfb2c003948`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.