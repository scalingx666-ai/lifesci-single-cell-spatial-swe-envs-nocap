# Issue

**Title:** fix: s3 user annotations

## Description

#2540 

#### Reviewers
**Functional:** 
@ebezzi
 
**Readability:** 

---

## Changes
- do _not_ attempt to create the user annotations directory if an s3 location is specified.

## QA
```
cellxgene launch --user-generated-data-dir s3://atolopko-tmp/cellxgene_desktop  ...

❯ aws s3 ls s3://atolopko-tmp/cellxgene_desktop/
                           PRE x-gene-sets-FXQEAGSB-backups/
2022-07-26 08:47:15        266 x-gene-sets-FXQEAGSB.csv
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `69a6d52240d9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.