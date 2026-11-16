# Issue

**Title:** scale by log10(exp(1)) for log10 plots

## Description

Attempt to address the following issue: 

I started looking into the units...and it's true that the plot is currently plotting in natural log scale, not log10(). 

This PR scales the plot values such that `adjustVariance` plots in log10. Note calculations for over-dispersed genes, etc. are still log()-based. 

That is, I don't touch this

```
ods <- order(df$v,decreasing=TRUE); if(length(ods)>1e3) { ods <- ods[1:1e3] }
...
if(use.unadjusted.pvals) {
    ods <- which(df$lp<log(alpha))     ## pf() from stats (the F-distribution)  uses log()
} else {
    ods <- which(df$lpa<log(alpha))   ## df$lpa is based on log()-based BH adjustments, bh.adjust()
 }
```
or this
```
vi <- which(is.finite(df$v) & df$nobs>=min.gene.cells);
```

I'm simply making sure that what was plotted previously is now log10-scaled. 

The resulting plot from the [walkthrough](https://github.com/kharchenkolab/pagoda2/blob/master/vignettes/pagoda2.walkthrough.oct2018.md) looks like the following:

<img width="1440" alt="log10_plot" src="https://user-images.githubusercontent.com/6968193/90321318-8319c480-df16-11ea-82ad-89429b69df96.png">

where it previously was the following:
<img width="708" alt="original" src="https://user-images.githubusercontent.com/6968193/90321344-bc523480-df16-11ea-8868-4a95dc2824c9.png">

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cadfb666852a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.