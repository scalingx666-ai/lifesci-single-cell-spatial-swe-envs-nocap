# Issue

**Title:** perf(quant): stream --writeUnmappedNames instead of accumulating it

## Description

Addresses the `--writeUnmappedNames` item in #1091. (Leaving #1091 open — the other items are being triaged separately.)

### Problem

The names of unmapped fragments accumulated in a per-worker `Vec<String>`, were merged into a shared `Vec<String>` at thread end, and were written out only after the whole mapping pass finished. That is one heap `String` per unmapped read, all retained until the process exited, with **no bound** — memory grows with however many reads fail to map, which on a contaminated sample is most of them.

### Change

Workers append `"<name> u"` lines into a per-thread `String` and hand the block to a shared writer at each batch boundary — exactly the idiom `sam_buf` already uses. An unmapped read no longer allocates at all, the lock is taken once per batch instead of once per read, and no name outlives the batch that produced it.

The file is also opened up front rather than at the end, so an unwritable output directory is reported before the mapping pass instead of after it.

### Measured

10M human fragments against a small transcriptome index, so nearly everything is unmapped (9,999,972 names):

| | peak RSS |
| --- | ---: |
| develop | 1620 MB |
| this PR | **159 MB** |

Same name set in both.

### Output unchanged

- `-p 1`: `unmapped_names.txt` **byte-identical** to develop
- `-p 16`: identical sorted name set, which also equals the `-p 1` set

Line order within the file is thread-interleaved both before and after this change — it was never deterministic across threads, and this does not make it less so.

### Test

There were no tests for this flag. The new one mixes simulated transcriptome reads with foreign reads so the expected unmapped set is known exactly, asserts the file lists precisely those fragments, and checks the file ends with a newline so a truncated flush cannot pass as a complete file.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6243fcfc7451`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.