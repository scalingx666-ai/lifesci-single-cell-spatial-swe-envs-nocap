# Issue

**Title:** Expand functionality of plotGene and add new utility functions

## Description

Allow plotGene to plot:
* Values scaled by different groupings based on features in cell.data (in addition to raw, norm values)
* Plots organized by different groupings in cell.data (instead of just by dataset)
* With min and max clips 

Also added more color options to both plotGene and plotFeature.

New functions: 
* reorganizeLiger (set up new liger object with datasets split by other feature in cell.data)
* getProportionMito

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9de1e0962975`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.