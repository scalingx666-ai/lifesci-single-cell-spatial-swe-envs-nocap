# Issue

**Title:** {ts} add filter umi dedup

## Description

This PR adds options to `extract` and `dedup` to filter the UMIs against a whitelist. This is useful for library preps with non-random UMIs, e.g https://perkinelmer-appliedgenomics.com/library-preparation-kits/illumina-rna-library-prep-kits/nextflex-rapid-directional-qrna-seq-kit/

I'm currently testing out whether it's better to filter UMIs at the extract or dedup stage with the above library prep. My initially inclination was to do the filtering at the dedup stage and let the network handle any error UMIs. However, in the current implementation of this approach, groups where the top read is not in the whitelist are discarded entirely. This will be too conservative for the edge cases where e.g groups with a single UMI which is an error UMI. Since the whitelist UMIs are designed to be more than one error apart, in most cases, it's possible to "correct" the UMIs in `extract`. 

With the current test data set (30 samples), filtering at the `extract` stage yields 1~4% more reads in the final deduplicated BAM compared to filtering at the `dedup` stage. To me, this suggests the edges case indicated above are indeed rare but present and filtering at the extract stage might be preferrable.

I'll leave this PR open until I've finalised the implementations

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `13bbcab4f14f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.