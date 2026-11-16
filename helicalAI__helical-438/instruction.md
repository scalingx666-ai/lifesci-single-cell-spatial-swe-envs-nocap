# Issue

**Title:** perf(downloader): validate each file once per process, keep cache when offline

## Description

## What

- `Downloader.download_via_name` checks a file against the remote once per process. Before, every call sent a HEAD request and hashed the file.
- If the remote cannot be reached, a cached file is kept and a warning is logged. Before, a failed HEAD deleted a valid file. A missing file is still downloaded.
- `check_file_valid` returns `False` when the remote cannot be reached.
- The static Ensembl table is parsed once per process.

## Checks

New tests in `ci/tests/test_utils/test_downloader.py`:

- one check per process across instances
- cache kept on a connection error and on a 403
- a mismatched file is replaced
- a missing file is downloaded
- a file deleted after its check is downloaded again
- the Ensembl table is parsed once

Breaking each change fails a test.

Version 3.1.4.

.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f190498b3497`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.