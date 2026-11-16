# Issue

**Title:** Fix: Allow Prodigal option '-p meta' by not exiting on first failure

## Description

### Description

CheckM/1.2.3 fails silently on a genome with error : ERROR: prodigal exited with code: 13312. Upon inspection, it appears that when a genome has a large number of N's and size > 100000, the error handling in the script prodigal.py causes the failure and exit before reaching the 2nd attempt with the option `-p meta` that usually takes care of this issue. 

#### Analysis of the error
**<output_dir>/checkm.log** 
```
INFO: CheckM v1.2.3
INFO: checkm lineage_wf -t 5 -x fna <input_dir> <output_dir>
INFO: CheckM data: /env/ig/biobank/by-soft/checkm/1.2.3
INFO: [CheckM - tree] Placing bins in reference genome tree.
INFO: Identifying marker genes in 1 bins with 10 threads:
ERROR: prodigal exited with code: 13312
INFO: Saving HMM info to file.
INFO: Calculating genome statistics for 1 bins with 10 threads:
INFO: Extracting marker genes to align.
ERROR: Models must be parsed before identifying HMM hits.
```
When running the exact same command line for prodigal from checkm' scripts : 
```
prodigal -p single -q -m -f gff -g 4 -a test.faa -i error_generating_genome.fna > test.gff 1> prodigal.out 2> prodigal.err
```
the following error in .err file is returned `Error: saw too many regions of 'N''s in the sequence.` However, when changing the option  `-p single` to `-p meta` prodigal exit successfully. In the checkm/prodigal.py script this was supposed to be taken care of by running the option `-p meta` if first attempt fails. However the error handling makes the code exit before reaching the alternative option. 

#### Modification of error handling in script checkm/prodigal.py

The suggested modification in the script checkm/prodigal.py takes into account that prodigal might fail on first attempt for genomes with large number of N's and size > 100000. In that case, prodigal is ran again with option `-p meta`. If, however, an error is still returned, the code exits with an error. 

After correction, here is an example of the resulting warning message in output file <output_dir>/checkm.log (the warning message appears twice maybe because of multithreading) : 
```
WARNING: Prodigal failed or returned no output (code: 13312). Retrying with '-p meta' due to possible high N content in the genome.
WARNING: Prodigal failed or returned no output (code: 13312). Retrying with '-p meta' due to possible high N content in the genome.
```

#### Validation

The modified checkm was tested on several microbial genomes including the genome that made the error arise in the first place with success.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `455f9cefcc10`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.