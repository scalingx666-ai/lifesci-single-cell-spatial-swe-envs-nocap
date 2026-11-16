# Issue

**Title:** Copy Clinical Trial Protocol Skill

## Description

Copy the clinical trial protocol generation skill which supports:
- Medical devices (IDE pathway) and drugs (IND pathway)
- Modular waypoint-based architecture
- Interactive sample size calculation
- Research-driven recommendations via ClinicalTrials.gov

Slack: https://anthropic.slack.com/archives/C09TJL9AY07/p1767997618669009

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `90f681f3723a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.