# Issue

**Title:** fix(hyena_dna): load weights-only checkpoint with weights_only=True

## Description

## Problem

HyenaDNA is the only model still loading its checkpoint with `torch.load(..., weights_only=False)`, which allows arbitrary code execution during unpickling (CWE-502). Every other model (scGPT, UCE, TranscriptFormer, Tahoe) already uses `weights_only=True`.

It couldn't simply flip the flag: the checkpoints hosted on S3 are the **original PyTorch-Lightning training checkpoints**, which pickle non-tensor objects (OmegaConf `DictConfig`/`ListConfig`, an `ABCMeta` class, optimizer/scheduler/loop state). `weights_only=True` rejects those with `UnpicklingError` — a hard crash, not a subtle regression.

## Fix

The code only ever consumes `checkpoint["state_dict"]` (pure tensors). Inference and fine-tuning both start from the weights with a **fresh** optimizer/scheduler, so the training-lifecycle state is entirely unused.

1. Point `HyenaDNAConfig` at a **new** S3 key `hyena_dna/<model>.weights.ckpt` — a slimmed, tensor-only re-save (`{"state_dict": <tensors>}`). The original `.ckpt` is left untouched, so this is fully reversible and older pinned helical versions keep working.
2. Flip the loader to `weights_only=True`.
3. Update `ci/download_all.py` and the config test for the new filename.

The one-off conversion (load full ckpt → keep `state_dict` → re-save) is done offline; the re-saved weights are byte-for-byte identical to the originals (SHA-256 verified). It's not part of the package.

## Scope: all five hosted checkpoints

All five checkpoints hosted on S3 are re-saved as weights-only and referenced from `ci/download_all.py` (`tiny-1k`, `tiny-1k-d256`, `small-32k`, `medium-450k`, `large-1m`). Note: only the two tiny variants are currently exposed via `HyenaDNAConfig.model_map` (i.e. loadable via `from_pretrained`); the larger ones are hosted so the artifacts exist if they're added to `model_map` later.

## Why there is no regression

- `checkpoint["state_dict"]` is the only thing read anywhere in the hyena_dna path (verified).
- Fine-tuning builds a fresh optimizer + scheduler; it never resumes from checkpoint optimizer state.
- Re-saved weights are byte-for-byte identical (SHA-256 verified). Files also shrink (unused optimizer state dropped).
- No other download/load sites for the checkpoint exist in helical, bio-agent, or bio-utils.

## ⚠️ Required before merge/release

The `.weights.ckpt` files must be uploaded to the `helicalpackage` S3 bucket first (new key `hyena_dna/<model>.weights.ckpt`, do **not** overwrite the originals). Until then `Downloader.download_via_name` will fail and HyenaDNA will not load.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4fbb1264b420`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.