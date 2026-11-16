# Issue

**Title:** RNA velocity integration

## Description

Hi! I tried my best at implementing velocity estimation into conos. To my understanding the biggest challenge was merging the velocity files and using a conos object instead of a pagoda object. The function `VelocityInfoConos` does exactly that. There are also two helper functions since we are now working on lists of samples. 

I tried to leave enough comments in the code to make everything clear, please ask if it's not. I also wrote a tutorial section in the README file. I know the use case is quite specific, but it should hopefully be helpful to some people or at least get them started. 

In terms of implementation I'm especially not sure of the PCA calculation step. To save on time and code I used existing conos function, so I hope everything is correct. I would greatly appreciate if someone more experienced could look into that part and maybe even try it on their data. I've run it at all on my data (two sets of samples) and the results made sense (at least they agreed with what I saw when analysing the samples separately). But you never know.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `dc80e3b291f0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.