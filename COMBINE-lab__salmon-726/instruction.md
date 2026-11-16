# Issue

**Title:** Add split-seq V1 and V2 to alevin

## Description

This PR addresses issue #699. To use the protocol, pass the `--splitseqV2` or `--splitseqV1` flag. To test the implementation correlation analysis was done on [data](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE137941) submitted with the [article](https://www.sciencedirect.com/science/article/pii/S1934590920300552). Thanks @jeremymsimon for pointing to the data. Here are the results of correlation b/w the alevin output and published counts. This test run was done as mentioned in .

![image](https://user-images.githubusercontent.com/12998572/145128352-6efe899a-ea06-49bf-9223-24ad4ba70223.png)

```
> summary(cr)
   Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
 0.2966  0.7128  0.8690  0.8163  0.9448  0.9963 
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e2b92cba8c95`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.