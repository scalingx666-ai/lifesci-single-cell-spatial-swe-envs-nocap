# Issue

**Title:** Add sci-rna-seq3 protocol to salmon

## Description

Add [sci-rna-seq3 protocol](https://www.nature.com/articles/s41586-019-0969-x) to salmon alevin. To use this protocol pass the `--sciseq3` flag. The details of library preparation can be seen [here](https://teichlab.github.io/scg_lib_structs/methods_html/sci-RNA-seq3.html). Briefly, the reads have 9-10 bp hairpin adaptor index, and 10bp reverse transcription index which together make the cell barcode of 19-20 bp in length; an 8 bp UMI which follows a 6bp anchor sequence CAGAGC. 

Summary of changes:
1. `--sciseq3` flag added to process sci-rna-seq3 reads
2. a local copy of single cell protocol is created before barcodes and UMI are extracted to allow share the position of anchor sequence and avoid searching twice
3. In case the barcode is 19bp, `A` is added as the last nucleotide to make the cell barcodes length 20 bp for all barcodes

It was tested on data from the [Nature paper](https://www.nature.com/articles/s41586-019-0969-x). Correlation b/w the counts from the GEO submission [GSE119945](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE119945) and sum of spliced, unspliced reads with and without ambiguous counts using `usa` mode in alevin-fry gave reasonable looking correlations. 
Results for one of the fastq files:
![image](https://user-images.githubusercontent.com/12998572/128923136-eefa8738-f87e-4f67-bba6-5cc1648ce194.png)

```
   Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
 0.4594  0.7805  0.8295  0.8253  0.8736  0.9943 
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `91129761d57c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.