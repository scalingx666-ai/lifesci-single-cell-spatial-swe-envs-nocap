# Issue

**Title:** Fix inaccurate resource monitor on M series Mac

## Description

For a cpu intensive task (let's say there isn't any I/O workload), wall clock time should roughly equal  `(cpu_user + cpu_system) / cpu_core_count`. On my Mac M2 (10 cpu cores), the result below looks much more reasonable, and it's also close to what we see from activity monitor:

<img width="1491" alt="截屏2025-05-26 20 09 39" src="https://github.com/user-attachments/assets/7a12751c-d839-4473-965c-0a5638a7ea03" />
<img width="698" alt="截屏2025-05-26 20 13 27" src="https://github.com/user-attachments/assets/27194f00-9a53-482f-abe2-947bd8b8ff71" />

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cd275654fb56`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.