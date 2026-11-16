# Issue

**Title:** fix the issue of some spatial packages which will retire

## Description

余老师，我查了下主要是`SeuratObject`这个包依赖`sp`包，而`sp`又跟`rgdal`, `rgeos`这些包相关，所以才会出现那个提示信息。根据您提供的那个文档是说，可以考虑把相关包移到`Suggests`里。

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f580862887f3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.