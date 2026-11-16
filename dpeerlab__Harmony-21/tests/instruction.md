# Issue

**Title:** Update dependency sklearn to scikit-learn

## Description

`sklearn` is deprecated and the pip install does not work anymore. Here is the error:
```bash
$ pip install harmonyTS
Looking in indexes: https://pypi.org/simple, https://pypi.ngc.nvidia.com
Collecting harmonyTS
  Downloading harmonyTS-0.1.4-py3-none-any.whl (16 kB)
Requirement already satisfied: numpy>=1.14.2 in ./mamba/envs/singlecell_test1/lib/python3.10/site-packages (from harmonyTS) (1.23.5)
Requirement already satisfied: pandas>=0.22.0 in ./mamba/envs/singlecell_test1/lib/python3.10/site-packages (from harmonyTS) (2.0.1)
Requirement already satisfied: scipy>=1.0.1 in ./mamba/envs/singlecell_test1/lib/python3.10/site-packages (from harmonyTS) (1.10.1)
Collecting sklearn (from harmonyTS)
  Downloading sklearn-0.0.post5.tar.gz (3.7 kB)
  Preparing metadata (setup.py) ... error
  error: subprocess-exited-with-error

  × python setup.py egg_info did not run successfully.
  │ exit code: 1
  ╰─> [18 lines of output]
      The 'sklearn' PyPI package is deprecated, use 'scikit-learn'
      rather than 'sklearn' for pip commands.

      Here is how to fix this error in the main use cases:
      - use 'pip install scikit-learn' rather than 'pip install sklearn'
      - replace 'sklearn' by 'scikit-learn' in your pip requirements files
        (requirements.txt, setup.py, setup.cfg, Pipfile, etc ...)
      - if the 'sklearn' package is used by one of your dependencies,
        it would be great if you take some time to track which package uses
        'sklearn' instead of 'scikit-learn' and report it to their issue tracker
      - as a last resort, set the environment variable
        SKLEARN_ALLOW_DEPRECATED_SKLEARN_PACKAGE_INSTALL=True to avoid this error

      More information is available at
      https://github.com/scikit-learn/sklearn-pypi-package

      If the previous advice does not cover your use case, feel free to report it at
      
      [end of output]

  note: This error originates from a subprocess, and is likely not a problem with pip.
error: metadata-generation-failed

× Encountered error while generating package metadata.
╰─> See above for output.

note: This is an issue with the package mentioned above, not pip.
hint: See above for details.
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `866309c120c5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.