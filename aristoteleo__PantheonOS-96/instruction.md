# Issue

**Title:** feat: chat export/import for portable replay bundles

## Description

## Summary
- Add `export_chat_bundle()` / `import_chat_bundle()` in `pantheon/chatroom/export.py`
- Bundles are self-contained zip archives with `chat.jsonl`, `chat.meta.json`, `manifest.json`, and referenced files
- Path scanning with regex for absolute, `.pantheon/`, and `workdir/` paths; automatic rewriting on export/import
- Import dedup: skips creation if original `chat_id` already exists locally
- Expose as `@tool export_chat` and `@tool import_chat` on `ChatRoom`

## Test plan
- [ ] Export a chat, verify zip contains all referenced files with correct paths
- [ ] Import on a fresh workspace, verify chat and files restore correctly
- [ ] Re-import same bundle, verify no duplicate chat created
- [ ] Verify files >100MB are skipped with log warning

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1b5214ff8b83`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.