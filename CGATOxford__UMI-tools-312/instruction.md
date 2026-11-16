# Issue

**Title:** Deal with chimeric read pairs

## Description

for motivation

- Hardcodes `dedup` to discard chimeric read pairs
- Defaults `group` to discard chimeric reads. These can be output with `--output-chimeric` but will not be grouped. 

The above makes the most sense to me since the `TLEN` of chimeric read pairs is 0. Thus, the current approach in UMI-tools to identify groups of read pairs with the same alignment coordinates will not work for chimeric reads. Therefore these reads are discarded by default but can be output in `group` without any group information. This is the same behaviour as can be switched on for unmapped reads (`--output-unmapped`)

Of course, if we switched to using the actual alignment coordinate of read2 (soft-clipped corrected, or not) to determine the read groups in future, we could then retain chimeric read pairs.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `56830dc77764`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.