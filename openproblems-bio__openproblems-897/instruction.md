# Issue

**Title:** Bump viash-io/viash-actions from 5 to 6

## Description

Bumps [viash-io/viash-actions](https://github.com/viash-io/viash-actions) from 5 to 6.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/viash-io/viash-actions/releases">viash-io/viash-actions's releases</a>.</em></p>
<blockquote>
<h2>v5.3.1</h2>
<h2>Bug fixes</h2>
<ul>
<li><code>project/detect-changed-components</code>: Fix components being listed more than once (PR <a href="">#29</a>).</li>
</ul>
<h2>v5.3.0</h2>
<h2>New functionality</h2>
<ul>
<li><code>project/detect-changed-components</code>: Detect changed components when a resource is a directory (PR <a href="">#28</a>).</li>
</ul>
<h2>v5.2.1</h2>
<h2>Bug Fixes</h2>
<ul>
<li><code>project/detect-changed-components</code>: fix changed components not being detected after updating <code>tj-actions/changed-files</code> (PR <a href="">#25</a>).</li>
</ul>
<h2>v5.2.0</h2>
<h2>Minor changes</h2>
<ul>
<li><code>project/detect-changed-components</code>: bump <code>tj-actions/changed-files</code> to <code>42.0.2</code> (PR <a href="">#24</a>)</li>
</ul>
<h2>v5.1.0</h2>
<h2>New functionality</h2>
<ul>
<li><code>pro/build-nextflow-schemas</code>: Add optional flag to allow dataset input for nf-tower (PR <a href="">#23</a>)</li>
</ul>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/viash-io/viash-actions/blob/main/CHANGELOG.md">viash-io/viash-actions's changelog</a>.</em></p>
<blockquote>
<h1>viash-actions v6.6.0</h1>
<h2>New functionality</h2>
<ul>
<li>Many actions: Add input <code>project_directory</code> to allow specifying the project directory (PR <a href="">#42</a>):
<ul>
<li><code>ns-build</code></li>
<li><code>ns-list</code></li>
<li><code>project/build-target</code></li>
<li><code>project/detect-changed-components</code></li>
<li><code>project/sync-and-cache</code></li>
</ul>
</li>
</ul>
<h2>Bug fixes</h2>
<ul>
<li>
<p><code>project/build-target</code>: Do not throw an error if there is no <code>.gitignore</code> in place (PR <a href="">#42</a>).</p>
</li>
<li>
<p><code>ns-build</code>, <code>ns-list</code>: If Viash throws an error, make sure that the error message gets printed (PR <a href="">#42</a>).</p>
</li>
<li>
<p><code>project/detect-changed-components</code>: Fix the action not listening to 'ci force' in commit messages (PR <a href="">#42</a>).</p>
</li>
</ul>
<h1>viash-actions v6.5.0</h1>
<h2>New functionality</h2>
<ul>
<li><code>build-nextflow-params</code> and <code>build-nextflow-schemas</code>: allow using viash versions starting from <code>0.9.0</code> (PR <a href="">#41</a>).</li>
</ul>
<h1>viash-actions v6.4.0</h1>
<h2>New functionality</h2>
<ul>
<li>
<p><code>.github/workflows/build.yaml</code>: Added a callable workflow for building Viash components (PR <a href="">#38</a>).</p>
</li>
<li>
<p><code>.github/workflows/test.yaml</code>: Added a callable workflow for testing Viash components (PR <a href="">#38</a>).</p>
</li>
</ul>
<h2>Minor changes</h2>
<ul>
<li><code>project/detect-changed-components</code>: Simplify separator handling of changed files array (PR <a href="">#40</a>).</li>
</ul>
<h2>Bug fixes</h2>
<ul>
<li><code>project/detect-changed-components</code>: Fix realpath not being able to resolve changed files (PR <a href="">#39</a>).</li>
</ul>
<h1>viash-actions v6.3.1</h1>
<h2>Bug fixes</h2>
<ul>
<li><code>project/sync-and-cache</code>: Skip caching steps in action if no test resources are found (PR <a href="">#37</a>).</li>
</ul>
<h1>viash-actions v6.3.0</h1>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>80d1c9f</code></a> fix publish dir</li>
<li><a href=""><code>a637a77</code></a> add project_directory to many actions (<a href="">#42</a>)</li>
<li><a href=""><code>b46ff03</code></a> Build nextflow schemas and params with viash 0.9 (<a href="">#41</a>)</li>
<li><a href=""><code>c113a65</code></a> Merge branch 'main' of github.com:viash-io/viash-actions</li>
<li><a href=""><code>ef56456</code></a> fix inputs</li>
<li><a href=""><code>04393de</code></a> Simplify separator handling of changed files array (<a href="">#40</a>)</li>
<li><a href=""><code>a47da7a</code></a> Add callable workflows (<a href="">#38</a>)</li>
<li><a href=""><code>3fcb79a</code></a> <code>project/detect-changed-components</code>: Fix realpath not being able to resolve c...</li>
<li><a href=""><code>7009f9c</code></a> fix refactoring error in <code>sync-and-cache</code></li>
<li><a href=""><code>f24f002</code></a> fix action</li>
<li>Additional commits viewable in <a href="https://github.com/viash-io/viash-actions/compare/v5...v6">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=viash-io/viash-actions&package-manager=github_actions&previous-version=5&new-version=6)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

Dependabot will resolve any conflicts with this PR as long as you don't alter it yourself. You can also trigger a rebase manually by commenting `@dependabot rebase`.

[//]: # (dependabot-automerge-start)
[//]: # (dependabot-automerge-end)

---

<details>
<summary>Dependabot commands and options</summary>
<br />

You can trigger Dependabot actions by commenting on this PR:
- `@dependabot rebase` will rebase this PR
- `@dependabot recreate` will recreate this PR, overwriting any edits that have been made to it
- `@dependabot merge` will merge this PR after your CI passes on it
- `@dependabot squash and merge` will squash and merge this PR after your CI passes on it
- `@dependabot cancel merge` will cancel a previously requested merge and block automerging
- `@dependabot reopen` will reopen this PR if it is closed
- `@dependabot close` will close this PR and stop Dependabot recreating it. You can achieve the same result by closing it manually
- `@dependabot show <dependency name> ignore conditions` will show all of the ignore conditions of the specified dependency
- `@dependabot ignore this major version` will close this PR and stop Dependabot creating any more for this major version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this minor version` will close this PR and stop Dependabot creating any more for this minor version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this dependency` will close this PR and stop Dependabot creating any more for this dependency (unless you reopen the PR or upgrade to it yourself)

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4ad08b91549d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.