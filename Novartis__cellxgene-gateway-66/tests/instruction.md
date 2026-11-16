# Issue

**Title:** Dockerise cellxgene-gateway

## Description

This PR adds a `Dockerfile` (and instructions) to build a Docker image with cellxgene-gateway in it. Perhaps you find it useful.

**Note**: I had to pin the `MarkupSafe` Python module to pre-2.1 to prevent the following error:

```sh
Traceback (most recent call last):
  File "/usr/local/bin/cellxgene-gateway", line 5, in <module>
    from cellxgene_gateway.gateway import main
  File "/usr/local/lib/python3.9/site-packages/cellxgene_gateway/gateway.py", line 16, in <module>
    from flask import (
  File "/usr/local/lib/python3.9/site-packages/flask/__init__.py", line 14, in <module>
    from jinja2 import escape
  File "/usr/local/lib/python3.9/site-packages/jinja2/__init__.py", line 12, in <module>
    from .environment import Environment
  File "/usr/local/lib/python3.9/site-packages/jinja2/environment.py", line 25, in <module>
    from .defaults import BLOCK_END_STRING
  File "/usr/local/lib/python3.9/site-packages/jinja2/defaults.py", line 3, in <module>
    from .filters import FILTERS as DEFAULT_FILTERS  # noqa: F401
  File "/usr/local/lib/python3.9/site-packages/jinja2/filters.py", line 13, in <module>
    from markupsafe import soft_unicode
ImportError: cannot import name 'soft_unicode' from 'markupsafe' (/usr/local/lib/python3.9/site-packages/markupsafe/__init__.py)
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5814cb99437e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.