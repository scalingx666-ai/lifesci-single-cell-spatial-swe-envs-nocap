# Issue

**Title:** Fix exception loading checkpoint

## Description

Addresses the following exception that occurs when re-running with a machine with more memory:
```
cellbender:remove-background: Running inference...
Traceback (most recent call last):
  File "/opt/conda/bin/cellbender", line 8, in <module>
    sys.exit(main())
  File "/opt/conda/lib/python3.7/site-packages/cellbender/base_cli.py", line 123, in main
    cli_dict[args.tool].run(args)
  File "/opt/conda/lib/python3.7/site-packages/cellbender/remove_background/cli.py", line 185, in run
    return main(args)
  File "/opt/conda/lib/python3.7/site-packages/cellbender/remove_background/cli.py", line 219, in main
    posterior = run_remove_background(args)
  File "/opt/conda/lib/python3.7/site-packages/cellbender/remove_background/run.py", line 113, in run_remove_background
    inferred_model, _, _, _ = run_inference(dataset_obj=dataset_obj, args=args)
  File "/opt/conda/lib/python3.7/site-packages/cellbender/remove_background/run.py", line 768, in run_inference
    final_elbo_fail_fraction=args.final_elbo_fail_fraction)
  File "/opt/conda/lib/python3.7/contextlib.py", line 74, in inner
    return func(*args, **kwds)
  File "/opt/conda/lib/python3.7/site-packages/cellbender/remove_background/train.py", line 248, in run_training
    best_test_elbo = max(test_elbo)
ValueError: max() arg is an empty sequence
```

Note that I don't understand the checkpoint code very well, so there may be a cleaner way to do this.  I simply eliminated the test_elbo local variable and refer to the list stored in the model directly.

Also, html generation was failing because the way lxml.html.clean needs to be installed has changed, so DockerfileGit contains a fix for that.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a4da38a2b977`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.