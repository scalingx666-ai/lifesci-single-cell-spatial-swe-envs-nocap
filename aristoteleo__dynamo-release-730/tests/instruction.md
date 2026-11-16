# Issue

**Title:** Fix: Add compatibility with anndata >= 0.10

## Description

This PR fixes the `ImportError: cannot import name 'read' from 'anndata'` that occurs when using dynamo-release with anndata >= 0.10.

### Problem

The `anndata.read()` function was **deprecated in anndata 0.8** and **removed in anndata 0.10.0** (released December 2023). Dynamo-release v1.4.1 still imports this function directly, causing an ImportError for all users with modern anndata versions.

**Error**:
```python
ImportError: cannot import name 'read' from 'anndata'
```

**Location**: `dynamo/data_io.py`, line 9

### Impact

This issue affects:
- All users with anndata >= 0.10 (released Dec 2023)
- All new installations (pip installs latest anndata by default)
- All downstream packages (spateo-release, etc.)


### Solution

Added a **compatibility wrapper** that:
1. Tries to import `read` from anndata (for old versions)
2. Falls back to `read_h5ad` if `read` doesn't exist (for new versions)
3. Maintains backward compatibility with anndata < 0.10
4. Ensures forward compatibility with anndata >= 0.10

### Changes

**File**: `dynamo/data_io.py`

**Before**:
```python
from anndata import (
    AnnData,
    read,  # ❌ This doesn't exist in anndata >= 0.10
    read_csv,
    # ... other imports
)
```

**After**:
```python
from anndata import (
    AnnData,
    read_csv,
    # ... other imports (removed 'read' from here)
)

# Compatibility with anndata >= 0.10
# The 'read' function was deprecated and removed in anndata 0.10.0
# Use read_h5ad as a fallback for backward compatibility
try:
    from anndata import read
except ImportError:
    # anndata >= 0.10 removed 'read', use 'read_h5ad' instead
    from anndata import read_h5ad as read
```

### Testing

**Tested with**:
-  anndata 0.9.2 (old version) - Works
- anndata 0.10.9 (new version) - Works
- anndata 0.12.2 (latest) - Works
- Python 3.11
- macOS, Linux (expected to work on Windows too)

**Verification**:
```python
# Import test
import dynamo as dyn  # ✅ No ImportError
print(dyn.__version__)  # ✅ 1.4.1

# Downstream test
import spateo as st  # ✅ Now works!
print(st.__version__)  # ✅ 1.1.1
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9f825632b3b3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.