# Issue

**Title:** fixed refs; hide ecosystems printing

## Description

- Method of the year references weren't showing correctly (dashes instead of author field). Per Nature Methods website, Method of the year pieces do not have an author field, so removing them should be fine and fixes the rendering.
- "bkd-ecosystems" is printing lots of unwanted stuff (not seeing this when rendering locally, likely due to something being cashed internally); see [here](https://lmweber.org/OSTA/pages/bkg-ecosystem.html#number-of-packages); this should be hidden now.

Current:
<img width="293" height="124" alt="image" src="https://github.com/user-attachments/assets/51921cc1-8164-452d-a64e-98b24205e805" />
Now:
<img width="354" height="135" alt="image" src="https://github.com/user-attachments/assets/f5e874bc-7010-463f-b7f0-9520aedad1ca" />

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e00ec597d72f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.