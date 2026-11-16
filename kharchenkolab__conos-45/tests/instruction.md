# Issue

**Title:** Better scanpy integration

## Description

## Better integration between conos and ScanPy
### The main additions
The main point of this PR is adding more functionality to the `saveConosForScanPy` function. I added the options to:
- save the normalised matrix of counts
- save the 2D embedding used for plotting in conos
- save a normal (not pseudo) PCA - done with the pca function I added in previous PR

Additionally, I made that saving particular elements is optional and controlled with parameters by the user. So by default, the function will save only the raw count matrix, the list of genes and the list of cells. 
### Tutorial changes
Finally, I have updated the two ScanPy integration tutorials to show the full potential of the updated function. I remade the jupyter notebook for the ScanPy part. With the new options in the updated function we can now visualise the not only the (pseudo)PCA, but also the same conos embedding (allows for having consistent style of plots if someone decides to have PAGA plots). I also added how to draw a graph based on the PAGA plot that shows all the connections calculated by conos. I think many people may be interested in that. 

## Other changes

Apart from all above, this PR includes a number of small fixes and style changes. Most notably, I added an option to the `velocityInfoConos` to choose clustering (or supply custom one). Before I was assuming leiden clustering, which is not consistent with the rest of the package and how people use the tool. 

I also implemented the usage of `getJoinCountMatrix` across the package. I saw it being added in one of the latest commits to simplify extracting and merging sample count matrices.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b9ce17bc8d80`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.