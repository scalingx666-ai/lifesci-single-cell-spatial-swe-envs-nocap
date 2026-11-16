# Issue

**Title:** {ts} retain unmapped

## Description

I've merged in the changes from {TS}-DedupPerGene to avoid conflicts later

**Per gene:**
This allows per-gene de-duplication by addition of a 'metafetcher' along the lines suggested by @IanSudbery. Each metacontig is considered in turn and all reads aligned to the contigs are tagged with the metacontig name which becomes the alignment position in reads_dict.

I've done some naive testing by manually modifying a samfile but the code is not currently covered by any testing.

**Output unmapped**
Unmapped reads are now yielded immediately and written out without the tags for corrected UMI and read group identifier. For paired end, if either read is unmapped, both and written out without tags.

I've also slightly modified the yielding of read bundles (umi_methods.py, line 323). Previously, when the contig changed, some reads from the previous contig were retained in the read_dict. This meant some reads were retained in the reads_dict until the very end when read_dict is cleared (line 410).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9ef816341ef4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.