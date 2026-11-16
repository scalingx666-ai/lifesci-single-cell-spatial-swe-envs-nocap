# Issue

**Title:** fix: Improve error handling for API responses

## Description

This commit addresses the 'Unexpected response format from OpenRouter API' error:

1. Enhanced check_consensus.R:
   - Added robust NULL and type checking before processing responses
   - Improved handling of empty or invalid responses
   - Added fallback mechanism for non-character responses

2. Enhanced process_openrouter.R:
   - Added detailed error logging for OpenRouter API errors
   - Added extraction and logging of error messages, codes, and types
   - Added full response structure logging for debugging

3. Updated version to 1.2.3 and documentation:
   - Updated DESCRIPTION file with new version number
   - Added detailed changelog in NEWS.md
   - Updated README.md with recent updates section

These changes make the code more robust against various API response scenarios and provide better diagnostic information when errors occur.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `23b97246fbe4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.