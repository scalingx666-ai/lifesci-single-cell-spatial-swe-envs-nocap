# Issue

**Title:** One hot issue fix

## Description

Addressing this issue 


```bash
export PYTHONNOUSERSITE="True"
conda create -y -n cell2location_sept_2025 python=3.10
conda activate cell2location_sept_2025

pip3 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu124
pip3 install scvi-tools
git clone git+https://github.com/vitkl/scvi-tools.git
git checkout one-hot-fix
pip install .[dev]

pip install scanpy igraph matplotlib ipykernel jupyter

python -m ipykernel install --user --name=cell2location_sept_2025 --display-name='Environment (cell2location_sept_2025)'
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8480e66ef2fd`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.