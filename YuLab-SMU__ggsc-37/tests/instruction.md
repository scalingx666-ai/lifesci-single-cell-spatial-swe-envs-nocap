# Issue

**Title:** fix the function of features parameter

## Description

In the former function, adding values to features can not show the specific item. Instead function will show all result.
```
p <- plot_lisa_feature(spe = SVP::gsvaExp(spe1,'LISA'),
                                      lisa.res = lisa,
                                      features ="CD6 T cells",
                                      assay.type='Gi',
                                      geom = geom_bg,
                                      pointsize=1,
                                      common.legend = TRUE,
                                      ncol = 4)
```
This pr is to fix this bug, after fixing, function will return specific result of feature.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7672f8ccd7e0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.