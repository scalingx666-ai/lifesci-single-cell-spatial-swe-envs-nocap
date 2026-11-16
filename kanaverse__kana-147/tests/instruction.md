# Issue

**Title:** Integrate with ExperimentHub datasets

## Description

I believe I have most things setup, but running into CORS errors from bioc azure storage 

<img width="1039" alt="image" src="https://user-images.githubusercontent.com/399324/197656841-0137948d-1793-49cd-936f-f1622b90b353.png">

we might need someone at bioc to enable cors headers - we need someone at bioc to add cors headers to the azure storage: https://learn.microsoft.com/en-us/rest/api/storageservices/cross-origin-resource-sharing--cors--support-for-the-azure-storage-services

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e7d75658eaf5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.