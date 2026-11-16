# Issue

**Title:** fix(singler): pass task cpus to SingleR num.threads

## Description

## Description

This PR fixes `CELLTYPES_SINGLER` to use the CPUs allocated by Nextflow, and full set of minimal tests now runs twice as faster! (58 -> 29 minutes on the same specs 10 CPU / 20 Gb RAM)

The module is currently labeled `process_medium`, but `SingleR()` was called without setting `num.threads`, so classification still ran single-threaded. This change derives the thread count from `task.cpus` in the `singleR.R` template and passes it to `SingleR(num.threads = ...)`.

(cherry picked from commit e8f0fa699f03466cc33f9ab6b45e1dd51f38c58e)


## PR checklist

- [x] This comment contains a description of changes (with reason).
- [ ] If you've fixed a bug or added code that should be tested, add tests! _(not applicable?)_
- [ ] If you've added a new tool - have you followed the pipeline conventions in the [contribution docs](https://github.com/nf-core/scdownstream/tree/master/.github/CONTRIBUTING.md)
- [x] If necessary, also make a PR on the nf-core/scdownstream _branch_ on the [nf-core/test-datasets](https://github.com/nf-core/test-datasets) repository.
- [ ] Make sure your code lints (`nf-core pipelines lint`).
- [ ] Ensure the test suite passes (`nextflow run . -profile test,docker --outdir <OUTDIR>`).
- [ ] Check for unexpected warnings in debug mode (`nextflow run . -profile debug,test,docker --outdir <OUTDIR>`).
- [ ] Usage Documentation in `docs/usage.md` is updated.
- [ ] Output Documentation in `docs/output.md` is updated.
- [ ] `CHANGELOG.md` is updated.
- [ ] `README.md` is updated (including new tool citations and authors/contributors).


## Testing


```
$ nextflow run main.nf -profile test,docker --outdir results_test -with-report  

 N E X T F L O W   ~  version 25.10.4

Launching `main.nf` [reverent_goldberg] DSL2 - revision: 9ccdf157fe


------------------------------------------------------
                                        ,--./,-.
        ___     __   __   __   ___     /,-._.--~'
  |\ | |__  __ /  ` /  \ |__) |__         }  {
  | \| |       \__, \__/ |  \ |___     \`-._,-`-,
                                        `._,._,'
  nf-core/scdownstream 0.0.1dev
------------------------------------------------------

Input/output options
  input                     : https://raw.githubusercontent.com/nf-core/test-datasets/3ba0ba7174a5667fc2e005430594ffb063f986c7/samplesheet.csv
  outdir                    : results_test

Quality control options
  doublet_detection         : solo,scrublet,scds

Integration options
  integration_methods       : scvi,harmony,bbknn,combat
  integration_hvgs          : 500

Tool options
  celltypist_model          : Adult_Human_Skin
  celldex_reference         : https://raw.githubusercontent.com/nf-core/test-datasets/scdownstream/singleR/references.csv

scVI/scANVI options
  scvi_max_epochs           : 2

Institutional config options
  config_profile_name       : Test profile
  config_profile_description: Minimal test dataset to check pipeline function

Generic options
  trace_report_suffix       : 2026-03-12_11-35-35

Core Nextflow options
  runName                   : reverent_goldberg
  containerEngine           : docker
  launchDir                 : /home/kim/singler_fix/scdownstream
  workDir                   : /home/kim/singler_fix/scdownstream/work
  projectDir                : /home/kim/singler_fix/scdownstream
  userName                  : kim
  profile                   : test,docker
  configFiles               : /home/kim/singler_fix/scdownstream/nextflow.config

!! Only displaying parameters that differ from the pipeline defaults !!
------------------------------------------------------

* The nf-core framework
    https://doi.org/10.1038/s41587-020-0439-x

* Software dependencies
    https://github.com/nf-core/scdownstream/blob/master/CITATIONS.md

executor >  local (210)
[-        ] NFCORE_SCDOWNSTREAM:SCDOWNSTREAM:LOAD_H5AD:SCANPY_READH5                                                   -
[15/2723fa] NFCORE_SCDOWNSTREAM:SCDOWNSTREAM:LOAD_H5AD:ADATA_READRDS (SRR28679758)                                     [100%] 4 of 4 ✔
[-        ] NFCORE_SCDOWNSTREAM:SCDOWNSTREAM:LOAD_H5AD:ADATA_READCSV                                                   -
[68/724053] NFCORE_SCDOWNSTREAM:SCDOWNSTREAM:QUALITY_CONTROL:GET_UNFILTERED_SIZE (SRR28679758)                         [100%] 3 of 3 ✔
[-        ] NFCORE_SCDOWNSTREAM:SCDOWNSTREAM:QUALITY_CONTROL:EMPTY_DROPLET_REMOVAL:CELLBENDER_REMOVEBACKGROUND         -
[-        ] NFCORE_SCDOWNSTREAM:SCDOWNSTREAM:QUALITY_CONTROL:EMPTY_DROPLET_REMOVAL:ANNDATA_BARCODES                    -
[97/ad2583] NFCORE_SCDOWNSTREAM:SCDOWNSTREAM:QUALITY_CONTROL:GET_FILTERED_SIZE (SRR28679758)                           [100%] 3 of 3 ✔
[76/7b96da] NFCORE_SCDOWNSTREAM:SCDOWNSTREAM:QUALITY_CONTROL:QC_RAW (SRR28679758)                                      [100%] 3 of 3 ✔
[8a/ad4e98] NFCORE_SCDOWNSTREAM:SCDOWNSTREAM:QUALITY_CONTROL:AMBIENT_CORRECTION:CELDA_DECONTX (SRR28679758)            [100%] 3 of 3 ✔
[-        ] NFCORE_SCDOWNSTREAM:SCDOWNSTREAM:QUALITY_CONTROL:UNIFY:MYGENE                                              -
[91/4c31c7] NFCORE_SCDOWNSTREAM:SCDOWNSTREAM:QUALITY_CONTROL:UNIFY:ADATA_UNIFY (SRR28679758)                           [100%] 3 of 3 ✔
[8a/980b00] NFCORE_SCDOWNSTREAM:SCDOWNSTREAM:QUALITY_CONTROL:UNIFY:UPSET_GENES (upset)                                 [100%] 1 of 1 ✔
[b1/422f9c] NFCORE_SCDOWNSTREAM:SCDOWNSTREAM:QUALITY_CONTROL:SCANPY_FILTER (SRR28679758)                               [100%] 3 of 3 ✔
[a9/9cf7d4] NFCORE_SCDOWNSTREAM:SCDOWNSTREAM:QUALITY_CONTROL:GET_THRESHOLDED_SIZE (SRR28679758)                        [100%] 3 of 3 ✔
[2a/1324be] NFCORE_SCDOWNSTREAM:SCDOWNSTREAM:QUALITY_CONTROL:DOUBLET_DETECTION:SCDS (SRR28679758)                      [100%] 3 of 3 ✔
[25/4806bf] NFCORE_SCDOWNSTREAM:SCDOWNSTREAM:QUALITY_CONTROL:DOUBLET_DETECTION:SCVITOOLS_SOLO (SRR28679758)            [100%] 3 of 3 ✔
[ba/717d9f] NFCORE_SCDOWNSTREAM:SCDOWNSTREAM:QUALITY_CONTROL:DOUBLET_DETECTION:SCANPY_SCRUBLET (SRR28679758)           [100%] 3 of 3 ✔
[e1/0fc44b] NFCORE_SCDOWNSTREAM:SCDOWNSTREAM:QUALITY_CONTROL:DOUBLET_DETECTION:DOUBLET_REMOVAL (SRR28679758)           [100%] 3 of 3 ✔
[9c/9c9dac] NFCORE_SCDOWNSTREAM:SCDOWNSTREAM:QUALITY_CONTROL:GET_DEDOUBLETED_SIZE (SRR28679758)                        [100%] 3 of 3 ✔
[e0/3ea898] NFCORE_SCDOWNSTREAM:SCDOWNSTREAM:QUALITY_CONTROL:QC_FILTERED (SRR28679758)                                 [100%] 3 of 3 ✔
[58/26b5b8] NFCORE_SCDOWNSTREAM:SCDOWNSTREAM:QUALITY_CONTROL:COLLECT_SIZES (sizes)                                     [100%] 1 of 1 ✔
[42/2174a5] NFCORE_SCDOWNSTREAM:SCDOWNSTREAM:CELLTYPE_ASSIGNMENT:SINGLER:CELLDEX_FETCHREFERENCE (hpca_celldex)         [100%] 2 of 2 ✔
[e5/0209fa] NFCORE_SCDOWNSTREAM:SCDOWNSTREAM:CELLTYPE_ASSIGNMENT:SINGLER:CELLTYPES_SINGLER (SRR28679756)               [100%] 3 of 3 ✔
[a6/5bfd0d] NFCORE_SCDOWNSTREAM:SCDOWNSTREAM:CELLTYPE_ASSIGNMENT:CELLTYPES_CELLTYPIST (SRR28679758)                    [100%] 3 of 3 ✔
[2a/f18ffb] NFCORE_SCDOWNSTREAM:SCDOWNSTREAM:FINALIZE_QC_ANNDATAS (SRR28679756)                                        [100%] 3 of 3 ✔
[47/3a041e] NFCORE_SCDOWNSTREAM:SCDOWNSTREAM:COMBINE:ADATA_MERGE (merged)                                              [100%] 1 of 1 ✔
[32/6e6bef] NFCORE_SCDOWNSTREAM:SCDOWNSTREAM:COMBINE:INTEGRATE:SCANPY_HVGS (merged)                                    [100%] 1 of 1 ✔
[f9/f3f89e] NFCORE_SCDOWNSTREAM:SCDOWNSTREAM:COMBINE:INTEGRATE:SCANPY_FILTER (merged)                                  [100%] 1 of 1 ✔
[4f/f9c831] NFCORE_SCDOWNSTREAM:SCDOWNSTREAM:COMBINE:INTEGRATE:SCVITOOLS_SCVI (scvi)                                   [100%] 1 of 1 ✔
[8e/f98dfe] NFCORE_SCDOWNSTREAM:SCDOWNSTREAM:COMBINE:INTEGRATE:SCANPY_HARMONY (harmony)                                [100%] 1 of 1 ✔
[66/53b47f] NFCORE_SCDOWNSTREAM:SCDOWNSTREAM:COMBINE:INTEGRATE:SCANPY_BBKNN (bbknn)                                    [100%] 1 of 1 ✔
[03/f69c11] NFCORE_SCDOWNSTREAM:SCDOWNSTREAM:COMBINE:INTEGRATE:SCANPY_COMBAT (combat)                                  [100%] 1 of 1 ✔
[9f/77e752] NFCORE_SCDOWNSTREAM:SCDOWNSTREAM:CLUSTER:NEIGHBORS (scvi-global)                                           [100%] 3 of 3 ✔
[94/cde642] NFCORE_SCDOWNSTREAM:SCDOWNSTREAM:CLUSTER:UMAP (scvi-global)                                                [100%] 4 of 4 ✔
[c6/15e940] NFCORE_SCDOWNSTREAM:SCDOWNSTREAM:CLUSTER:LEIDEN (scvi-global-0.5)                                          [100%] 8 of 8 ✔
[48/120259] NFCORE_SCDOWNSTREAM:SCDOWNSTREAM:CLUSTER:ENTROPY (scvi-global-0.5)                                         [100%] 8 of 8 ✔
[13/e91837] NFCORE_SCDOWNSTREAM:SCDOWNSTREAM:PER_GROUP:SCANPY_PAGA (scvi-global-0.5)                                   [100%] 11 of 11 ✔
[82/7ca637] NFCORE_SCDOWNSTREAM:SCDOWNSTREAM:PER_GROUP:LIANA_RANKAGGREGATE (scvi-global-0.5)                           [100%] 9 of 9 ✔
[19/8fc939] NFC…WNSTREAM:PER_GROUP:DIFFERENTIAL_EXPRESSION:SCANPY_RANKGENESGROUPS (condition:scvi-global-0.5_leiden:3) [100%] 101 of 101 ✔
[8d/4cc575] NFCORE_SCDOWNSTREAM:SCDOWNSTREAM:FINALIZE:ADATA_EXTEND (merged)                                            [100%] 1 of 1 ✔
[23/4d4bf5] NFCORE_SCDOWNSTREAM:SCDOWNSTREAM:FINALIZE:ADATA_TORDS (merged)                                             [100%] 1 of 1, ignored: 1 ✔
[ce/95cfa7] NFCORE_SCDOWNSTREAM:SCDOWNSTREAM:MULTIQC                                                                   [100%] 1 of 1 ✔
-[nf-core/scdownstream] Pipeline completed successfully, but with errored process(es) -
[23/4d4bf5] NOTE: Process `NFCORE_SCDOWNSTREAM:SCDOWNSTREAM:FINALIZE:ADATA_TORDS (merged)` terminated with an error exit status (1) -- Error is ignored
Completed at: 12-Mar-2026 12:05:12
Duration    : 29m 35s
CPU hours   : 1.8 (0.4% failed)
Succeeded   : 209
Ignored     : 1
Failed      : 1
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ea863ec8d7f1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.