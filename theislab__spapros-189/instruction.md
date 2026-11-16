# Issue

**Title:** [DEPENDABOT]: Bump actions/setup-python from 2.2.2 to 2.3.0

## Description

Bumps [actions/setup-python](https://github.com/actions/setup-python) from 2.2.2 to 2.3.0.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/actions/setup-python/releases">actions/setup-python's releases</a>.</em></p>
<blockquote>
<h2>Support caching dependencies</h2>
<p>This release introduces dependency caching support (<a href="https://github-redirect.dependabot.com/actions/setup-python/pull/266">actions/setup-python#266</a>)</p>
<h2>Caching dependencies.</h2>
<p>The action has a built-in functionality for caching and restoring pip/pipenv dependencies. The <code>cache</code> input is optional, and caching is turned off by default.</p>
<p>Besides, this release introduces dependency caching support for mono repos and repositories with complex structure.</p>
<p>By default, the action searches for the dependency file (requirements.txt for pip or Pipfile.lock for pipenv) in the whole repository. Use the <code>cache-dependency-path</code> input for cases when you want to override current behaviour and use different file for hash generation (for example requirements-dev.txt). This input supports wildcards or a list of file names for caching multiple dependencies.</p>
<h3>Caching pip dependencies:</h3>
<pre><code>steps:
- uses: actions/checkout@v2
- uses: actions/setup-python@v2
  with:
    python-version: '3.9'
    cache: 'pip'
- run: pip install -r requirements.txt
- run: pip test
</code></pre>
<h3>Caching pipenv dependencies:</h3>
<pre><code>steps:
- uses: actions/checkout@v2
- name: Install pipenv
  run: pipx install pipenv
- uses: actions/setup-python@v2
  with:
    python-version: '3.9'
    cache: 'pipenv'
- run: pipenv install
- run: pipenv test
</code></pre>
<h3>Change dependency file:</h3>
<pre><code>steps:
- uses: actions/checkout@v2
- uses: actions/setup-python@v2
  with:
    python-version: '3.9'
    cache: 'pip'
    cache-dependency-path: '**/requirements-dev.txt'
- run: pip install -r subdirectory/requirements-dev.txt
- run: pip test
</code></pre>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>0066b88</code></a> Add a workflow to release a new version of the action (<a href="https://github-redirect.dependabot.com/actions/setup-python/issues/274">#274</a>)</li>
<li><a href=""><code>280924f</code></a> Implementation of python's caching (<a href="https://github-redirect.dependabot.com/actions/setup-python/issues/266">#266</a>)</li>
<li><a href=""><code>52636cf</code></a> Fix consistency in README (<a href="https://github-redirect.dependabot.com/actions/setup-python/issues/250">#250</a>)</li>
<li><a href=""><code>ca5c590</code></a> Update version for setup-python in package.json (<a href="https://github-redirect.dependabot.com/actions/setup-python/issues/264">#264</a>)</li>
<li><a href=""><code>feeaa3b</code></a> Add issue and pull request templates (<a href="https://github-redirect.dependabot.com/actions/setup-python/issues/258">#258</a>)</li>
<li><a href=""><code>002b1e4</code></a> Change python version for pypy in workflow files (<a href="https://github-redirect.dependabot.com/actions/setup-python/issues/259">#259</a>)</li>
<li><a href=""><code>d12543a</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/actions/setup-python/issues/252">#252</a> from dmitry-shibanov/v-dmshib/update-dependencies</li>
<li><a href=""><code>4aa563b</code></a> update dependencies</li>
<li><a href=""><code>70e2063</code></a> Update test-python.yml (<a href="https://github-redirect.dependabot.com/actions/setup-python/issues/246">#246</a>)</li>
<li><a href=""><code>2d803e7</code></a> Create check-dist.yml (<a href="https://github-redirect.dependabot.com/actions/setup-python/issues/236">#236</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/actions/setup-python/compare/v2.2.2...v2.3.0">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=actions/setup-python&package-manager=github_actions&previous-version=2.2.2&new-version=2.3.0)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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
- `@dependabot ignore this major version` will close this PR and stop Dependabot creating any more for this major version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this minor version` will close this PR and stop Dependabot creating any more for this minor version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this dependency` will close this PR and stop Dependabot creating any more for this dependency (unless you reopen the PR or upgrade to it yourself)

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fff28d2e8326`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.