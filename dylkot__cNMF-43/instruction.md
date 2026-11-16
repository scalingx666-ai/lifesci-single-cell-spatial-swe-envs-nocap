# Issue

**Title:** adding multiprocess option from python native multiprocess module

## Description

Hi,

This PR adds the functionality of using python native multiprocess module to parallelize execution of factorize.
To do so it adds 1 function, 1 method (NMF class) and 1 additional import

The method "factorize_multi_process" takes the maximum number of workers as an integer and launch the corresponding number of  "factorize" call, with the corresponding arguments through the function/wrapper "factorize_mp_signature".

The import is from python std lib: "from multiprocessing import Pool "

usage:
```
# instead of calling 
nmf_obj.factorize()
# call
nmf_obj. factorize_multi_process(<number of workers>)
```


I tested it on a "CentOS Linux release 7.9.2009 (Core)" Linux server.

This could be used directly inside a python program or replace the CLI launch 1 by 1. 
In a first time, I did not want to change your code, neither the README. 

If you wish, I can make a PR that adds the option to use multiprocess from the CLI (keeping the older option available).
And  detail those options (CLI and in script) in the README.

Best,
Romain

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `99f8414bf37b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.