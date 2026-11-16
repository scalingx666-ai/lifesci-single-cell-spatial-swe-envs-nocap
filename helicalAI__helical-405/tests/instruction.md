# Issue

**Title:** fix(lora): make out_proj a real module call for scGPT/Nicheformer

## Description

Supersedes #403 (accidentally opened against `release` instead of `main`).

## Summary

Stock `torch.nn.MultiheadAttention.forward()` applies its output projection via a raw `F.linear(x, out_proj.weight, out_proj.bias)` call inside `F.multi_head_attention_forward` — never an actual `self.out_proj(x)` module call. PEFT-style LoRA adapters attach by overriding a module's `forward()`, so an adapter targeting `out_proj` was never on the gradient path and never trained. This affected **both** scGPT and Nicheformer, since both build on stock `MultiheadAttention` (scGPT via a vendored-but-unmodified copy of it, Nicheformer via plain `nn.TransformerEncoderLayer`).

`bio-agent` PR #1009 worked around this by retargeting LoRA from `out_proj` to `linear1`/`linear2`, which stops LoRA from touching attention at all. This PR fixes the actual root cause instead.

## Changes

- **New**: `helical/utils/transformer_encoder.py` — `LoraCompatibleSelfAttention`, a self-attention-only (no cross-attention, no separate K/V weights) replacement for `nn.MultiheadAttention` that always finishes with an explicit `self.out_proj(context)` call. Uses `F.scaled_dot_product_attention` for the fused fast path when attention weights aren't requested, and a manual softmax path (matching the existing `need_weights=True` behavior) when they are. Parameter names (`in_proj_weight`, `in_proj_bias`, `out_proj.weight`, `out_proj.bias`) and weight-init (`_reset_parameters`) exactly match stock `MultiheadAttention`, since pretrained-checkpoint loading (e.g. scGPT's `load_pretrained`) matches state-dict keys by name with `strict=False` and silently skips anything that doesn't match. Also includes `TransformerEncoderLayer`/`TransformerEncoder`, adapted from scGPT's old vendored copy with the dead PyTorch "fast path" scaffolding removed (confirmed always inert whenever `self.training=True`, i.e. always during fine-tuning).
- **scGPT**: `helical/models/scgpt/model_dir/transformer.py` (previously a 718-line vendored copy of PyTorch's own `TransformerEncoder`/`TransformerEncoderLayer`) is now a thin re-export shim pointing at the shared module. `model_dir/model.py`'s existing import is unaffected.
- **Nicheformer**: `helical/models/nicheformer/modeling_nicheformer.py` now builds its encoder from the shared classes instead of stock `nn.TransformerEncoderLayer`/`nn.TransformerEncoder`. `model.py`'s `Nicheformer._extract_attention_weights` (which reaches directly into `.self_attn`/`.norm1`/`.norm_first`) needed **no changes** — verified by test.
- Updated one hardcoded model-`repr()` snapshot test (`test_scgpt_utils.py::test_load_model`) for the two lines that legitimately change (`MultiheadAttention` → `LoraCompatibleSelfAttention`, `NonDynamicallyQuantizableLinear` → `Linear`).

## Out of scope (flagged only)

`helical/models/scgpt/model_dir/multiomic_model.py` is a separate scGPT variant that imports **stock** `torch.nn.TransformerEncoder` directly (not the vendored file), so it still has the same underlying issue. `bio-agent`'s fine-tuning path doesn't use this variant, so it's left untouched here.

## Follow-up (tracked separately, not part of this PR)

Once this is merged/released, `bio-agent`'s `_get_default_lora_target_modules` for scGPT/Nicheformer should be reverted to target `out_proj` again (undoing PR #1009's `linear1`/`linear2` workaround) — tracked at helicalAI/bio-agent#1015.

## Test plan

- [x] New `ci/tests/test_utils/test_transformer_encoder.py`: numerical equivalence vs. stock `nn.MultiheadAttention` (no mask / key-padding mask / causal mask / fused-vs-manual paths), shape parity in training mode, a LoRA-style forward-hook-fires test on `out_proj`, `output_attentions` shape checks, gradient-flow-to-`out_proj` check, and checkpoint-key-name parity vs. stock.
- [x] New `ci/tests/test_scgpt/test_scgpt_attention_lora_fix.py` and `ci/tests/test_nicheformer/test_nicheformer_lora_fix.py`: confirm `out_proj` is reachable via `named_modules()` and receives nonzero gradient through the real model construction path for each model; Nicheformer test also directly exercises the exact `_extract_attention_weights` call pattern against a real (tiny) model.
- [x] All existing `ci/tests/test_scgpt/` and `ci/tests/test_nicheformer/` tests pass unchanged (57/57 Nicheformer, 30/31 scGPT — the one updated snapshot test noted above).
- [x] `black` formatting applied to all changed/new files.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9fd850716a46`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.