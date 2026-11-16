# Issue

**Title:** H5Writer

## Description

## Changes
- Pulled in from @pmelsted's branch (ecmap_vector)
- Changed index char manipulations to use cstring manipulations (should be equivalent)
- H5 utilities to write out vector of string, int, or double
- New class H5Writer which takes an EM or Bootstrap and writes it to the HDF5 file
- Defaults to writing out to HDF5 file now
## Design questions
- Do we want to add an option to write out to plaintext OR do we want to have a utility in kallisto (e.g. `kallisto h5dump`) which takes the H5 result and outputs to plaintext
- FYI, there is already functionality to read/write in `sleuth` so I guess it depends how coupled we want the tools to be
## Notes
- Compression doesn't seem to be as good as I was getting when I built the HDF5 file on R, I need to investigate why. Still better than writing out to plaintext (obviously)
## Code review
- @pmelsted if you have any tips on how I can make `h5utils.{h,cpp}` more modular (particularly the `vec_to_ptr` and `get_datatype_id` functions), I'd be happy to hear them.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `aa6a8a4654f3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.