# Issue

**Title:** cmake/TestSalmonQuasi.cmake: more verbose test failure messages.

## Description

Greetings,

When trying to debug test failure, I ended up with an incomplete error messages which turned out to stem from a typo in the variable name, so I took the liberty to make the whole message a bit more verbose to help with the present and future debugging.

I thought you might be interested.
Have a nice day,  :)
Étienne.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f66d7e8ce0f2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.