# Issue

**Title:** Add mLLMCelltype to tools and categories

## Description

Added mLLMCelltype package to the tools database and classified it as a Classification tool.

mLLMCelltype is a multi-model LLM consensus framework for single-cell RNA sequencing cell type annotation,
featuring transparent uncertainty quantification and structured deliberation process that significantly improves annotation accuracy.

The package is available in both R and Python implementations.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0e289a3a983a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.