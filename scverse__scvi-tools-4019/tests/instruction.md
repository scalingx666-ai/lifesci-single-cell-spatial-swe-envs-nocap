# Issue

**Title:** feat: FCLayers residual and forward kwargs

## Description

Dear scvi-tools team,

I am making this PR to add two small, backwards-compatible extensions to `FCLayers`. This allows easier extension of DRVI code without requiring to reimplement/repeat big chunks of code. Both are off/unused by default, so existing callers are unaffected.

- **`residual` option.** Wraps every block except the first in a skip connection, whenever that block's input and output widths match. The first block is always excluded, so the flag needs `n_layers >= 2` to do anything.
- **`forward(**kwargs)`.** Extra per-call context is threaded to the `_apply_layer` and `_apply_batch_norm` hooks. The base layers ignore unknown keywords; a subclass can branch on them (e.g. to change behavior between encode/decode calls without a separate code path).

`SplitFCLayers` (`scvi.external.drvi`), the one `FCLayers` subclass in the repo, picks up `**kwargs` on its own `_apply_layer` / `_apply_batch_norm` overrides so it isn't broken by the new signature.

## Testing

`tests/nn/test_fclayers.py` adds a residual test that checks the full forward against a hand-built reference with skip connections on same-width blocks only.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e72ccccfe5fc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.