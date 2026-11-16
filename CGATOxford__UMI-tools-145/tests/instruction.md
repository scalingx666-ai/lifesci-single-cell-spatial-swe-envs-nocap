# Issue

**Title:** Precythonize extensions

## Description

This PR changes the way the cython extensions are handled.

Previously extensions were cythonized and compiled on the fly using 'pyximport'. This required users to have access to the install directory the first time the extension was required. It also installed the extension in a weird place. 

Now the cythonized extension is provided, and is compiled at install-time. This means that users do not have to have cython installed *before* they install umi_tools (it also means they don't need it afterwards either, but that is a secondary concern), but we do not rely on pyximport.

I have a feeling we may also be able to remove the try..expects around import statements. They ahve been left in for now. I havn't yet been able to test if the installation works on a clean machine. 

**It does mean that if you change _umi_tools.pyx you MUST re-cythonize before committing and pushing. If you wish to test changes, you must re-run setup.py.**

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9d8c1eae6854`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.