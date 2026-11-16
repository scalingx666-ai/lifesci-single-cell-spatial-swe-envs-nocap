# Issue

**Title:** fix: clarify Dataset YAML primary library errors

## Description

## Summary
- Report the supported primary read types and the library types found when a Dataset YAML has no primary reads.
- For `pacbio`-only datasets, explain that PacBio CCS reads should use `single`, while `pacbio` is for supplementary CLR reads.
- Add a parser regression using an empty synthetic FASTQ placeholder and YAML metadata only.

.

## Validation
- `py -3.9 -S -B src/projects/spades/pipeline/spades_pipeline/tests/test_error_codes.py` (32 tests passed)
- Parser-only synthetic reproduction returned the improved diagnostic and exit code 67 before any assembler stage.

No build or assembly was run; neither is needed or authorized for this diagnostic change.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e617eb81d766`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.