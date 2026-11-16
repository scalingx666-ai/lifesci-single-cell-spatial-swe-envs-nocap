# Issue

**Title:** Fix get_data gh

## Description

I found the reason of #131

Basically, **gh::gh_token()** is not optional but a requirement for **piggyback::pb_download()** to successfully download the data.

I also found that when **piggyback::pb_download()** failed, a corrupted rds object was saved in cache.
That means in future downloads **piggyback::pb_download()** would not download as the corrupted file is found.
Because the download is very fast, I set _overwrite = TRUE_

Realated to this, I decided to to remove the if statement checking if hte tmp file exists.

In addition, please note that **gh::gh_token()** makes use of **gitcreds::gitcreds_get()** to retireve the githb_pat -> https://gh.r-lib.org/reference/gh_token.html
I tried to find there in the DockerFile you install the R deps but I was not lucky.
A modification in the Docker image must be done so that **gitcreds** R package is installed.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8cb235fb495a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.