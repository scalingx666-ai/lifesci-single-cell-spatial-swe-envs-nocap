# Issue

**Title:** Support visium-hd for snakemake

## Description

Fix 

We can now pass the fullres_image directly:
```sh
snakemake --config data_path=/space/ranger/out fullres_image_file=fullres_image.btf [...]
```

@reJELIN, could you please try this branch and let me know if it works for you?
I also added a `stardist_proseg.yaml` config to run both stardist + proseg on top.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8a790f511aea`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.