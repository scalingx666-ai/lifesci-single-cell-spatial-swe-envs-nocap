# Issue

**Title:** Add remote MCP plugin entries and configuration

## Description

…nd Open Targets

Add plugin configurations for five new remote MCP servers:
- bioRxiv (DeepSense.AI) - biology preprints search
- Clinical Trials (DeepSense.AI) - clinical trial data access
- ChEMBL (DeepSense.AI) - bioactive molecule and drug discovery data
- Owkin - AI-powered drug discovery and precision medicine
- Open Targets - drug target identification and validation data

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9dd566fe2e11`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.