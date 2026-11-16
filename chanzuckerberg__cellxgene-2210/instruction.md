# Issue

**Title:** feat[sastisfaction]: adding non-blocking security linting to cellxgene

## Description

### Summary
#### Description
This PR introduces a security tool that is being worked on by @edulop91, @jacobrheath, and the [prodsec team](https://wiki.czi.team/display/TECH/Product+Security).
The tool combines reviewdog and semgrep to make educational security comments about dangerous functions and potentially bad code patterns relating to security.
The main priority of the tool is not to be annoying or blocking, but to bring security learning closer to the development lifecycle. We will do our best to make this tool non-blocking.

#### Notes
- This is a non-blocking tool, and purely for educational purposes. We encourage you to read any comments that are produced and reach out to the prodsec team if you'd like to learn more information.
- If you see a mistake (a comment was created that seems to not be relevant to the code or something similar), let us know! We want to make this as high-signal and non-noisy as possible.
- The tool only runs semgrep rules on the diff from the PR.
- We only have a short number of rules that run right now, but we plan to bring in more over time.
- We have no Python rules at this time, but plan to create some in the future, so expect no comments until those rules are made.

Comments will look like this:
![image](https://user-images.githubusercontent.com/3452666/118001691-f705c380-b314-11eb-9f67-23de460ba38a.png)

- Each comment will have a short description, as well as links to more educational material.
- The addition of new rules or changes to the tool do not require modifications to this codebase.
- If you have rule suggestions or patterns you'd like to prevent in your app please let us know!
- We collect some data around which rules are getting triggered and what action they prompt. This will help us tune our rules, avoid false positives, and hopefully make this a high-quality integration. 

#### FAQs
- *How does this compare with other static analysis tools?*
We opted to use `semgrep` for now (with room to grow into possible different tools) since it gives us the chance to write rules that are not necessarily framework/language specific. We can share rules with other projects at CZI and write rules for various languages with the same format.

- *Will this block my work?*
Our primary goal with this tool is to bring "Security Awareness" earlier into to the development lifecycle. Our hope is this project will help us highlight certain patterns we hope to avoid by tying in external documentation, example code snippets, etc directly into the development cycle. We've spent some time making sure tests run quickly, they are non-blocking, and we collect metrics to make sure we drive down false positives. Data we collect includes the rule that was triggered, the line that triggered it, the repo/SHA/branch, and any corresponding comments/responses in the GitHub PR review.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1ea2b7fe806d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.