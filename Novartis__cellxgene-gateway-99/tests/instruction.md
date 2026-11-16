# Issue

**Title:** Gunicorn support

## Description

Enables production deployment with Gunicorn/WSGI servers by fixing three bugs that prevented the gateway from functioning outside the Flask development server.

  Three Core Fixes

  1. UnicodeDecodeError on Dataset Viewing (b9f4d35)
    - Removed accept-encoding from proxied headers
    - Allows requests library to handle compression/decompression transparently
    - File: cache_entry.py:151
  2. WSGI Server Initialization (08c546f)
    - Moved data source initialization from main() to module import time
    - Created initialize_data_sources() called at module load
    - Added guard flag to prevent double initialization
    - Fixes empty file crawler when running under Gunicorn
    - File: gateway.py:84-121
  3. AttributeError in Single Source Configuration (903d257)
    - Changed default_item_source to store ItemSource objects instead of strings
    - Fixes crash when accessing default_item_source.name
    - File: gateway.py:106-116

  Testing

  Verified with both deployment modes:
  - ✅ Gunicorn worker (1 worker)
  - ⚠️ Gunicorn multi-worker (4 workers)
    - It seems the cache does not behave well across workers. I see js/css 404s that appear to be related to an apparent cache hit, but no data being in the cache. **A workaround is sadly to reduce the number of workers to 1.** It seems like any enhancements related to this would be significant reworking of the cache system. Perhaps adding dataset affinity between the workers and the cellxgene backends (portmappinng from dataset to backend process port). Or allocating sufficient memory so you could run MxN datasets (where M=number of workers and N=number of datasets)
  - ✅ Flask development server
  - ✅ File crawler displays datasets
  - ✅ Dataset viewing works correctly

  Impact

  Resolves: GitHub issues #33 and #92 (WSGI compatibility, empty file list)

  This enables production-ready deployment with proper WSGI servers.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `05a95c2ca9ff`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.