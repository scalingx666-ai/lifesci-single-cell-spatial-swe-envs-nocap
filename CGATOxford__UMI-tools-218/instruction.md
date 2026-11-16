# Issue

**Title:** {ts} add retain umi option

## Description

@IanSudbery  - This branch introduces an experimental option `--retain-umi` in `extract` to retain the umi in the read sequence. 

I used this for some (slightly unusual) samples where ~2/3 of reads contain a 1-9bp sequence of non-template nucleotides which are added to the 5' end of the read prior to amplification. This is not by design! However, the benefit is that the first 9bp can be used as a pseudo-umi but the length and presence of the non-tempate nucleotides is not consistent so I also need to retain the pseudo-umi in the read sequence and allow the aligner to soft-clip where appropriate. The other option would have been to extract the soft-clipped bases from the BAM and annotate the BAM with these. However, this wouldn't have worked with `umi_tools dedup` due to the need for a uniform UMI length.

Since this option is very bespoke, I've hidden the option from users.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `62ed3a3870c2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.