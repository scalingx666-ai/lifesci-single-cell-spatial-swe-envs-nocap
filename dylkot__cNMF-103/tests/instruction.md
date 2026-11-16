# Issue

**Title:** Change sc.pp.normalize_per_cell() to sc.pp.normalize_total() in prepocess.py

## Description

Hi! 

Thanks for the fantastic tool, it keeps on giving.

This change has already been applied elsewhere to avoid conflicts with the deprecated sc.pp.normalize_per_cell() function () , so I took the liberty to apply it to the preprocess.py module. In my setting, I made this change in a monkey-patched version of the preprocess_for_cnmf() and normalize_batchcorrect() functions with the conda install of cNMF (cnmf, 1.6.0, pyhdfd78af_0, bioconda). 

This is my first time attempting to contribute to a project I am not involved in myself, so please let me know if there are some issues with anything related to the code, testing or etiquette on my end. 

Cheers,
Rob

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `48c5cdf31dfa`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.