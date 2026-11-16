# Issue

**Title:** CVE-2007-4559 Patch

## Description

# Patching CVE-2007-4559

Hi, we are security researchers from the Advanced Research Center at [Trellix](https://www.trellix.com). We have began a campaign to patch a widespread bug named CVE-2007-4559. CVE-2007-4559 is a 15 year old bug in the Python tarfile package. By using extract() or extractall() on a tarfile object without sanitizing input, a maliciously crafted .tar file could perform a directory path traversal attack. We found at least one unsantized extractall() in your codebase and are providing a patch for you via pull request. The patch essentially checks to see if all tarfile members will be extracted safely and throws an exception otherwise. We encourage you to use this patch or your own solution to secure against CVE-2007-4559. Further technical information about the vulnerability can be found in this [blog](https://www.trellix.com/en-us/about/newsroom/stories/research/tarfile-exploiting-the-world.html).

If you have further questions you may contact us through this projects lead researcher [Kasimir Schulz](mailto:kasimir.schulz@trellix.com).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7aabc4b0a6f8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.