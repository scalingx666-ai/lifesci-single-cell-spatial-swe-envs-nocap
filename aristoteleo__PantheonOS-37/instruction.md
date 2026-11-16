# Issue

**Title:** feat: update custom endpoints support for custom_anthropic and custom_openai

## Description

- Add CustomEndpointConfig dataclass for custom endpoint configuration
- Support CUSTOM_ANTHROPIC_* and CUSTOM_OPENAI_* environment variables
- Update setup wizard to handle custom endpoint configuration
- Add provider detection priority for custom endpoints
- Add "custom" tag for explicitly using custom endpoint models
- Update API key/base URL retrieval to check custom endpoints first

<img width="886" height="508" alt="image" src="https://github.com/user-attachments/assets/dad5ae42-d1df-4355-a064-b8398466ff74" />

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `001125d74f19`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.