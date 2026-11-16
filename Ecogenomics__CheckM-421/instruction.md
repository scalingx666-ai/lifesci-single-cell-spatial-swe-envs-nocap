# Issue

**Title:** fix(1.2.6): fixes for issues #387, #402, and #386

## Description

Bumps the version to 1.2.6 and fixes three open issues.

## #387: `NameError: free variable 'mask' referenced before assignment`
`HMMERRunner.align()` only checked hmmalign's return code inside the `--allcol` retry branch (return code 256). Other failures, such as hmmalign missing from `PATH` or being killed for lack of memory, were ignored. The resulting empty alignment then failed in `_maskAlignment` with an unhelpful `NameError`.
- Any non-zero hmmalign return code is now reported and the process exits with code 1. Previously it exited with `sys.exit(rtn)`, and a wait status of 256 becomes exit code 0.
- `_maskAlignment` reports a clear error when the `#=GC RF` mask line is missing.
- The parent process now checks worker exit codes after the parallel alignment steps and stops if any worker failed. Previously it continued with missing alignments.

## #402: `OSError: AF_UNIX path too long` with `--tmpdir`
`--tmpdir` sets `tempfile.tempdir` for the whole process. The `mp.Manager()` socket is created in that directory, and Linux limits socket paths to about 108 characters. Since Python 3.12 the temp path is always made absolute, so even a short relative `--tmpdir` can go over the limit. The multiprocessing temp directory is now created in the system default location before `--tmpdir` takes effect. CheckM's own temporary files still go to `--tmpdir`.

## #386: `checkm coverage` drops bins
Sequences were stored in a dict keyed on sequence ID alone. When bins came from different assemblies that reuse contig names (e.g., `k141_1`, `NODE_1_...`), later bins overwrote earlier ones and whole bins disappeared from the output. Sequences are now tracked as (bin ID, sequence ID) pairs, so every bin is reported.

BAM files identify reference sequences only by name. When a sequence ID appears in more than one bin, BAM coverage is assigned to a bin's copy only if the BAM reference length matches that copy's length, and a warning is logged. Sequences sharing both ID and length can't be told apart, so their coverage is assigned to every bin containing them; the warning says so. Other readers of the coverage file (`profile`, `qa --coverage_file`) already group rows by bin ID and are unaffected.

Addresses #386. This is the most likely cause, but the reporters haven't confirmed it yet.

## Testing
- `checkm test` (E. coli end-to-end) passes all 5 steps with Python 3.11, HMMER, pplacer, and the 2015-01-16 reference data.
- Each issue was reproduced on `master` and confirmed fixed on this branch:
  - #387: a failing hmmalign now exits with code 1 (`master`: 0, and the parent continued). An empty alignment now gives a clear error instead of an unhelpful failure.
  - #402: with a 212-character `--tmpdir`, `mp.Manager()` now works (`master`: `OSError: AF_UNIX path too long`).
  - #386: tested with two bins from different assemblies that share contig IDs. Both bins are now reported (`master` dropped `binA` entirely), with coverage assigned by length.
- Unit tests in `checkm/test`: 21 of 24 pass. The 3 errors in `test_genomicSignatures.VerifyBinStatistics` also fail on `master`, because that test still calls private methods renamed in 1.2.1.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `acb42ba20b29`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.