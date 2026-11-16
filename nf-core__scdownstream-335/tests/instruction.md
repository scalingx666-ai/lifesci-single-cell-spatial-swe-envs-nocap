# Issue

**Title:** Fix relative paths for scvi_model, scanvi_model and mito_genes

## Description

## Summary

Wrap `--scvi_model`, `--scanvi_model` and `--mito_genes` in `file(..., checkIfExists: true)` in `main.nf`, as is already done for `base_adata`, `symphony_reference`, `s_genes`, `g2m_genes` and `interesting_genes`.

### Symptom

Passing a relative local path, e.g. `--scvi_model ../02_integration/results/.../model.pt`, aborts the run:

```
nextflow.exception.ProcessUnrecoverableException: Not a valid path value: '../...model.pt'
```

Nextflow shows this as "Execution aborted due to an unexpected error", because the dynamic `errorStrategy` closure in `conf/base.config` cannot be evaluated for a task that has no work dir. That is only a side effect and is not changed here.

### Root cause

`params.scvi_model`, `params.scanvi_model` and `params.mito_genes` were passed through `main.nf` -> `workflows/scdownstream.nf` -> subworkflows as raw Strings and then fed into process `path` inputs (`SCVITOOLS_SCVI`, `SCVITOOLS_SCANVI`, `SCANPY_FILTER`, `SCANPY_PLOTQC`). Nextflow only accepts absolute paths or URLs for plain Strings given to a `path` input, so relative paths are rejected. The pipeline tests did not catch this because they pass URLs (`pipelines_testdata_base_path + 'extension_base/model.pt'`), which are valid Strings.

### Fix

```diff
+    def mito_genes_file = params.mito_genes ? file(params.mito_genes, checkIfExists: true) : null
+    def scvi_model      = params.scvi_model ? file(params.scvi_model, checkIfExists: true) : null
+    def scanvi_model    = params.scanvi_model ? file(params.scanvi_model, checkIfExists: true) : null
...
-        params.mito_genes,
+        mito_genes_file,
...
-        params.scvi_model,
-        params.scanvi_model,
+        scvi_model,
+        scanvi_model,
```

- When a param is unset the value is `null`, so the downstream truthiness checks (`scvi_model ? ch_h5ad : ch_h5ad_hvg`, `scvi_model ? channel.value([[id: 'scvi'], scvi_model]) : [[], []]`, `mito_genes ?: []`) behave as before.
- URLs (used in the tests) still work, because `file()` resolves them to remote paths.
- Take-block comments are updated to `path: file or null`.

Audited and deliberately left unchanged:

- `expimap_gmt`: already wrapped with `file(..., checkIfExists: true)` in `subworkflows/local/integrate/main.nf`.
- `integration_excluded_genes`: already wrapped with `file()` in `workflows/scdownstream.nf` and `subworkflows/local/combine/main.nf`.
- `scimilarity_model`: wrapped with `file(..., checkIfExists: true)` in `subworkflows/local/scimilarity/main.nf` and relies on `.endsWith('.tar.gz')` on the String, so it is not touched.
- `celldex_reference`: consumed as a samplesheet by `samplesheetToList`, not by a `path` input.

## Evidence

Verified with a minimal Nextflow repro: a tiny process with `path x`, called with `channel.value(params.p)`:

- `--p ../f.txt` => `Not a valid path value`
- `--p /abs/f.txt` => works

Only `nextflow lint` of the touched files was run locally (no errors). The nf-test suite was not run locally; CI covers it.

## PR checklist

- [x] This comment contains a description of changes (with reason).
- [ ] If you've fixed a bug or added code that should be tested, add tests! (existing tests exercise the `file()` path via URLs; no new test data added for relative paths)
- [x] If you've added a new tool - have you followed the pipeline conventions in the [contribution docs](https://github.com/nf-core/scdownstream/tree/master/docs/CONTRIBUTING.md) (n/a)
- [x] If necessary, also make a PR on the nf-core/scdownstream _branch_ on the [nf-core/test-datasets](https://github.com/nf-core/test-datasets) repository (n/a)
- [ ] Make sure your code lints (`nf-core pipelines lint`). (`nextflow lint` on touched files is clean)
- [ ] Ensure the test suite passes (`nextflow run . -profile test,docker --outdir <OUTDIR>`).
- [ ] Check for unexpected warnings in debug mode (`nextflow run . -profile debug,test,docker --outdir <OUTDIR>`).
- [x] Usage Documentation in `docs/usage.md` is updated. (n/a)
- [x] Output Documentation in `docs/output.md` is updated. (n/a)
- [x] `CHANGELOG.md` is updated.
- [x] `README.md` is updated (including new tool citations and authors/contributors). (n/a)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2c7b8a44d59d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.