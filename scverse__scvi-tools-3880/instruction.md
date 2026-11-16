# Issue

**Title:** Fix: Extract some methods from FCLayers for easier inheritance

## Description

Add _build_layer, _is_linear_layer, _apply_batch_norm, and _apply_layer as overridable hooks so subclasses (e.g. SplitFCLayers in DRVI) can customise layer construction and dispatch without duplicating the forward loop and scArches logic. Store constructor args as instance attributes so _build_layer can reference them.

Also, fix set_online_update_hooks to use [..., dims_to_update] instead of [:, dims_to_update] so the gradient mask works on 3-D weight tensors (as in DRVI decoder).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ed5485f9a10a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.