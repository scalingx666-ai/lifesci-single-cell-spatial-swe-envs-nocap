# Issue

**Title:** VERSION: correct 1.3.0 memory figures

## Description

Corrects the memory figures in the 1.3.0 change-log entry of `checkm/VERSION` before tagging v1.3.0. This entry is shown on the docs change-log page and included in the sdist.

- gPlace: ~18 GB with 64 threads (was 12 GB). pplacer with the full tree: ~45 GB (was 35 GB). These figures are from the cgroup measurements on the Performance docs page.
- Removed the claim that gPlace needs less memory than pplacer did with the reduced tree (< 16 GB). With 64 threads it does not.
- The `--gplace_max_memory` example `6G for 128 bins` is now `8G`. It notes that the results are identical and points to the Performance page.

One line changed. No code changes.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b0e8ded77233`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.