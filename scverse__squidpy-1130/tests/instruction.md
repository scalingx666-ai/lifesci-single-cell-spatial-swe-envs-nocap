# Issue

**Title:** Add explicit error handling in _make_tiles.py

## Description

## Summary
- Adds upfront parameter validation with clear `KeyError`/`ValueError` messages to `make_tiles()`, `make_tiles_from_spots()`, `_get_largest_scale_dimensions()`, and `_get_spot_coordinates()`
- Validates that image/spots keys exist in `sdata`, `tile_size` has positive values, and `min_tissue_fraction` is in [0, 1]
- Adds 5 test cases covering all new error conditions

## Test plan
- [x] `test_make_tiles_invalid_image_key` — bad image key raises `KeyError`
- [x] `test_make_tiles_invalid_tile_size` — non-positive tile size raises `ValueError`
- [x] `test_make_tiles_invalid_min_tissue_fraction` — out-of-range fraction raises `ValueError`
- [x] `test_make_tiles_from_spots_invalid_spots_key` — bad spots key raises `KeyError`
- [x] `test_make_tiles_from_spots_invalid_image_key` — bad image key raises `KeyError`

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `95d8b18a875f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.