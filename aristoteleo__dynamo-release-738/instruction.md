# Issue

**Title:** Added more species support to convert the ensembl to symbol

## Description

This pull request enhances species detection and gene symbol conversion utilities in the preprocessing pipeline, with a focus on supporting more species and improving robustness. It also adds an automatic installation step for the `polars` library in the GTF parser. The most important changes are grouped below:

**Species Detection and Mapping Improvements**

* Expanded the supported species in `_infer_species_and_release` and the gene symbol conversion function, now covering human, mouse, rat, zebrafish, fly, chicken, dog, pig, cow, and macaque, with improved Ensembl ID prefix matching logic to avoid misclassification due to overlapping prefixes. [[1]](diffhunk://#diff-538c1e1ff32e392a99fa0b43b3751b775b6a40c4915f1b9a4ed1083a79294c62R29-R40) [[2]](diffhunk://#diff-538c1e1ff32e392a99fa0b43b3751b775b6a40c4915f1b9a4ed1083a79294c62L37-L45)
* Updated docstrings and documentation in `convert2gene_symbol` to reflect the expanded species support and clarify behavior for unknown or missing gene symbols.

**Gene Symbol Conversion Robustness**

* Improved species prefix validation in gene symbol conversion, including a helper function to handle overlapping prefixes and ensure only valid IDs for the detected species are queried.
* Extended the test gene IDs for database validation to include all supported species, improving reliability of the conversion process.

**Default Behavior Adjustments**

* Changed the default Ensembl release version from 109 to 77 for database initialization, likely to improve compatibility or stability.

**Dependency Management**

* Added logic to automatically install the `polars` library if not present when importing the GTF parser, improving ease of use for new users.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `641f7f3f6a13`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.