# Issue

**Title:** Retrieve the downloaded resources with pooch

## Description

Moves `li.rs.get_metalinks` and `li.rs.get_hcop_orthologs` onto `pooch.retrieve`, caching under `scanpy.settings.datasetdir` instead of `os.getcwd()` — they were leaving untracked files in whatever directory you ran from and re-downloading whenever it changed. MetaLinksDB gains a pinned sha256, so a truncated copy is re-fetched rather than cached forever. `pooch` already arrives with `scverse-misc[datasets]`, so this adds no dependency and drops one: `requests` is no longer imported.

Also fixes a leaked sqlite connection in `get_metalinks_values`. Net -63 lines.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1e466c5c8177`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.