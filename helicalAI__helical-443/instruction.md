# Issue

**Title:** fix(mapping): query Ensembl BioMart over https without pybiomart

## Description

Refs helicalAI/dashboard#2538

`_get_ensembl_mart_df` used pybiomart over plain http. pybiomart cannot connect over https, and importing it installs a global requests cache that never expires. At the same time, it uses and parses XML.

- Fetch the gene table with one https TSV request to Ensembl BioMart.
- Retry up to 5 times with exponential backoff. Ensembl's outage page returns HTTP 200, so a response only counts when it is a complete TSV.
- Cache the table per species with `functools.lru_cache`.
- Remove the `pybiomart` dependency.

Only non-`hsapiens` species are affected; `hsapiens` still uses the static CSV.

## Testing
- `ci/tests/test_utils` passes, including 5 new tests with a mocked `requests.get`.
- Against live Ensembl, the result equals the old pybiomart output for `mmusculus` and `hsapiens`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `efe3d703dff8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.