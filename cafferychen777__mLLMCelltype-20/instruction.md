# Issue

**Title:** Fix OpenRouter model handling in consensus check process

## Description

This commit addresses issues with OpenRouter model handling during the consensus check phase:

1. Modified get_provider.R to correctly identify OpenRouter models by detecting the '/' character in model names
2. Enhanced check_consensus.R to properly handle OpenRouter models with provider prefixes (e.g., 'google/gemini-2.5-pro-preview-03-25')
3. Updated facilitate_cluster_discussion.R to pass the consensus_check_model parameter to check_consensus function
4. Modified consensus_annotation.R to ensure consensus_check_model is properly passed through all relevant function calls

These changes ensure that when using OpenRouter models for consensus checking, the system correctly identifies them as OpenRouter models and uses the appropriate API keys, rather than trying to interpret the provider prefix as a separate provider.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0cb309182c61`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.