# Issue

**Title:** Reduce FASTQC time limit from 120h to the process_low default (4h)

## Description

FASTQC on this pipeline runs on demultiplexed FASTQ pairs and routinely finishes in minutes, yet conf/modules.config hardcodes `time = { 120.h * task.attempt }` for the FASTQC withName block. This override predates the FASTQC step itself (introduced wholesale alongside CELLRANGER_COUNT/CELLRANGERARC_COUNT's 240h limits in b5bcedb, "Move increased runtime limits from base.config to modules.config") and was never tied to any reported FASTQC-specific runtime issue.

On HPC sites where QOS/partition wall-time caps are shorter than 120h (a very common setup), Slurm rejects the job submission outright with `QOSMaxWallDurationPerJobLimit`, failing the pipeline on its very first task before any real work runs.

Removing the override lets FASTQC fall back to the `process_low` default of `4.h * task.attempt` (from conf/base.config), which is far more than FASTQC needs and is compatible with typical HPC wall-time limits.

## PR checklist

- [x ] This comment contains a description of changes (with reason).
- [ ] If you've fixed a bug or added code that should be tested, add tests!
- [ ] If you've added a new tool - have you followed the pipeline conventions in the [contribution docs](https://github.com/nf-core/scrnaseq/tree/master/docs/CONTRIBUTING.md)
- [ ] If necessary, also make a PR on the nf-core/scrnaseq _branch_ on the [nf-core/test-datasets](https://github.com/nf-core/test-datasets) repository.
- [] Make sure your code lints (`nf-core pipelines lint`).
- [] Ensure the test suite passes (`nextflow run . -profile test,docker --outdir <OUTDIR>`).
- [] Check for unexpected warnings in debug mode (`nextflow run . -profile debug,test,docker --outdir <OUTDIR>`).
- [ ] Usage Documentation in `docs/usage.md` is updated.
- [ ] Output Documentation in `docs/output.md` is updated.
- [ ] `CHANGELOG.md` is updated.
- [ ] `README.md` is updated (including new tool citations and authors/contributors).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c972f5688eb2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.