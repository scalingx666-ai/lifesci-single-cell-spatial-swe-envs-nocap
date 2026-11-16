# Issue

**Title:** Fix 'dir' handling for cloud file systems

## Description

<!--
# nf-core/spatialvi pull request

Many thanks for contributing to nf-core/spatialvi!

Please fill in the appropriate checklist below (delete whatever is not relevant).
These are the most common things requested on pull requests (PRs).

Remember that PRs should be made against the dev branch, unless you're preparing a pipeline release.

Learn more about contributing: [CONTRIBUTING.md](https://github.com/nf-core/spatialvi/tree/main/.github/CONTRIBUTING.md)
-->

The current code has a big problem, in that [here](https://github.com/nf-core/spatialvi/blob/b20e4c7c05289af3da01209bb2da42a07a4e91b6/subworkflows/local/input_check/main.nf#L42) it puts a file object from UNTAR through a map, which flattens it into a string. A Path object representing an S3 bucket path like `s3://foo/bar` becomes just `/foo/bar`.

That causes problems when you get to [here](https://github.com/nf-core/spatialvi/blob/b20e4c7c05289af3da01209bb2da42a07a4e91b6/subworkflows/local/input_check/main.nf#L120), because the flattened path string (see above) looks like, but isn't, a local file path, so the FASTQ files are not found.

This PR addresses the issue by letting the Path object from UNTAR remain a path, and by making a path object (using `file`) from any actual directory paths in the sample sheet). Then we don't need the `file()` call in the Groovy function, and we can derive fastq files by querying the object.

Local paths DO flatten to something valid, which is why it worked in those contexts.

Also snuck a tower.yml in.

## PR checklist

- [ ] This comment contains a description of changes (with reason).
- [ ] If you've fixed a bug or added code that should be tested, add tests!
- [ ] If you've added a new tool - have you followed the pipeline conventions in the [contribution docs](https://github.com/nf-core/spatialvi/tree/main/.github/CONTRIBUTING.md)
- [ ] If necessary, also make a PR on the nf-core/spatialvi _branch_ on the [nf-core/test-datasets](https://github.com/nf-core/test-datasets) repository.
- [ ] Make sure your code lints (`nf-core pipelines lint`).
- [ ] Ensure the test suite passes (`nextflow run . -profile test,docker --outdir <OUTDIR>`).
- [ ] Check for unexpected warnings in debug mode (`nextflow run . -profile debug,test,docker --outdir <OUTDIR>`).
- [ ] Usage Documentation in `docs/usage.md` is updated.
- [ ] Output Documentation in `docs/output.md` is updated.
- [ ] `CHANGELOG.md` is updated.
- [ ] `README.md` is updated (including new tool citations and authors/contributors).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b20e4c7c0528`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.