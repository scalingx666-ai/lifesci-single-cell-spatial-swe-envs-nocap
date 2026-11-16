# Issue

**Title:** Register Medidata and ToolUniverse plugins for life sciences research

## Description

Add MCP server integrations for Medidata and ToolUniverse to expand the life sciences research toolkit.

## Medidata Plugin

Medidata's MCP Connector for Claude provides clinical trial tools:

**Tools:**
- search_support_documentation - Query Medidata's platform documentation for Rave EDC, Data Connect, and Clinical Data Studio
- get_ranked_sites - Predictive site ranking for clinical trials
- get_supported_disease_areas - Available disease areas for site ranking

**Features:**
- Platform Help for product documentation queries
- Predictive Site Ranking for Intelligent Trials customers to identify sites aligned with enrollment goals

**Resources:**
- Documentation: https://learn.medidata.com/en-US/bundle/mcp-server-documentation/page/medidata_mcp_server_documentation.html
- Support: helpdesk@mdsol.com
- MCP Server: https://mcp.imedidata.com/mcp

## ToolUniverse Plugin

AI agents and tools for scientific discovery and automation, democratizing access to advanced research capabilities.

## Changes

- Updated .claude-plugin/marketplace.json with both plugin entries
- Added medidata/.claude-plugin/plugin.json with MCP configuration
- Added tooluniverse/.claude-plugin/plugin.json with MCP configuration
- Included ToolUniverse MCP binary bundle

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `00dd850d85e5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.