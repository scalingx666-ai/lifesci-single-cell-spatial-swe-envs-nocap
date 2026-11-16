# Issue

**Title:** feat: return two lists for diffexp

## Description

#### Reviewers
**Functional:** 
@maniarathi 
**Readability:** 
@seve 
---

## Changes
- modify DiffExpObsAPI "/diffexp/obs" -- when two_lists=True is passed as part of the request body, return two separate lists for the diffexp results. If two_lists is not passed in as an arg the endpoint will return a single list of diffexp values (current functionality)
currently the endpoint returns  
for top N genes, [ varindex, logfoldchange, pval, pval_adj ] 

if two_lists is True the endpoint returns 
{"positive": for top N genes, [ varindex, logfoldchange, pval, pval_adj ], 
"negative": for top N genes, [ varindex, logfoldchange, pval, pval_adj ]}

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6f6634a4d976`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.