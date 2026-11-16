# Issue

**Title:** Feat marker genes

## Description

This is an addition that my lab wanted because we wanted to be able to BLAST genes from our bins that were identified as marker genes.

It looks similar to what I think issue #22 is requesting. With that in mind, I thought I'd upload my code. Feel free pull it into the main branch if this is what you had in mind. It would be possible to sort the genes by contig and position on contig to have an ordered FASTA of marker genes. This isn't currently done for speed reasons but it could be a good complement to a graphic of the dispersion of marker genes across the contigs. My lab also has interest in knowing how evenly dispersed the markers are over the genome bin (to ensure we haven't just happened to assemble a region that is dense in markers which makes it look more complete than it actually is). So, I may work on making a dispersion graphic at some time in the future.

Commit 8ee5f90 message describes the addition in more detail.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `dd248111b975`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.