# Issue

**Title:** Fixes issue #15 (I believe)

## Description

I modified `enrichIt` so that it uses a simple list of gene sets rather than worrying about GSEA/GSEABase dependencies. This was based on an old error (and its solution) described here: <https://support.bioconductor.org/p/42073/>

This way, users can also easily construct their own customized lists of gene sets without having to go the GeneSetCollection route. 

Also added some details to the vignette to clarify the different handling of Seurat and SCE objects.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `847a734618a6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.