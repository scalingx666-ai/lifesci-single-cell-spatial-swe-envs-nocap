# Issue

**Title:** [DEPENDABOT]: Bump typeguard from 2.11.1 to 2.12.0

## Description

Bumps [typeguard](https://github.com/agronholm/typeguard) from 2.11.1 to 2.12.0.
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/agronholm/typeguard/blob/master/docs/versionhistory.rst">typeguard's changelog</a>.</em></p>
<blockquote>
<h1>Version history</h1>
<p>This library adheres to <code>Semantic Versioning 2.0 &lt;https://semver.org/#semantic-versioning-200&gt;</code>_.</p>
<p><strong>2.12.0</strong> (2021-04-01)</p>
<ul>
<li>Added <code>@typeguard_ignore</code> decorator to exclude specific functions and classes from
runtime type checking (PR by Claudio Jolowicz)</li>
</ul>
<p><strong>2.11.1</strong> (2021-02-16)</p>
<ul>
<li>Fixed compatibility with Python 3.10</li>
</ul>
<p><strong>2.11.0</strong> (2021-02-13)</p>
<ul>
<li>Added support for type checking class properties (PR by Ethan Pronovost)</li>
<li>Fixed static type checking of <code>@typechecked</code> decorators (PR by Kenny Stauffer)</li>
<li>Fixed wrong error message when type check against a <code>bytes</code> declaration fails</li>
<li>Allowed <code>memoryview</code> objects to pass as <code>bytes</code> (like MyPy does)</li>
<li>Shortened tracebacks (PR by prescod)</li>
</ul>
<p><strong>2.10.0</strong> (2020-10-17)</p>
<ul>
<li>Added support for Python 3.9 (PR by Csergő Bálint)</li>
<li>Added support for nested <code>Literal</code></li>
<li>Added support for <code>TypedDict</code> inheritance (with some caveats; see the user guide on that for
details)</li>
<li>An appropriate <code>TypeError</code> is now raised when encountering an illegal <code>Literal</code> value</li>
<li>Fixed checking <code>NoReturn</code> on Python &lt; 3.8 when <code>typing_extensions</code> was not installed</li>
<li>Fixed import hook matching unwanted modules (PR by Wouter Bolsterlee)</li>
<li>Install the pytest plugin earlier in the test run to support more use cases
(PR by Wouter Bolsterlee)</li>
</ul>
<p><strong>2.9.1</strong> (2020-06-07)</p>
<ul>
<li>Fixed <code>ImportError</code> on Python &lt; 3.8 when <code>typing_extensions</code> was not installed</li>
</ul>
<p><strong>2.9.0</strong> (2020-06-06)</p>
<ul>
<li>Upped the minimum Python version from 3.5.2 to 3.5.3</li>
<li>Added support for <code>typing.NoReturn</code></li>
<li>Added full support for <code>typing_extensions</code> (now equivalent to support of the <code>typing</code> module)</li>
<li>Added the option of supplying <code>check_type()</code> with globals/locals for correct resolution of
forward references</li>
<li>Fixed erroneous <code>TypeError</code> when trying to check against non-runtime <code>typing.Protocol</code>
(skips the check for now until a proper compatibility check has been implemented)</li>
<li>Fixed forward references in <code>TypedDict</code> not being resolved</li>
<li>Fixed checking against recursive types</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>abcaa5d</code></a> Added release date</li>
<li><a href=""><code>c24f24d</code></a> Test against the latest py3.10 alpha</li>
<li><a href=""><code>a8d1c79</code></a> Added decorator to disable run time type checking (<a href="https://github-redirect.dependabot.com/agronholm/typeguard/issues/180">#180</a>)</li>
<li>See full diff in <a href="https://github.com/agronholm/typeguard/compare/2.11.1...2.12.0">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=typeguard&package-manager=pip&previous-version=2.11.1&new-version=2.12.0)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2730ce0fb6db`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.