# Issue

**Title:** added install_name_tool conditional in src/Makevars

## Description

(I'm not sure if you prefer PRs into master---we could use another branch)

Currently, this is my best solution for Mac OS users experiencing this issue:



R data.table does something similar, so it feels like a reasonable approach:
https://github.com/Rdatatable/data.table/blob/master/src/Makevars.in#L6

Works for me. 

************************

My current set-up:
R version 4.0.0 (not installed via brew)
Mac OS 10.15.4 Catalina
Installed LLVM and gcc via brew, i.e. `brew install llvm gcc`
and I included the following in my `~/.zshrc`:
```
export PATH="/usr/local/opt/llvm/bin:$PATH"
export LDFLAGS="-L/usr/local/opt/llvm/lib"
export CPPFLAGS="-I/usr/local/opt/llvm/include"

```
clang:
```
clang -v
clang version 10.0.0 
Target: x86_64-apple-darwin19.4.0
Thread model: posix
InstalledDir: /usr/local/opt/llvm/bin
```

Here is my `.R/Makevars`, explicitly settting the `-fopenmp` flags (which could be a problem for some packages installed from source...look into this):
```
XCBASE:=$(shell xcrun --show-sdk-path)
LLVMBASE:=$(shell brew --prefix llvm)
GCCBASE:=$(shell brew --prefix gcc)
GETTEXT:=$(shell brew --prefix gettext)

CC=$(LLVMBASE)/bin/clang -fopenmp
CXX=$(LLVMBASE)/bin/clang++ -fopenmp
CXX11=$(LLVMBASE)/bin/clang++ -fopenmp
CXX14=$(LLVMBASE)/bin/clang++ -fopenmp
CXX17=$(LLVMBASE)/bin/clang++ -fopenmp
CXX1X=$(LLVMBASE)/bin/clang++ -fopenmp

CPPFLAGS=-isystem "$(LLVMBASE)/include" -isysroot "$(XCBASE)"
LDFLAGS=-L"$(LLVMBASE)/lib" -L"$(GETTEXT)/lib" --sysroot="$(XCBASE)"

FC=$(GCCBASE)/bin/gfortran -fopenmp
F77=$(GCCBASE)/bin/gfortran -fopenmp
FLIBS=-L$(GCCBASE)/lib/gcc/9/ -lm
```

With the above, I was successfully able to install conos (and pagoda2).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `abb6372a4f38`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.