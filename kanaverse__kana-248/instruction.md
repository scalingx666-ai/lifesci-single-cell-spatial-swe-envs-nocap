# Issue

**Title:** Correctly pass options to the bakana result readers.

## Description

This can either be done as I've shown, or it can be done by modifying the `useEffect` on **each** card to avoid an unnecessary nesting of options - for example, in the SE result reader:

https://github.com/kanaverse/kana/blob/e6764a7a607f3e2c4b226cd1d59631f77ef22261/src/components/LoadExplore/SECard.js#L65-L67

There is only ever one dataset, so there's no point doing this nesting.

This provides a user-level fix to #246, rather than requiring removal of the offending data from the file.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e6764a7a607f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.