# Issue

**Title:** crs-imputation

## Description

Initialize `crs-imputation` (Issue: #136)

* Integration between Janesick 10x scRNA and Xenium using `harmony`
* transfer gene expression from scRNA to Xenium using kNN of harmony embedding.

TODO: 

- [x] adapt to `OSTA.data`
- [x] review processing of data prior to `harmony`
- [x] move chapter to `crs`
- [x] visualize a gene from scRNA that is missing in Xenium, and compare with a similar marker available in Xenium 
- [x] review text
- [x] provide references if necessary

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7913ba25be78`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.