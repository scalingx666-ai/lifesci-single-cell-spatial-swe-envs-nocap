# Issue

**Title:** Add Life Sciences MCP Marketplace

## Description

## Summary

Creates a new marketplace for life sciences MCP servers, providing access to 6 research and analysis tools:

### MCPB-based (local servers):
- **benchling-mcp**: Benchling notebooks, entries, and schemas
- **10x-genomics**: 10x Genomics Cloud analysis data

### HTTP-based (remote servers):
- **pubmed**: PubMed biomedical literature search
- **biorender**: Scientific illustrations and diagrams
- **synapse**: Sage Bionetworks research data management
- **wiley-scholar-gateway**: Wiley academic research access

## Implementation

- All plugin manifests validated with `claude plugin validate`
- MCPB files hosted on anthropic-serve S3 bucket (not in repo)
- Comprehensive README with installation and authentication instructions
- Proper author attribution for each provider

## Installation

Users can install with:
```bash
claude marketplace add https://github.com/anthropics/life-sciences.git
claude plugin install life-sciences pubmed
```

## Test Plan

- ✅ Marketplace validation passing
- ✅ MCPB files uploaded to S3 and accessible
- ✅ Plugin manifests reference correct S3 URLs
- ✅ All 6 plugins properly configured

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8190603b95f5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.