# Issue

**Title:** Do not cache read for mate output if mate is unmapped.

## Description

pysam.AlignedSegment.next_reference_name throws ValueError if the mate is unmapped.

If `group` is run with `--output-unmapped` then if read1 is mapped, but read2 is not, TwoPassWriter throws an error because of this. 

This fix skips trying to store the mate details for delayed outputting if the mate is unmapped. In this case the mate is output independently anyway.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `949b7c15224e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.