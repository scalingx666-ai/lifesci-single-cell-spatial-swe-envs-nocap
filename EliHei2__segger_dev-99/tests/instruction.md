# Issue

**Title:** CosMx Data Support and Transcript Processing Improvements

## Description

CosMx Data Support and Transcript Processing Improvements

## Overview
This PR adds support for CosMx data processing and improves transcript handling by addressing missing metadata fields and adding boundary buffering capabilities.

## Key Changes

### 1. CosMx Data Support
- Added `cosmx.yaml` configuration file to handle CosMx-specific data formats and parameters
- Implemented CosMx-specific data loading and processing pipeline

### 2. Transcript Processing Improvements
- **Transcript ID Generation**
  - Added automatic generation of unique transcript IDs based on coordinate information
  - Implemented coordinate-based hashing to ensure consistent IDs across runs

- **Nuclear Overlap Computation**
  - Added dynamic computation of transcript-nucleus overlap when not pre-computed
  - Implemented efficient spatial indexing for overlap calculations
  - Added fallback mechanism when `overlaps_nucleus` field is missing

- **Quality Value (QV) Handling**
  - Made QV filtering optional when the field is not present
  - Added graceful handling of missing QV information in transcript filtering

### 3. Boundary Processing Enhancement
- **Adaptive Boundary Buffering**
  - Implemented area-based boundary buffering for membrane stainings
  - Added buffer ratio parameter to control boundary expansion/shrinking
  - Buffer distance calculated based on polygon area: `sqrt(area/π) * (buffer_ratio - 1.0)`
  - Added automatic recomputation of nuclear overlap when buffer ratio ≠ 1

## Technical Details
- Added new utility functions in `_utils.py` for boundary buffering and transcript processing
- Modified `STSampleParquet` class to handle missing metadata fields
- Updated transcript filtering logic to be more flexible with missing fields
- Added logging for boundary-transcript overlap computation status

## Impact
These changes enable:
1. Support for CosMx data processing
2. More flexible handling of different data formats and missing fields
3. Support for both nuclear and membrane stainings through boundary buffering
4. Improved robustness in transcript processing

## Testing
- Added test cases for coordinate-based ID generation
- Verified boundary buffering with different buffer ratios
- Tested nuclear overlap computation with both pre-computed and missing fields

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1a46ea44935a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.