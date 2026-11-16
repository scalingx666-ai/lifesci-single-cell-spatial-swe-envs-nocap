# Issue

**Title:** feat: add LiveView dynamic endpoints

## Description

## Summary

**Complete implementation of dynamic HTTP endpoints for LiveView**, enabling agents to serve computed data to browser-based visualizations.

### Core Features
- **`serve_endpoint(name, path, config?)`** - Register lightweight Python HTTP endpoints
- **`manage_endpoints(action, name?)`** - Unified endpoint lifecycle management (list/info/unregister)
- **Dynamic endpoint dispatch** - `/api/<name>/...` with token-gated server-mode access
- **GET/POST support** - Full browser fetch compatibility with CORS
- **Security enhancements** - Generic error messages, token authentication, path validation

### Architecture
```
Browser → Modal Tunnel (8770) → Agent (aiohttp) → Dynamic Endpoints
```

### Enhancements (beyond original PR)
- ✅ **Security**: Fix error message information leakage - return generic errors to clients
- ✅ **Lifecycle Management**: Add list_endpoints(), unregister_endpoint(), endpoint_exists()
- ✅ **Unified Tool**: manage_endpoints(action, name?) reduces tool count
- ✅ **Testing**: 22 new tests (61 total, 100% pass rate)
- ✅ **Documentation**: Complete design docs + Hub compatibility analysis

### Use Cases
- Gosling computed tracks (A/B compartments, peak annotations)
- Interactive dashboards with POST-based queries
- On-demand data generation
- Future: tileset-style APIs

### Documentation
- **Technical Design**: docs/DESIGN.md - Complete architecture, design decisions, security model
- **Enhancements**: docs/ENHANCEMENTS.md - Code review issues addressed, migration guide
- **Hub Compatibility**: docs/HUB_COMPATIBILITY.md - pantheon-hub requires **no changes**

## Test Plan

All tests passing (61/61):
```bash
uv run pytest tests/test_live_view_factory_fallback.py \
             tests/test_startup_defaults.py \
             tests/test_live_view_data_server_endpoints.py \
             tests/test_live_view_serve_endpoint_tool.py \
             tests/test_live_view_endpoint_management.py \
             tests/test_live_view_manage_endpoints_tool.py -q
# Result: 61 passed in 1.86s ✅

uv run python -m compileall -q pantheon/toolsets/live_view tests/test_live_view_*.py
# Result: no errors ✅
```

## Hub Compatibility

✅ **pantheon-hub requires no code changes**

- Modal tunnel (port 8770) already configured
- Token auth environment variables already injected
- CORS already supports POST/OPTIONS
- /api/ routes are Agent-side only (no conflict with Hub routes)
- Dynamic endpoints fully reuse existing LiveView server-mode infrastructure

See docs/HUB_COMPATIBILITY.md for detailed analysis.

## Code Quality

- **Test Coverage**: 100% of public API
- **Security**: Generic error messages, token validation, path sanitization
- **Performance**: Builder pattern optimizes registration-time vs request-time costs
- **Documentation**: 3 comprehensive technical docs (1,705 lines)
- **Backward Compatible**: All original PR #120 functionality preserved

## Changes

**Modified**:
- pantheon/toolsets/live_view/data_server.py (+67 lines) - Endpoint registry, lifecycle methods, error sanitization
- pantheon/toolsets/live_view/toolset.py (+83 lines) - manage_endpoints tool
- pantheon/factory/templates/skills/live_view/SKILL.md (+13 lines) - Updated docs

**Added**:
- tests/test_live_view_endpoint_management.py (+178 lines) - Lifecycle tests
- tests/test_live_view_manage_endpoints_tool.py (+204 lines) - Tool tests
- docs/DESIGN.md (+936 lines) - Complete technical design
- docs/ENHANCEMENTS.md (+301 lines) - Enhancement summary
- docs/HUB_COMPATIBILITY.md (+468 lines) - Hub compatibility analysis

**Total**: +2,250 lines / -2 lines

---

**Ready to merge** ✅ - Production-ready, fully tested, comprehensively documented

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a7bb77645b24`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.