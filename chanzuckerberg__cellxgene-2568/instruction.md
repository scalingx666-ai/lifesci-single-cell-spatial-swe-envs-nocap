# Issue

**Title:** feat: annotate command improvements

## Description

#2566 

#### Reviewers
**Functional:** 
@seve 

**Readability:** 
@MaximilianLombardo: please review `cellxgene annotate --help` and review changes from UX perspective.


---

## Changes
* Replace --input-h5ad-file with a positional argument, for consistency with other CLI commands
* Replace --update-h5ad-file with --overwrite, for consistency with `prepare` command.
* Fix/clarify various help descriptions
* Fix final output message when input file is overwritten

The revised help output:
```
Usage: annotate.py <options> <path to H5AD input file>

  Add predicted annotations to an H5AD file. Run `cellxgene annotate --help`
  for more information.

Options:
  -c, --annotation-prefix TEXT    An optional prefix used to form the names
                                  of: 1) new `obs` annotation columns that
                                  will store the predicted annotation values
                                  and confidence scores, 2) `obsm` embeddings
                                  (reference and umap embedding), and 3) `uns`
                                  metadata for the prediction operation
                                  [default: cxg]
  --classifier TEXT               For cell type annotation, the classifier
                                  level to use. The classifier is model-
                                  dependent, so refer to documentation for the
                                  specified model for valid values.
  -l, --counts-layer TEXT         If specified, raw counts will be read from
                                  the AnnData layer of the specified name. If
                                  unspecified, raw counts will be read from
                                  `X` matrix, unless 'raw.X' exists, in which
                                  case that will be used.
  -g, --gene-column-name TEXT     The name of the `var` column that contains
                                  gene names. The values in this column will
                                  be used to match genes between the query and
                                  reference datasets. If not specified, the
                                  gene names are expected to exist in
                                  `var.index`.
  -h, --help                      Show this message and exit.
  --mlflow-env-manager [virtualenv|conda|local]
                                  Annotation model prediction will be
                                  installed and executed in the specified type
                                  of environment. MacOS users on Apple Silicon
                                  (arm64, M1, M2, etc.) are recommended to use
                                  'conda' to avoid Python package installation
                                  errors. If 'conda' is specified then
                                  cellxgene must also have been installed
                                  within a conda environment
  --model-cache-dir TEXT          Local directory used to store model files
                                  that are retrieved from a remote location.
                                  Model files will be read from this directory
                                  first, if they exist, to avoid repeating
                                  large downloads.
  -m, --model-url TEXT            The URL of the model used to prediction
                                  annotated labels. May be a local filesystem
                                  directory or S3 path (s3://)  [required]
  --organism [Homo sapiens|Mus musculus]
                                  For cell type annotation, the organism of
                                  the dataset. Used to normalize gene names to
                                  HGLC conventions when an annotation model
                                  has been trained using data from different
                                  organism.
  -o, --output-h5ad-file <filename>
                                  The output H5AD file that will contain the
                                  generated annotation values. If this option
                                  is not provided, the input file will be
                                  overwritten to include the new annotations;
                                  in this case you must specify --overwrite.
  --overwrite                     Allow overwriting of the specified H5AD
                                  output file, if it exists. For safety, you
                                  must specify this flag if the specified
                                  output file already exists or if the
                                  --output-h5ad-file option is not provided.
  -n, --run-name TEXT             An optional run name that will be used as a
                                  suffix to form the names of new `obs`
                                  annotation columns that will store the
                                  predicted annotation values and confidence
                                  scores. This can be used to allow multiple
                                  annotation predictions to be run on a single
                                  AnnData object.
  --use-gpu / --no-use-gpu        Whether to use a GPU for annotation
                                  operations (highly recommended, if
                                  available).
  --use-model-cache / --no-use-model-cache
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `450261f109e9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.