# Issue

**Title:** fix NoneType errors

## Description

Fix the following error:

```

barcode_fastq	barcodes.fastq.gz
read1	read1.fastq.gz
read2	None
bases	16
prefix	
suffix	
whitelist	None
func	<function run_barcode at 0x7f50f63389d0>
Traceback (most recent call last):
  File "/usr/local/bin/sinto", line 10, in <module>
    sys.exit(main())
  File "/usr/local/lib/python3.10/site-packages/sinto/arguments.py", line 555, in main
    options.func(options)
  File "/usr/local/lib/python3.10/site-packages/sinto/utils.py", line 24, in wrapper
    func(args)
  File "/usr/local/lib/python3.10/site-packages/sinto/cli.py", line 105, in run_barcode
    addbarcodes.addbarcodes(
  File "/usr/local/lib/python3.10/site-packages/sinto/addbarcodes.py", line 100, in addbarcodes
    if len(whitelist) > 0:
TypeError: object of type 'NoneType' has no len()

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d87da33685a2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.