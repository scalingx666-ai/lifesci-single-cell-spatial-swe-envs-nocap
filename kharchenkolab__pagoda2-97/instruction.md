# Issue

**Title:** Add biocViews in DESCRIPTION

## Description

* adds `biocViews:` within the `DESCRIPTION`, which is used by devtools to install bioconductor packages
* removes the `bioc::release/*` packages in Remotes, i.e.

```
bioc::release/AnnotationDbi,
bioc::release/BiocGenerics,
bioc::release/org.Dr.eg.db,
bioc::release/org.Hs.eg.db,
bioc::release/org.Mm.eg.db,
bioc::release/pcaMethods,
```

My understanding is that `bioc::` is meant to download the development versions from Bioconductor (which exists in the master branch). I think this was changed to `bioc::release`, but `biocViews` should take care of this, I think.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0250af90d21f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.