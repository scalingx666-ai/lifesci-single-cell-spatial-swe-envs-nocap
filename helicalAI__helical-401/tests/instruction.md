# Issue

**Title:** fix(security): remove pickle write in geneformer; annotate numpy-in-pytorch

## Description

## Summary

Addresses two Bastion auto-analysis findings from helicalAI/dashboard#1154.

### 1. CWE-502 avoid-pickle — `helical/models/geneformer/geneformer_utils.py`
Removed the `pkl.dump(gene_id_to_ensemble, open("./human_gene_to_ensemble_id.pkl", "wb"))` side-effect write in `load_mappings`, plus the duplicate/now-unused `import pickle as pkl`.

- `load_mappings()` has **no callers** in helical, bio-agent, or dags (dead code path).
- The written `.pkl` had **no in-repo reader**.
- The function's return value is unchanged, so callers (if any are added later) are unaffected.

Result: pickle is fully removed from the file.

### 2. numpy-in-pytorch-modules — `helical/models/tahoe/tahoe_x1/model/blocks.py`
Annotated the `np.load` inside `ChemEncoder.__init__` with `# nosemgrep` and a justification.

- The call runs **once at construction** to read a `.npy` drug-fingerprint file into a tensor.
- It is **not part of `forward()`** and does not affect ONNX tracing or runtime efficiency.
- This is vendored Tahoe code; the annotation matches the existing convention already used at `blocks.py:387`.

## Testing
- Both files compile (`python -m py_compile`).
- No tests reference `load_mappings` / `ChemEncoder`; no runtime behavior changed (dead-code cleanup + comment-only annotation).
- High-effort workflow code review: no findings.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01QZEAKo8XzdH6S2ugf2i67i

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `740c92e4ae31`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.