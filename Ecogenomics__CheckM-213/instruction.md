# Issue

**Title:** Fix checkm data setRoot command to work from command line.

## Description

Briefly, with this patch, `checkm data setRoot <path>` will now correctly set the data root for checkm to `<path>`. Previously it would not respect `<path>` and would instead prompt for interactive output.

In particular, this causes problems with workflows that construct conda environments, because the workflow manager cannot automatically set the data location for a newly installed checkM via the command line.

NOTE: this is a PR into `python3_dev`.

More:

I've been bedeviled for years now by this minor issue, so I thought I'd set out to fix it! It was trickier than expected... The cause of the problem appears to be that the `DBManager` class is created on import of the `defaultValues` module, which happens before any argument parsing happens.

I made the following changes:
* added an explicit `initValues()` call to the DefaultValues object instead of having things depend on class variables;
* in main.py, intercepted the `data SetRoot` action before `initValues()`;
* intercepted the `setRoot` action in DBManager.__init__ before database was initialized;
* added an `os._exit` to get out of things without printing an error message.

It's a bit hacky but it seemed like the minimal set of changes needed to fix this, and I _think_ it works more generally. Happy to massage and updated as needed.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `39f7a8317c1a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.