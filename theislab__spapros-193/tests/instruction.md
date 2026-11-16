# Issue

**Title:** [DEPENDABOT]: Bump typeguard from 2.13.0 to 2.13.2

## Description

Bumps [typeguard](https://github.com/agronholm/typeguard) from 2.13.0 to 2.13.2.
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/agronholm/typeguard/blob/master/docs/versionhistory.rst">typeguard's changelog</a>.</em></p>
<blockquote>
<h1>Version history</h1>
<p>This library adheres to <code>Semantic Versioning 2.0 &lt;https://semver.org/#semantic-versioning-200&gt;</code>_.</p>
<p><strong>2.13.2</strong> (2021-11-23)</p>
<ul>
<li>Fixed <code>typing_extensions</code> being imported unconditionally on Python &lt; 3.9
(bug introduced in 2.13.1)</li>
</ul>
<p><strong>2.13.1</strong> (2021-11-23)</p>
<ul>
<li>Fixed <code>@typechecked</code> replacing abstract properties with regular properties</li>
<li>Fixed any generic type subclassing <code>Dict</code> being mistakenly checked as <code>TypedDict</code> on
Python 3.10</li>
</ul>
<p><strong>2.13.0</strong> (2021-10-11)</p>
<ul>
<li>Added support for returning <code>NotImplemented</code> from binary magic methods (<code>__eq__()</code> et al)</li>
<li>Added support for checking union types (e.g. <code>Type[Union[X, Y]]</code>)</li>
<li>Fixed error message when a check against a <code>Literal</code> fails in a union on Python 3.10</li>
<li>Fixed <code>NewType</code> not being checked on Python 3.10</li>
<li>Fixed unwarranted warning when <code>@typechecked</code> is applied to a class that contains unannotated
properties</li>
<li>Fixed <code>TypeError</code> in the async generator wrapper due to changes in <code>__aiter__()</code> protocol</li>
<li>Fixed broken <code>TypeVar</code> checks – variance is now (correctly) disregarded, and only bound types
and constraints are checked against (but type variable resolution is not done)</li>
</ul>
<p><strong>2.12.1</strong> (2021-06-04)</p>
<ul>
<li>Fixed <code>AttributeError</code> when <code>__code__</code> is missing from the checked callable (PR by epenet)</li>
</ul>
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
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>4615f19</code></a> Fixed typing_extensions being imported unconditionally on Python &lt; 3.9</li>
<li><a href=""><code>2516f18</code></a> Added release date</li>
<li><a href=""><code>4ac7f28</code></a> Install coverage with toml support in GA test workflow</li>
<li><a href=""><code>0ec3dad</code></a> Fixed Dict-derived classes being mistaken for TypedDict on Python 3.10+</li>
<li><a href=""><code>8cfbe29</code></a> Fixed <a href="https://github.com/typechecked"><code>@​typechecked</code></a> replacing abstract properties with regular properties</li>
<li>See full diff in <a href="https://github.com/agronholm/typeguard/compare/2.13.0...2.13.2">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=typeguard&package-manager=pip&previous-version=2.13.0&new-version=2.13.2)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c0f56d6d8db3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.