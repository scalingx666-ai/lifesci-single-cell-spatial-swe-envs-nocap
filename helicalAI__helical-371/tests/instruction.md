# Issue

**Title:** Fix save_model to include fine-tuning head weights

## Description

## Summary

- `save_model()` currently calls `torch.save(self.model.state_dict(), path)`, which only persists backbone weights and silently drops the `fine_tuning_head`
- Users who fine-tune, save, and reload get random head weights instead of trained ones
- Affects all 7 model types (Geneformer, scGPT, UCE, HyenaDNA, Caduceus, HelixmRNA, Mamba2mRNA)
- Changed to `self.state_dict()` which includes both backbone and head
- Updated `load_model` to auto-detect three checkpoint formats for backward compatibility (full, backbone-only, legacy pickle)

## Test plan

- [ ] Fine-tune a model, save, reload — verify head weights are preserved
- [ ] Load a v2.0.0 backbone-only checkpoint — verify warning is logged and backbone loads correctly
- [ ] Load a pre-v2.0.0 legacy pickle checkpoint — verify backward compatibility

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7ff138a30bb5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.