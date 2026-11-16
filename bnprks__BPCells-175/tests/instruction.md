# Issue

**Title:** [r] Improve error printing in `call_peaks_macs`

## Description

I noticed that `call_peaks_macs` wasn't printing out helpful error messages because they get trapped inside the `mclapply` call sometimes. (This came up because I accidentally broke macs in my local virtualenv, but when tests failed there weren't good error messages)

Previous output when MACS hit an error while running peak calling:
```
Warning message:
In parallel::mclapply(file_names, function(shell_file) { :
  2 function calls resulted in an error
```

New output when MACS hits an error while running peak calling:

```
2024-12-20 16:01:21  Error running MACS for cluster: a_group
MACS log file written to: /tmp/RtmpwYXpma/file30a8322a9d7527/macs-test/output/a_group/log.txt
2024-12-20 16:01:21  Error running MACS for cluster: b_group
MACS log file written to: /tmp/RtmpwYXpma/file30a8322a9d7527/macs-test/output/b_group/log.txt
Error in `call_peaks_macs()`:
! MACS calls encountered 2 failures
• See error logs listed above
Run `rlang::last_trace()` to see where the error occurred.
```

The problem here is that if we throw an error inside a `mclapply` call, then it just reports there was some error but the text never gets printed

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e7551359f85b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.