# Issue

**Title:** fix: drop MAML2-NOTCH entries from the consensus resource

## Description

MAML2 is a nuclear transcriptional co-activator, not a secreted or membrane-bound ligand. The interaction NOTCH signaling actually involves is between the cleaved intracellular domain of the NOTCH receptor and MAML2 inside the nucleus, regulating transcription, not a cell-surface ligand-receptor pair. The four MAML2-NOTCH1/2/3/4 rows in `omni_resource.csv` tagged `consensus` look like a curation artifact from the same process discussed in #177.

Removed the four rows, updated the `test_select_resource` count (4624 to 4620), and added `test_consensus_resource_excludes_maml2` as a regression check.

Tested `tests/test_select_resource.py` and `tests/test_orthology.py` in a fresh Python 3.12 container: 9/9 passing.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `705bcf9dd9fa`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.