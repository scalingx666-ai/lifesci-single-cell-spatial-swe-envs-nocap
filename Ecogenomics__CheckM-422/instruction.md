# Issue

**Title:** fix(1.2.7): crash in BinStatistics.sequenceStats when no called genes are available

## Description

Bumps the version to 1.2.7.

## Bug
`BinStatistics.sequenceStats()` has a branch for when no `genes.faa` file exists, for example when the user supplied genes that were already called. That branch referenced `gene` before it was assigned, so it raised `UnboundLocalError`. It also only updated the last sequence in the bin.

## Fix
When no called genes are available, `# ORFs` and `Coding bases` are now set to 0 for every sequence, as the existing comment intended.

Nothing in CheckM currently calls `sequenceStats()`; its only consumer was the commented-out output format 10 code in `resultsParser.py`. No current command is affected, but the method no longer crashes if it is used again.

## Testing
- Added `testSequenceStatsWithGenes` and `testSequenceStatsWithoutGenes` to `checkm/test/test_binStatistics.py`.
- On `master`, `testSequenceStatsWithoutGenes` fails with `UnboundLocalError: local variable 'gene' referenced before assignment`.
- With this fix, all 26 unit tests pass on Python 3.6 and 3.11.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `81d94cc601ce`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.