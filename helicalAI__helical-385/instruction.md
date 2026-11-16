# Issue

**Title:** fix(security): harden CWE-502 torch.load sites (weights_only + nosemgrep)

## Description

## What & why

Follow-up to the annotation-only PR #384. This PR **actually mitigates** the CWE-502 (unsafe deserialization) scan findings from helicalAI/dashboard#1154 for the **`torch.load`** sites, and suppresses the Trail of Bits scanner on the sites that are now safe (or unavoidably require full unpickling).

Scope: **Groups A + B (`torch.load`)**. **Group C** (raw `pickle.load` of gene dictionaries — geneformer/uce/transcriptformer/tahoe) is **intentionally deferred** to a follow-up PR and is left untouched here.

## Changes

| Site | Change | Rationale |
|---|---|---|
| `scgpt_utils.py`, `uce_utils.py` (×2), `uce/gene_embeddings.py` (×2) | add `weights_only=True` + `# nosemgrep` | payloads are tensors / plain state dicts; real mitigation |
| `transcriptformer/model.py`, `tahoe/.../blocks.py`, `base_models.py:319` | `# nosemgrep` + justification | already used `weights_only=True`; just clears the scanner |

Notes:
- Under the pinned **torch 2.7.0**, `weights_only` already defaults to `True`, so the added kwargs are **no-ops at runtime** and only harden intent.
- `uce_utils.py:167` (UCE model-weights load) was **missed by the Bastion scan** but hardened here for consistency with the token-file load in the same file.
- Every `# nosemgrep: trailofbits.python.pickles-in-pytorch.pickles-in-pytorch` is placed on the line **immediately preceding** its `torch.load` (Semgrep only honors adjacent suppressions).


## Verification

- **scGPT** and **HyenaDNA** load real downloaded checkpoints end-to-end (dummy instantiation + `test_scgpt_utils.py`/`test_hyena_dna_model.py` pass).
- `python -m py_compile` passes on all 7 touched files.
- CI exercises these load paths against **real, non-mocked** upstream artifacts, so the PR checks will catch any load breakage.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `af17d8721597`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.