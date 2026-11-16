# Issue

**Title:** Maintenance: Fixing bugs, typos, version conflicts, etc.

## Description

1. [combosciplex.ipynb](https://github.com/ArianAmani/sCPA/blob/maintenance/docs/tutorials/combosciplex.ipynb) changes:
    - Version conflicts fixed for Colab (now works smoothly in Colab)
    - Data Loading fixed (The previous code didn't work properly)

2. [Installation docs](https://github.com/ArianAmani/sCPA/blob/maintenance/docs/installation.rst) Updated to contain the correct version of prerequisites to install and also added a code block for installing in Colab ().

3. [combosciplex_Rdkit_embeddings.ipynb](https://github.com/ArianAmani/sCPA/blob/maintenance/docs/tutorials/combosciplex_Rdkit_embeddings.ipynb) changes:
    - Version conflicts fixed for Colab (now works smoothly in Colab)
    - Data Loading fixed (The previous code didn't work properly)
    
4. [Kang.ipynb](https://github.com/ArianAmani/sCPA/blob/maintenance/docs/tutorials/Kang.ipynb) changes:
    - Version conflicts fixed for Colab (now works smoothly in Colab)
    - Data Loading fixed (The previous code didn't work properly)
    
5. [_model.py](https://github.com/ArianAmani/sCPA/blob/maintenance/cpa/_model.py) changes:
    - Code was using `smiles_key` although it is optional, fixed to `if smiles_key is not None:`

6. [Norman.ipynb](https://github.com/ArianAmani/sCPA/blob/maintenance/docs/tutorials/Norman.ipynb) changes:
    - Version conflicts fixed for Colab (now works smoothly in Colab)
    - Data Loading fixed (The previous code didn't work properly)
    - obs keys changed to match the linked dataset
    * `pathway` needs to be added to the linked dataset. Currently unavailable.

7. [pyproject.toml](https://github.com/ArianAmani/sCPA/blob/maintenance/pyproject.toml) changes:
    - Resolved some of the version conflicts.
    * `scanpy` is not getting installed using `pip install cpa-tools`. Needs to be resolved.

*  #16

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c53a68e2eebe`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.