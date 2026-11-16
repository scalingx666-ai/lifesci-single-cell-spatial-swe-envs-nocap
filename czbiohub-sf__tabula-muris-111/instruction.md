# Issue

**Title:** Heart_FACS

## Description

All clusters have been reannotated. However, cluster 11 is a a new cluster only showing up this time. After gene ontology analysis of the uniquely expressed genes in this cluster, those cells seem to be neuron cells (maybe conduction cells), but they do not express the commonly used cardiac conduction cell marker genes, so I have annotated them as NA.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a29b6c82999b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.