# Issue

**Title:** implement palantir.plot.plot_stats

## Description

@ManuSetty This implements `palantir.plot.plot_stats` which is a more general version of `palantir.plot.plot_branch`. It works very similarly but allows to plot other stats than just pseudo time on the y-axis. Optionally, it allows to subset to a specific branch just like the `palantir.plot.plot_branch` does. Here is an example where we plot the Mellon log-density over the MAGIC imputed EBF1 expression, color by cell type and subsetted to the B-cell branch:
![image](https://github.com/dpeerlab/Palantir/assets/4857068/59793cb4-26aa-48d5-bee1-86c158c8811d)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cf196adaa1bd`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.