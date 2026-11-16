# Issue

**Title:** [r][cpp] add normalizations and tile widths to `write_insertion_bedgraph()`

## Description

Kind of unrelated to anything we previously discussed.  
I found a few scenarios where I needed to get bedgraphs/bigwigs that were normalized by pseudobulk.  There was no easy way of doing this from an IterableFragments object.  
I also noticed that I didn't always need full base pair resolution, and could get away with large tiles for bedgraphs, hence the added ability to convolve by tile width.  
Fundamentally, this can probably replace `write_insertion_bedgraph()` just by setting tile_width to 1.  


## Concerns:
I'm not sure if I should have the last variable tile, since we need to clip by the end of chromosome.  This is the only tile that has a different tile width.  We can probably change this behaviour if there's a suitable alternative.

## Performance:
Follows `writeInsertionBedgraph` pretty much to a tee.  I tried to make it so we had as little of branching as possible for normalization.  Just did this via a lambda, but I don't think the core fragment logic will be the bottleneck.  Most likely it is the gzprintf statements.  I think batch writing and doing the string logic altogether would give a sizable improvement in the future. 

## Future Work:
From what I see, bedgraphs are normally just used as an intermediary before converting into a bigwig.  Problem is that creating the bigwigs is probably non-trivial.  This is because we either need to use the [bedgraphtobigwig:](https://www.encodeproject.org/software/bedgraphtobigwig/), or rtracklayer.  bedgraphtobigwig introduces a lot of bioconductor dependencies, while rtracklayer introduces memory constraints.  Writing the bigwigs ourselves is also probably non-trivial.  I'll leave it here as a discussion, but I don't have a good answer for this just yet.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b7272b713b2b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.