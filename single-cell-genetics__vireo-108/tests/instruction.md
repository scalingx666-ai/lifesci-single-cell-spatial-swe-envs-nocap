# Issue

**Title:** Check if cell data has any variant and check if cell data variants ha…

## Description

…ve any overlap with donor VCF file.

Check if cell data has any variant and check if cell data variants have any overlap with donor VCF file.

Examples:

  - Running vireo with a cellSNP directory that does not have any variant (as provided CBs for cellSNP-lite did not overlap with any variants).

    [vireo] Loading cell folder ... Error: cell data in vcf file, or cellSNP output folder, or vartrix's alt.mtx,ref.mtx,barcodes.tsv does not contain any variants.

  - Running vireo with a VCF file that does not overlap at all with the SNPs used in cellSNP-lite.

    cellSNP-lite [vireo] Loading cell folder ... [vireo] Loading donor VCF file ... /conda/envs/cellsnp/lib/python3.11/site-packages/numpy/core/fromnumeric.py:3504: RuntimeWarning: Mean of empty slice. return _methods._mean(a, axis=axis, dtype=dtype, /conda/envs/cellsnp/lib/python3.11/site-packages/numpy/core/_methods.py:129: RuntimeWarning: invalid value encountered in scalar divide ret = ret.dtype.type(ret / rcount) [vireo] warning: no variants matched to donor VCF, please check chr format! Error: No matching variants found between cell data and donor VCF.

Before:

    [vireo] Loading cell folder ... [vireo] Loading donor VCF file ... /conda/envs/cellsnp/lib/python3.11/site-packages/numpy/core/fromnumeric.py:3504: RuntimeWarning: Mean of empty slice. return _methods._mean(a, axis=axis, dtype=dtype, /conda/envs/cellsnp/lib/python3.11/site-packages/numpy/core/_methods.py:129: RuntimeWarning: invalid value encountered in scalar divide ret = ret.dtype.type(ret / rcount) [vireo] warning: no variants matched to donor VCF, please check chr format! Traceback (most recent call last): File "/conda/envs/cellsnp/bin/vireo", line 8, in <module> sys.exit(main()) ^^^^^^ File "/conda/envs/cellsnp/lib/python3.11/site-packages/vireoSNP/vireo.py", line 168, in main donor_GPb = parse_donor_GPb(donor_vcf['GenoINFO'][options.geno_tag], ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^ File "/conda/envs/cellsnp/lib/python3.11/site-packages/vireoSNP/utils/vcf_utils.py", line 328, in parse_donor_GPb GT_prob = np.zeros((len(GT_dat), len(GT_dat[0]), 3)) ~~~~~~^^^ IndexError: list index out of range

    The traceback obscures the warning message.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `97971e37a7bb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.