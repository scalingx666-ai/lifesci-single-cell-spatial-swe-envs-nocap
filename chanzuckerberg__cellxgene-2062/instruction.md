# Issue

**Title:** Turn on caching for AnnotationsObs API and Schema API since we don't need recent information from user annotations.

## Description

## Reviewers

**Functional:** @mckinsel 
**Readability:** @MDunitz 

---

## Changes

Modifying the AnnotationsObs API so that subsequent API calls to `obs?` are loaded from disk cache instead of fetching from the database, refreshing on a one week cycle. Also turning on caching for Schema API with similar caching behavior.

Please note that this PR is merging into @mckinsel's branch splitting the backend, instead of merging into `main` directly.

Below is a screenshot of this change deployed to `dev`: I hit the same dataset pbmc3k twice and the second time, made sure to note that it was pulling data from cache.
![Screen Shot 2021-02-13 at 11 38 11 AM](https://user-images.githubusercontent.com/4887796/107862334-0a31f180-6e01-11eb-844b-0d88251b5b7a.png)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `66b872ead08b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.