# Issue

**Title:** Add LFF_ERC_spatial data to fetch_data()

## Description

Add 8 files from ERC project to fetch data:

1.  LFF_spatial_ERC_SRT. 
2. LFF_spatial_ERC_SRT_pseudobulk
3. LFF_spatial_ERC_SRT_modeling_results
4. LFF_spatial_ERC_snRNAseq
5. LFF_spatial_ERC_snRNAseq_pseudobulk_broad
6. LFF_spatial_ERC_snRNAseq_pseudobulk_subcluster
7. LFF_spatial_ERC_snRNAseq_modeling_results_broad
8. LFF_spatial_ERC_snRNAseq_modeling_results_subcluster

Paths to data in ERC are listed [here](https://github.com/LieberInstitute/LFF_spatial_ERC/blob/devel/processed-data/00_project_prep/spatialLIBD_ERC_data_paths.csv)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `20d2ef8c6129`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.