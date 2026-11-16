# Issue

**Title:** Move seqeralabs/action-tower-launch to @v2 (v2.4.0)

## Description

This moves `seqeralabs/action-tower-launch` to the `@v2` tag, which now points to [v2.4.0](https://github.com/seqeralabs/action-tower-launch/releases/tag/v2.4.0), in the AWS test workflows.

Earlier versions only scrubbed the Seqera Platform access token from the uploaded `tower_action_*.log` debug artifact when the launch succeeded. v2.4.0 always removes it. It also stops running `tw launch` in verbose mode by default (from v2.3.0) and adds a link to the launched run to the job summary.

The next template sync makes the same change on `dev`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a663fe43aec4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.