# Issue

**Title:** Update nf-schema plugin version to 2.7.2

## Description

Bump nf-schema version to fix CLI parameter type casting with Nextflow v2 parser (default in Nextflow >= 26.04)

Note that an alternative workaround is to set the environment variable `NXF_SYNTAX_PARSER=1`

## PR checklist

- [X] This comment contains a description of changes (with reason).
- [ ] If you've fixed a bug or added code that should be tested, add tests!
- [ ] If you've added a new tool - have you followed the pipeline conventions in the [contribution docs](https://github.com/nf-core/spatialvi/tree/master/docs/CONTRIBUTING.md)
- [ ] If necessary, also make a PR on the nf-core/spatialvi _branch_ on the [nf-core/test-datasets](https://github.com/nf-core/test-datasets) repository.
- [X] Make sure your code lints (`nf-core pipelines lint`).
- [X] Ensure the test suite passes (`nextflow run . -profile test,docker --outdir <OUTDIR>`).
- [ ] Check for unexpected warnings in debug mode (`nextflow run . -profile debug,test,docker --outdir <OUTDIR>`).
- [ ] Usage Documentation in `docs/usage.md` is updated.
- [ ] Output Documentation in `docs/output.md` is updated.
- [ ] `CHANGELOG.md` is updated.
- [ ] `README.md` is updated (including new tool citations and authors/contributors).


Current nf-core/spatialvi dev branch () (tested in a codespace):
```
/workspaces/spatialvi -> nextflow run . -profile test,docker --outdir out --qc_min_counts 5   --qc_min_genes 3   --skip_downstream

 N E X T F L O W   ~  version 26.04.1

Launching `./main.nf` [admiring_rutherford] revision: dbc24d81d4

WARN: Unrecognized config option 'validation.defaultIgnoreParams'
WARN: Unrecognized config option 'validation.monochromeLogs'

------------------------------------------------------
                                        ,--./,-.
        ___     __   __   __   ___     /,-._.--~'
  |\ | |__  __ /  ` /  \ |__) |__         }  {
  | \| |       \__, \__/ |  \ |___     \`-._,-`-,
                                        `._,._,'
  nf-core/spatialvi 1.0dev
------------------------------------------------------

Input/output options
  input                         : https://raw.githubusercontent.com/nf-core/test-datasets/spatialvi/testdata/human-brain-cancer-11-mm-capture-area-ffpe-2-standard_v2_ffpe_cytassist/samplesheet_spaceranger.csv
  outdir                        : out

Space Ranger options
  spaceranger_probeset          : https://raw.githubusercontent.com/nf-core/test-datasets/spatialvi/testdata/human-brain-cancer-11-mm-capture-area-ffpe-2-standard_v2_ffpe_cytassist/outs/probe_set.csv
  spaceranger_reference         : https://raw.githubusercontent.com/nf-core/test-datasets/spatialvi/testdata/homo_sapiens_chr22_reference.tar.gz

Filtering options
  qc_min_counts                 : 5
  qc_min_genes                  : 3
  qc_mito_threshold             : 20.0
  qc_ribo_threshold             : 0.0
  qc_hb_threshold               : 100.0

Principal component analysis options
  pca_use_highly_variable       : true

Clustering options
  cluster_resolution            : 1.0

Integration options
  integration_cluster_resolution: 1.0

Optional outputs
  skip_downstream               : true

Institutional config options
  config_profile_name           : Test profile
  config_profile_description    : Test pipeline functionality, including Space Ranger v2

Generic options
  trace_report_suffix           : 2026-05-21_15-23-12

Core Nextflow options
  runName                       : admiring_rutherford
  containerEngine               : docker
  container.REPORT              : community.wave.seqera.io/library/harmonypy_scanorama_gcc_gxx_pruned:95f731fde0b9ddef
  container.REPORT_INTEGRATED   : community.wave.seqera.io/library/harmonypy_scanorama_gcc_gxx_pruned:95f731fde0b9ddef
  container.MULTIQC             : docker.io/multiqc/multiqc:v1.29
  launchDir                     : /workspaces/spatialvi
  workDir                       : /workspaces/spatialvi/work
  projectDir                    : /workspaces/spatialvi
  userName                      : root
  profile                       : test,docker
  configFiles                   : /workspaces/spatialvi/nextflow.config

!! Only displaying parameters that differ from the pipeline defaults !!
------------------------------------------------------

* The nf-core framework
    https://doi.org/10.1038/s41587-020-0439-x

* Software dependencies
    https://github.com/nf-core/spatialvi/blob/master/CITATIONS.md

ERROR ~ Validation of pipeline parameters failed!

 -- Check '.nextflow.log' file for details
The following invalid input values have been detected:

* --qc_min_genes (3): Value is [string] but should be [integer]
* --qc_min_counts (5): Value is [string] but should be [integer]
* --skip_downstream (true): Value is [string] but should be [boolean]

 -- Check script 'subworkflows/nf-core/utils_nfschema_plugin/main.nf' at line: 68 or see '.nextflow.log' file for more details
 ```
 
 After bumping nf-schema to version 2.7.2 (this PR):
 
 ```
 /workspaces/spatialvi ->  nextflow run . -profile test,docker --outdir out --qc_min_counts 5   --qc_min_genes 3   --skip_downstream

 N E X T F L O W   ~  version 26.04.1

Launching `./main.nf` [pedantic_wescoff] revision: dbc24d81d4


------------------------------------------------------
                                        ,--./,-.
        ___     __   __   __   ___     /,-._.--~'
  |\ | |__  __ /  ` /  \ |__) |__         }  {
  | \| |       \__, \__/ |  \ |___     \`-._,-`-,
                                        `._,._,'
  nf-core/spatialvi 1.0dev
------------------------------------------------------

Input/output options
  input                         : https://raw.githubusercontent.com/nf-core/test-datasets/spatialvi/testdata/human-brain-cancer-11-mm-capture-area-ffpe-2-standard_v2_ffpe_cytassist/samplesheet_spaceranger.csv
  outdir                        : out

Space Ranger options
  spaceranger_probeset          : https://raw.githubusercontent.com/nf-core/test-datasets/spatialvi/testdata/human-brain-cancer-11-mm-capture-area-ffpe-2-standard_v2_ffpe_cytassist/outs/probe_set.csv
  spaceranger_reference         : https://raw.githubusercontent.com/nf-core/test-datasets/spatialvi/testdata/homo_sapiens_chr22_reference.tar.gz

Filtering options
  qc_min_counts                 : 5
  qc_min_genes                  : 3
  qc_mito_threshold             : 20.0
  qc_ribo_threshold             : 0.0
  qc_hb_threshold               : 100.0

Principal component analysis options
  pca_use_highly_variable       : true

Clustering options
  cluster_resolution            : 1.0

Integration options
  integration_cluster_resolution: 1.0

Optional outputs
  skip_downstream               : true

Institutional config options
  config_profile_name           : Test profile
  config_profile_description    : Test pipeline functionality, including Space Ranger v2

Generic options
  trace_report_suffix           : 2026-05-21_15-59-20

Core Nextflow options
  runName                       : pedantic_wescoff
  containerEngine               : docker
  launchDir                     : /workspaces/spatialvi
  workDir                       : /workspaces/spatialvi/work
  projectDir                    : /workspaces/spatialvi
  userName                      : root
  profile                       : test,docker
  configFiles                   : /workspaces/spatialvi/nextflow.config

!! Only displaying parameters that differ from the pipeline defaults !!
------------------------------------------------------

* The nf-core framework
    https://doi.org/10.1038/s41587-020-0439-x

* Software dependencies
    https://github.com/nf-core/spatialvi/blob/master/CITATIONS.md

executor >  local (7)
[6f/57cf17] NFCORE_SPATIALVI:SPATIALVI:INPUT_CHECK:UNTAR_SPACERANGER_INPUT (fastq_dir.tar.gz)         [100%] 1 of 1 ✔
[-        ] NFCORE_SPATIALVI:SPATIALVI:INPUT_CHECK:UNTAR_DOWNSTREAM_INPUT                             -
[b5/e48a61] NFCORE_SPATIALVI:SPATIALVI:FASTQC (CytAssist_11mm_FFPE_Human_Glioblastoma_2)              [100%] 1 of 1 ✔
[ab/109694] NFC…ATIALVI:SPACERANGER:SPACERANGER_UNTAR_REFERENCE (homo_sapiens_chr22_reference.tar.gz) [100%] 1 of 1 ✔
[84/d9aab2] NFC…VI:SPATIALVI:SPACERANGER:SPACERANGER_COUNT (CytAssist_11mm_FFPE_Human_Glioblastoma_2) [100%] 1 of 1 ✔
[a3/ce59d7] NFCORE_SPATIALVI:SPATIALVI:SDATA_READ_VISIUM (CytAssist_11mm_FFPE_Human_Glioblastoma_2)   [100%] 1 of 1 ✔
[af/91e12e] NFCORE_SPATIALVI:SPATIALVI:SDATA_MERGE                                                    [100%] 1 of 1 ✔
[08/b50418] NFCORE_SPATIALVI:SPATIALVI:MULTIQC (spatialvi)                                            [100%] 1 of 1 ✔
-[nf-core/spatialvi] Pipeline completed successfully-
Completed at: 21-May-2026 16:09:24
Duration    : 10m 2s
CPU hours   : 0.6
Succeeded   : 7


 ```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d0fd35d9a985`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.