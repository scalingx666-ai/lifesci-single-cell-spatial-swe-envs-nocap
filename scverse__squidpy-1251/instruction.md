# Issue

**Title:** chore: unify thread and process helpers

## Description

This pull request refactors how the number of parallel workers is determined throughout the codebase. It deprecates the old `_get_n_cores` utility in favor of a new `get_n_processes` function for process-based parallelization and introduces `get_n_threads` for numba-based threading. All relevant imports and function calls are updated to use the new functions, ensuring more consistent and descriptive handling of parallelism.

**Parallelization utilities refactor:**

* Added `get_n_threads` to `src/squidpy/_utils.py` for resolving numba thread counts, and replaced `_get_n_cores` with `get_n_processes`, which is now used for process-based parallelization and is marked as deprecated in favor of numba threading where appropriate.
* Updated all imports and usages of `_get_n_cores` to `get_n_processes` in the following modules: `src/squidpy/experimental/im/_tiling.py`, `src/squidpy/gr/_ligrec.py`, `src/squidpy/gr/_nhood.py`, `src/squidpy/gr/_ppatterns.py`, `src/squidpy/gr/_sepal.py`, and `src/squidpy/im/_feature.py`. [[1]](diffhunk://#diff-54826d95fe3ddfd7f0e261a7244bd955717b360c9d066307ba7ab49387fda9a5L25-R25) [[2]](diffhunk://#diff-f8ee1194403b12d9f322b38697977a0c6403eeb9f92aa402572e3be73d112fe7L27-R27) [[3]](diffhunk://#diff-b0f880b8a8accb2572d8e7c94512c48a8ebc1d2b47c43542eefc3762525f4d31L27-R27) [[4]](diffhunk://#diff-bf9a241973b44a1f9a215d07f233adf22089da131b7569a6dee3d5b6616a8d88L29-R30) [[5]](diffhunk://#diff-62cae86a57d912d2c557f624c90a1c44b0c387fe2870e2813ea56a9c83ef8832L17-R17) [[6]](diffhunk://#diff-cd382ef5e29e7c0c77d6a34031b03250306ab5608a0ff3f72bc977c882bfb289L13-R13)
* Replaced all internal calls to `_get_n_cores` with `get_n_processes` for determining the number of worker processes or threads in parallel computations. [[1]](diffhunk://#diff-54826d95fe3ddfd7f0e261a7244bd955717b360c9d066307ba7ab49387fda9a5L473-R473) [[2]](diffhunk://#diff-f8ee1194403b12d9f322b38697977a0c6403eeb9f92aa402572e3be73d112fe7L421-R421) [[3]](diffhunk://#diff-b0f880b8a8accb2572d8e7c94512c48a8ebc1d2b47c43542eefc3762525f4d31L210-R210) [[4]](diffhunk://#diff-b0f880b8a8accb2572d8e7c94512c48a8ebc1d2b47c43542eefc3762525f4d31L315-R315) [[5]](diffhunk://#diff-bf9a241973b44a1f9a215d07f233adf22089da131b7569a6dee3d5b6616a8d88L218-R218) [[6]](diffhunk://#diff-62cae86a57d912d2c557f624c90a1c44b0c387fe2870e2813ea56a9c83ef8832L114-R114) [[7]](diffhunk://#diff-cd382ef5e29e7c0c77d6a34031b03250306ab5608a0ff3f72bc977c882bfb289L87-R87)
* Updated documentation and comments to reference the new `get_n_processes` convention and clarify its intended usage and deprecation plan.

These changes standardize parallelization configuration, improve code clarity, and prepare the codebase for future migration to numba threading.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9b81fe7de9eb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.