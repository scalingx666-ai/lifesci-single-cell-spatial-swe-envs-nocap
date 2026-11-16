# Issue

**Title:** Unittest

## Description

Hi Catalina,

I added a unit case using testthat (looks promising and new). So now, if you are in the folder of your package and want to test. you can do:

``` R
devtools::test()
```

and it will run whatever tests you have in folder tests. Please, change whatever you want in that. I gave some descriptions for the tests that might be just bad descriptions of what is actually being tested =P

I also added a file .gitattributes to the root of the project. This should not come with BASiCS as a release package but it is used by whoever develops BASiCS. It is useful to guarantee the same type of newlines (Windows uses one type and Linux/OSX another one).

Also as a side comment, to avoid multiple line changes in merging it is a good idea to not have trailing whitespaces (i.e., whitespaces at end of lines, which don't do nothing but makes lines differ). To do that, most of editors has an option to automatically remove those whitespaces when a file is saved (since it is so easy to add them accidentally).

Danilo

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a798c3b0f9d7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.