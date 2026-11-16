# Issue

**Title:** Add extra star parameters for read filtering

## Description

This pull request adds new options to fine-tune read alignment filtering in the STAR mapping step, allowing users to set minimum alignment score thresholds and matched base ratios. 

**Mapping parameter additions:**

* Added new command-line arguments (`--star-min-score`, `--star-min-score-ratio`, `--star-min-matched-bases-ratio`) to control the minimum alignment score and matched base ratios for STAR, with defaults set for each. These are documented in `docs/usage.md` and registered in the pipeline argument parser. [[1]](diffhunk://#diff-72376d0b487d7231cf31959bf266f6aea098e899743bae02e36d176cef4db476R137-R147) [[2]](diffhunk://#diff-570e05e1a62d7c56b569bcb63758edfa4ac14efe00862e0b5bc84585f82bd9c8R575-R605)
* Updated the `Pipeline` class to include new attributes for these parameters, set their defaults, and load them from the parsed arguments. [[1]](diffhunk://#diff-570e05e1a62d7c56b569bcb63758edfa4ac14efe00862e0b5bc84585f82bd9c8R125-R127) [[2]](diffhunk://#diff-570e05e1a62d7c56b569bcb63758edfa4ac14efe00862e0b5bc84585f82bd9c8R910-R912)

**STAR command modification:**

* Modified the `alignReads` function in `stpipeline/core/mapping.py` to accept the new parameters and pass them to the STAR command line as `--outFilterScoreMin`, `--outFilterScoreMinOverLread`, and `--outFilterMatchNminOverLread`. [[1]](diffhunk://#diff-ee17b880d197f5f1e128d7dd62910ea35d139524af69eff4af4c6f6eb43d633dR35-R37) [[2]](diffhunk://#diff-ee17b880d197f5f1e128d7dd62910ea35d139524af69eff4af4c6f6eb43d633dR60-R62) [[3]](diffhunk://#diff-ee17b880d197f5f1e128d7dd62910ea35d139524af69eff4af4c6f6eb43d633dR127-R132)
* Updated calls to `alignReads` within the pipeline's `run` method to include the new parameters. [[1]](diffhunk://#diff-570e05e1a62d7c56b569bcb63758edfa4ac14efe00862e0b5bc84585f82bd9c8R1138-R1140) [[2]](diffhunk://#diff-570e05e1a62d7c56b569bcb63758edfa4ac14efe00862e0b5bc84585f82bd9c8R1198-R1200)

**Logging:**

* Extended pipeline logging to report the values of the new STAR filtering parameters at runtime.# 

## Type of change

- [x] New feature (non-breaking change which adds functionality)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `23a85fa5c8f5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.