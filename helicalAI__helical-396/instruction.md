# Issue

**Title:** fix(security): remove pickle deserialization paths (CWE-502)

## Description

## Summary

Hardens CWE-502 (insecure deserialization) findings in the transcriptformer / dict-asset loading paths:

1. Load dict assets as JSON instead of pickle (original commit on this branch).
2. Remove the `pickle.load` code path from `load_embeddings` in `helical/models/transcriptformer/utils/utils.py`; non-`.h5` paths now raise an explicit `RuntimeError`.

## Why the `load_embeddings` pickle path is not used

`load_embeddings` is only reached via transcriptformer embedding surgery: `tokenizer/vocab.py` -> `construct_gene_embeddings` -> `load_embeddings`, driven by `inference_config.pretrained_embedding`.

**Every bundled and downloaded transcriptformer embedding asset is HDF5, not pickle:**
- The default species path in `transcriptformer_config.py` builds `f"{s}_gene.h5"`.
- The entire download manifest (`list_of_files_to_download`) is `*_gene.h5` files (e.g. `homo_sapiens_gene.h5`, `mus_musculus_gene.h5`, ...).

So in the normal/default flow the `.pkl` branch was **dead code** -- everything went through the safe `load_from_hdf5` HDF5 path. The `pickle.load` branch was only reachable if a user *explicitly* passed a custom `pretrained_embedding` path ending in `.pkl`. No first-party asset triggers it, which is also why the scanner rated this finding LOW confidence.

## Changes to `load_embeddings`

- Removed the `.pkl` / `pickle.load(f)` branch -- no `pickle.load` remains in the file.
- Dropped the now-unused `import pickle`.
- Removed the dead `with open(embeddings_path, "rb") as f:` wrapper (the HDF5 branch never used `f`; `load_from_hdf5` opens the path itself).
- Any non-`.h5` path now raises a clear `RuntimeError`. Previously such a path silently produced an `UnboundLocalError`, so this is also a small robustness improvement.

## Compatibility

No behavior change for the default flow (all assets are `.h5`). The only observable change is that a user explicitly passing a `.pkl` (or other non-`.h5`) path now gets an explicit error instead of an unpickle.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4fbb1264b420`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.