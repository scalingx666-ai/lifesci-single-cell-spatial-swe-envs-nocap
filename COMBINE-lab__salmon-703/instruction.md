# Issue

**Title:** Add inDrop v2 to alevin

## Description

Add [inDropv2 protocol](https://www.nature.com/articles/nprot.2016.154) to salmon alevin. To use this protocol pass the `--indropV2` flag. The details of library preparation can be seen [here](https://teichlab.github.io/scg_lib_structs/methods_html/inDrop.html). R1 is the biological read and R2 is the metadata read. Briefly, the reads have 8-11 bp barcode1, followed by a `W1` sequence which should be specified using `--w1` flag then 8bp barcode2 and 6 bp UMI sequence follows. 

Summary of changes:
1. `--indropV2` flag added to process indropV2 reads
2. a local copy of single cell protocol is created before barcodes and UMI are extracted to allow share the positions and avoid searching twice
3. In case the barcode1 is less than 11bp, `A` is added after joining barcodes 1 and 2 to make the total length 19 bp
4. If no exact match for w1 is found, a search for w1 with a hamming distance <=2 is performed

It was tested for correlation on run SRR7165069 from GEO submission [GSM3141960](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSM3141960).
Results:
![image](https://user-images.githubusercontent.com/12998572/133622734-9b473318-fb39-421d-a322-b018f93ac139.png)


```
  Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
 0.3634  0.8981  0.9655  0.9307  0.9874  0.9976 
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5bdbf3c420dd`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.