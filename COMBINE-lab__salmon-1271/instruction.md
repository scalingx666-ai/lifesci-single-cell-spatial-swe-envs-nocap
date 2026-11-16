# Issue

**Title:** fix(map): do not reuse the previous fragment's hits for a mate shorter than k

## Description

In `--sketch` mode, `map_read` is what clears a mate's cache, and it is skipped for a mate shorter than k. `merge_se_mappings` then read the previous fragment's hits, so a trimmed pair could be counted on the wrong transcripts or lose its orphan.

The cache is now cleared when the mate is skipped. Adds a regression test. Sketch results change for samples with mates shorter than k.

## How it was found

Found via [Ponytail](https://github.com/DietrichGebert/ponytail)'s repo audit (`/ponytail-audit`), run with Claude Code over the 2.10.0 code. The audit read `map_read_pair_sketch_into`, saw that `map_read` is skipped for a mate shorter than k, and followed `merge_se_mappings` into piscem-rs to confirm that `map_read` is what clears the cache. This one came from reading the code; the regression test was added with the fix. Tracked in #1283 (finding 5).

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fd36f3b3cfb8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.