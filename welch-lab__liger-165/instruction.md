# Issue

**Title:** Enhancements for plotGene and plotGenes and plotByDatasetAndCluster

## Description

Hi Welch & Macosko Labs,

I'm still new to putting in PR for packages so please let me know if there is anything else I need to do or change to make this work.

I've made two changes to plotting code:
`plotGene()` now has an additional call in the function for TRUE/FALSE that I call `keep.scale`.  Setting `keep.scale = TRUE` extracts the min & max expression values across all datasets and then uses those values to set the color scale identically between all datasets instead of the local min/max per dataset (see attached image).  This is especially helpful when comparing level of expression across datasets and not just within a single dataset.
I set the default value to be `keep.scale = F` within the PR though I leave that up to you all as to what you want for the package and could easily be set to TRUE by default as well.

The other change I made was to `plotGenes()` by adding a `...` to the function to allow it to call aspects of `plotGene()`.  I did this to allow for specifying keep.scale when plotting multiple genes though I realize the ability to specify anything from plotGene to plotGenes may not 100% work (for example, I tried `return.plots = T` in new plotGenes and it doesn't work but specifying new color scheme with `cols.use` works just fine).  If you prefer can simply just add the `keep.scale` call to `plotGenes` as below though I do think that the ... functionality for specifying other parameters is handy.
```
plotGenes <- function(object, genes, keep.scale = F) {
  for (i in 1:length(genes)) {
    print(genes[i])
    plotGene(object, genes[i], keep.scale = keep.scale)
  }
}
```

I also edited the ```#` @param``` for both functions though did not roxygenize those changes.

Please let me know if there is anything else you need to make this PR work if there are any issue.

Thanks!
Sam

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8d9503e06938`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.