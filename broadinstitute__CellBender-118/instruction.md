# Issue

**Title:** Fix setup.py to include subpackages

## Description

Current version of `setup.py` installs incomplete package when installing in non-developer mode with `pip install git+https://github.com/broadinstitute/CellBender.git@v0.2.0#egg=cellbender`

This results in an error:
```
$ cellbender
Traceback (most recent call last):
  File "/projects/b1038/Pulmonary/nmarkov/test/venv/bin/cellbender", line 8, in <module>
    sys.exit(main())
  File "/projects/b1038/Pulmonary/nmarkov/test/venv/lib/python3.9/site-packages/cellbender/base_cli.py", line 90, in main
    parser = get_populated_argparser()
  File "/projects/b1038/Pulmonary/nmarkov/test/venv/lib/python3.9/site-packages/cellbender/base_cli.py", line 76, in get_populated_argparser
    module_argparse = importlib.import_module('.'.join(module_argparse_str_list))
  File "/projects/b1038/tools/pyenv/versions/3.9.5/lib/python3.9/importlib/__init__.py", line 127, in import_module
    return _bootstrap._gcd_import(name[level:], package, level)
  File "<frozen importlib._bootstrap>", line 1030, in _gcd_import
  File "<frozen importlib._bootstrap>", line 1007, in _find_and_load
  File "<frozen importlib._bootstrap>", line 972, in _find_and_load_unlocked
  File "<frozen importlib._bootstrap>", line 228, in _call_with_frames_removed
  File "<frozen importlib._bootstrap>", line 1030, in _gcd_import
  File "<frozen importlib._bootstrap>", line 1007, in _find_and_load
  File "<frozen importlib._bootstrap>", line 984, in _find_and_load_unlocked
ModuleNotFoundError: No module named 'cellbender.remove_background'
```

Please, create a new version tag when you fix setup.py

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2507742203a3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.