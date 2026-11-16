# Issue

**Title:** Gate FA2 attention backend on model-class support

## Description

Rationale
---------
select_attn_backend previously returned "flash_attention_2" whenever flash_attn was installed and the device was CUDA, without checking whether the target model class actually declares FA2 support via HF's dispatcher. For BertForMaskedLM (Geneformer) that silently routed the model down a code path transformers can't actually dispatch, so the "Loading ... in bfloat16 for flash_attention_2 compatibility" warning wasn't just cosmetic noise — it flagged a branch that couldn't work. The helical integration-tests job doesn't install flash_attn, so this gap was invisible in CI.

Plan
----
* Add a supports_fa2 parameter to select_attn_backend. Only models whose class declares _supports_flash_attn / _supports_flash_attn_2 can take the FA2 branch; others (Geneformer) fall back to sdpa.
* Pass supports_fa2=True from HelixmRNA. Leave Geneformer on the default (False) and annotate the call site so callers who want FA2 for BertForMaskedLM know they have to wire flash_attn directly.
* Drop the now-unreachable bfloat16-for-FA2 warnings from Geneformer; the sdpa fallback path never triggers them.
* Add a flash-attn-integration CI job that installs flash_attn and smoke-tests both paths: Geneformer (regression guard — must still load on sdpa even with flash_attn present) and HelixmRNA (must actually run on the FA2 branch).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `49290fa1c39a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.