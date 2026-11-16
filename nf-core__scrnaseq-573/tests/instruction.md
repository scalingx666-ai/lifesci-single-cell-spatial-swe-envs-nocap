# Issue

**Title:** Bump nf schema 2.8.0

## Description

This PR bumps the `nf-schema` plugin from `2.5.1` to `2.8.0`.

The main motivation is , fixed in [2.8.0](https://github.com/nextflow-io/nf-schema/releases/tag/2.8.0). With nf-schema<2.8.0, calling `nextflow run nf-core/scrnaseq --input lamin://instance/artifacts/ABCDEFGHI` fails even though the lamin URI can correctly resolve to a csv file. With nf-schema 2.8.0, the validation of the input value is retried against the resolved real path (e.g. `s3://lamin-instance/path/to/underlying/input.csv`).

This version bump thus allows `nf-core/scrnaseq` workflows to be ran with lamin:// input artifacts.

I wasn't sure whether to send this PR to the master branch or to the dev branch. If master is better, I'm happy to recreate it there.

---

One caveat is that nf-schema 2.8.0 requires Nextflow >=26.04.0 (2.7.3 and earlier still work with 25.10.0), so this PR also bumps the pipeline's minimum Nextflow version from 25.10.4 to **26.04.9**, the latest stable bugfix release in the 26.04 series ([release](https://github.com/nextflow-io/nextflow/releases/tag/v26.04.9)), rather than 26.04.0. The CI matrix, README badge, and RO-Crate metadata use the same minimum. A version-gate smoke check confirmed that 26.04.6 is rejected and 26.04.9 can launch the pipeline help; targeted config/README lint passed with no failures.

---

## PR checklist

- [x] This comment contains a description of changes (with reason).
- [ ] ~If you've fixed a bug or added code that should be tested, add tests!~
- [ ] ~If you've added a new tool - have you followed the pipeline conventions in the [contribution docs](https://github.com/nf-core/scrnaseq/tree/master/docs/CONTRIBUTING.md)~
- [ ] ~If necessary, also make a PR on the nf-core/scrnaseq _branch_ on the [nf-core/test-datasets](https://github.com/nf-core/test-datasets) repository.~
- [x] Make sure your code lints (`nf-core pipelines lint`).
- [x] Ensure the test suite passes (`nextflow run . -profile test,docker --outdir <OUTDIR>`).
- [x] Check for unexpected warnings in debug mode (`nextflow run . -profile debug,test,docker --outdir <OUTDIR>`).
- [ ] ~Usage Documentation in `docs/usage.md` is updated.~
- [ ] ~Output Documentation in `docs/output.md` is updated.~
- [x] `CHANGELOG.md` is updated.
- [ ] ~`README.md` is updated (including new tool citations and authors/contributors).~

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6c6a2a5f1689`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.