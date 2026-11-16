# Issue

**Title:** fix(llm): drop the scGPT integration placeholder that shadows the real implementation

## Description

## Problem

`ScGPTModel._predict_integration` is defined **twice** in `omicverse/llm/scgpt_model.py`:

| | lines | length | docstring |
|---|---|---|---|
| first | 1345–1511 | 167 | "Perform batch integration following Tutorial_Integration exactly." |
| second | 1545–1572 | 28 | "Use trained integration model for prediction." |

The second definition is a placeholder — its own comments say so:

```python
def _predict_integration(self, adata, batch_key="batch", **kwargs):
    """Use trained integration model for prediction."""
    ...
    # This would use the actual integration model prediction
    # Similar to the predict method but for integration task
    adata_processed = self.preprocess(adata, add_cls_token=True)

    # Get integrated embeddings from the trained model
    # Implementation would depend on the trained integration model
    embeddings = self.get_embeddings(adata_processed, **kwargs)
```

It is the later binding in the class body, so it is the one that ends up on `ScGPTModel`. The 167-line implementation above it has never executed.

## Impact

Both call sites reach the placeholder:

- **`predict(adata, task="integration")`** (line 1153) already calls `self.preprocess(adata, **kwargs)` on line 1146 and passes the result down. The placeholder preprocesses it a *second* time and returns plain `get_embeddings()` output — no tokenization against the model vocabulary, no batch-aware forward pass.
- **`integrate()`** (line 1513) routes a model with `_integration_trained` set to `self._predict_integration(...)`. So a model that *was* fine-tuned for integration produces exactly the same embeddings as the pre-trained `_apply_post_hoc_integration` path, while the returned dict advertises `integration_method: "trained_model"` and `method: "fine_tuned_integration"`.

The real implementation is the one that does the work: it validates the `X_binned` layer and the batch key, reports the batch distribution, maps genes through `self.vocab`, calls `tokenize_and_pad_batch` with `self.config.max_seq_len`, runs the model, and emits `operation_start` / `operation_complete` telemetry — matching its sibling methods `_predict_annotation` and `_predict_embedding`, which follow the same "Tutorial exactly" structure.

## Fix

Delete the placeholder. `+0 / −29`, no other change.

## Verification

- After the change the class body contains a single `_predict_integration`, at line 1345 (checked with `ast`).
- Both call sites bind to the surviving signature `(self, adata: AnnData, **kwargs)` unchanged — `integrate()` passes `batch_key=batch_key`, which the implementation reads back via `kwargs.get('batch_key', 'batch')` and validates against `adata.obs`.
- `pyflakes` reports no undefined names anywhere in the restored body (lines 1345–1511) — only the "f-string is missing placeholders" notes that already occur throughout the file.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `06735e883b69`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.