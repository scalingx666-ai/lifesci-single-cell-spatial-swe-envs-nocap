# Issue

**Title:** Use of read.tags += was causing a change of type for some tags. Now i…

## Description

fix for #285 

Use of `read.tags += [(tag, value)]` was cuasing a change in the type for some tags. Specifically if an application had set the read group tag (`RG`), using a `Z` type, after passing through `group` the type of the RG tag would be `A`. 

The samtools specification requires that the RG tag has the type `Z`, and so bam validation tools were failing. 

I belive this is happening becausae when

 `read.tags += [(tag, value)]`

`(tag,value)` pairs are being extracted from the `tags` attribute, a new list of `(tag, value)` pairs is being created, and this is being passed back to the read. In this process a guess is being made as to the type. 

Now uses `read.set_tag(tag, value)`, which doesn't have this problem.

Note that this doesn't apply to all versions of pysam. This problem is present in 0.11 and 0.12, but not in 0.15

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `46abe3aa36b8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.