# Issue

**Title:** refactor: improve logging and introduce content conversion for respon…

## Description

…ses API

- Updated logging in agent and file manager to use structured logging with exception handling.
- Added a new function to convert Chat Completions-style content blocks to Responses API blocks, enhancing content handling for user and assistant roles.
- Refactored message conversion logic in Codex and OpenAI adapters to utilize the new content conversion function, streamlining the integration with the Responses API.
- Added tests to validate the new content conversion functionality, ensuring accurate processing of multimodal content blocks.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `01423ce6be8c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.