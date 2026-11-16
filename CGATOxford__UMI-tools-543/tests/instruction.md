# Issue

**Title:** Speed up writing mates

## Description

.

When `TwoPassPairWriter` reaches the end of a contig, it calls `write_mates`, which reopens that contig from the start and scans through for remaining mates. To do this, `write_mates` uses `pysam.AlignmentFile.fetch(...., multiple_iterators=True)`. As the file uses is the same filehandle being used by `bundle_iterator`, then `multiple_iterators=True` ensures that the position in the file is not lost in this operation. 

`multiple_iterators=True` imposes some overhead. With a reasonable number of contigs this is not a problem, as the overhead is small compared to the cost of the scan. However, when alignment is done to the transcriptome, `write_mates` is called 100s of thousands of times, and for some reason, `fetch` calls the `__init__` of `psyam.RowIteratorRegion` 4 times for each call to `fetch`. This causes a serious slow down, such that adding `--paired` to the commandline slows the processing for an example file down from a couple of minutes to five hours. 

This PR changes `TwoPassPairWriter` so that it's `__init__` opens a second file handle to the input file. This allows it to drop the requirement to use `multiple_iterators=True` and returns the performance to near that of the performance without `--paired`. 

As far as I can tell, this does not change the output (i.e. the two handles act independently). I have tested this both on the test files and on an example transcriptome alignment provided in #539. 

Time to run is reduced from 5 hours to 200 seconds.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0c72fa99c518`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.