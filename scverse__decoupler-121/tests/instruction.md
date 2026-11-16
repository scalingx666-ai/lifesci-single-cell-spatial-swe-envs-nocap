# Issue

**Title:** Gene Symbols from Ensembl or custom source + better handling of identifiers and orthology translation

## Description

Hi @PauBadiaM,

Here I implemented the stuff that the email discussion was about, now the user has 5 choices:
- Use the gene symbols from the web service (the original behaviour)
- Update them from Ensembl
- Update them from UniProt
- Provide a `dict[str, set[str]]` with any custom mapping
- Use UniProt IDs instead of gene symbols

I checked all `omnip.get_*` functions with various options, and everything looks alright for me. If you agree, feel free to merge this to `main`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4f3eb817488f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.