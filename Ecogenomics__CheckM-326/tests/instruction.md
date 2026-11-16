# Issue

**Title:** Allow user to specify path to `DATA_CONFIG` file, for use with Singularity containers

## Description

Hi @dparks1134 and @ctSkennerton ,
First of all, thanks for creating CheckM, it's a very much needed tool for working with *de novo* assembly binning !

Right now, the way CheckM is set up, the `DATA_CONFIG` file is distributed with the checkm python package, and updated on the same path when running the `checkm data setRoot <PATH_TO_DB_DIR>` command.

This is causing an issue when running checkM with [singularity containers](https://sylabs.io/guides/3.5/user-guide/introduction.html) as they are read only file-system (i.e. the checkm package files can not be overwritten).

For example:

```bash 
$ singularity shell quay.io/biocontainers/checkm-genome:1.1.3--py_1
Singularity> checkm data setRoot ~/tmp/checkm/
[2022-03-01 15:40:09] INFO: CheckM v1.1.3
[2022-03-01 15:40:09] INFO: checkm data setRoot /home/maxime_borry/tmp/checkm/
[2022-03-01 15:40:09] INFO: [CheckM - data] Check for database updates. [setRoot]

Unexpected error: <class 'NameError'>
Traceback (most recent call last):
  File "/usr/local/lib/python3.7/site-packages/checkm/checkmData.py", line 87, in checkPermissions
    open(self.configFile, 'a')
OSError: [Errno 30] Read-only file system: '/usr/local/lib/python3.7/site-packages/checkm/DATA_CONFIG'

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "/usr/local/bin/checkm", line 611, in <module>
    checkmParser.parseOptions(args)
  File "/usr/local/lib/python3.7/site-packages/checkm/main.py", line 834, in parseOptions
    self.updateCheckM_DB(options)
  File "/usr/local/lib/python3.7/site-packages/checkm/main.py", line 78, in updateCheckM_DB
    DBM = DBManager(set_path=action[1])
  File "/usr/local/lib/python3.7/site-packages/checkm/checkmData.py", line 107, in __init__
    self.setRoot(set_path)
  File "/usr/local/lib/python3.7/site-packages/checkm/checkmData.py", line 142, in setRoot
    if not self.config.checkPermissions():
  File "/usr/local/lib/python3.7/site-packages/checkm/checkmData.py", line 88, in checkPermissions
    except (IOError, e):
NameError: name 'e' is not defined
```

What I propose with this pull request is to allow the user to specify the `DATA_CONFIG` path, so that it can be also on a writeable filesystem.

With this modification, the user can use:
- `checkm data setRoot <PATH_TO_DB_DIR>` like before, and use the `DATA_CONFIG` file provided with the checkM package
- `checkm data setRoot <DB_PATH> <CONFIG_PATH>` to also specify the path to a `DATA_CONFIG` file somewhere writeable.

Note: this feature is particularly relevant for the integration of checkm in computation pipelines for HPC, such as in

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e79d420194f3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.