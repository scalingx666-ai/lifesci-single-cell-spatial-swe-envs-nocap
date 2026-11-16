# Issue

**Title:** Feat: Feature gene annotation

## Description

I have written some code that will produce a per gene CNV matrix, giving the mean log2 CNV per gene (as 1 gene can appear in many windows) 
I have also updated the `np.convolve` mode to `valid` so it matches the documentation in the function. Full methods [here](https://numpy.org/doc/stable/reference/generated/numpy.convolve.html)

I have also updated the code in the instance where the window is larger than the number of genes on the chromosome, to only run one convolution the length of the genes on the given chr see https://github.com/grantn5/infercnvpy/blob/feature_geneAnnotation/src/infercnvpy/tl/_infercnv.py#L198

I have also updated the `genomic_position_from_gtf` function so it will always read the gtf in as a pandas df (avoids bug where it reads it in as polars df) 

```
gtf = gtfparse.read_gtf(
        gtf_file, usecols=["seqname", "feature", "start", "end", "gene_id", "gene_name"], result_type="pandas"
    )
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ad98e5834340`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.