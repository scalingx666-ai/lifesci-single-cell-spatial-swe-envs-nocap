# Issue

**Title:** Clarified Selecting the representative read documentation

## Description

A user queried the use of quality in which read is kept upon
deduplication (#261)

> your selection procedure does not seem to take into
> account read sequencing quality (only mapping quality).
>
> In other words, if 2 reads have the same high score
> mapping quality (i.e. unique mappers), one being long and
> with good base scores, the other short with errors, it will
> select randomly among these, too, right?

The response was:

> Yes, that's correct.

Updated umi-tools/dedup.py "Selecting the representative read" comment
section to clarify that the read quality is not used.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `617722d1b282`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.