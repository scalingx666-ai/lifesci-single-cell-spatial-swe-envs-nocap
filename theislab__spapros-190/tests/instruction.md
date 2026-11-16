# Issue

**Title:** [DEPENDABOT]: Bump coverage from 5.5 to 6.1.2

## Description

Bumps [coverage](https://github.com/nedbat/coveragepy) from 5.5 to 6.1.2.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/nedbat/coveragepy/releases">coverage's releases</a>.</em></p>
<blockquote>
<h2>coverage-5.6b1</h2>
<ul>
<li>Third-party packages are now ignored in coverage reporting. This solves a few problems:
<ul>
<li>Coverage will no longer report about other people’s code (<a href="https://github-redirect.dependabot.com/nedbat/coveragepy/issues/876">issue 876</a>). This is true even when using <code>--source=.</code> with a venv in the current directory.</li>
<li>Coverage will no longer generate “Already imported a file that will be measured” warnings about coverage itself (<a href="https://github-redirect.dependabot.com/nedbat/coveragepy/issues/905">issue 905</a>).</li>
</ul>
</li>
<li>The HTML report uses j/k to move up and down among the highlighted chunks of code. They used to highlight the current chunk, but 5.0 broke that behavior. Now the highlighting is working again.</li>
<li>The JSON report now includes <code>percent_covered_display</code>, a string with the total percentage, rounded to the same number of decimal places as the other reports’ totals.</li>
</ul>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/nedbat/coveragepy/blob/master/CHANGES.rst">coverage's changelog</a>.</em></p>
<blockquote>
<h2>Version 6.1.2 — 2021-11-10</h2>
<ul>
<li>
<p>Python 3.11 is supported (tested with 3.11.0a2).  One still-open issue has to
do with <code>exits through with-statements &lt;issue 1270_&gt;</code>_.</p>
</li>
<li>
<p>Fix: When remapping file paths through the <code>[paths]</code> setting while
combining, the <code>[run] relative_files</code> setting was ignored, resulting in
absolute paths for remapped file names (<code>issue 1147</code>_).  This is now fixed.</p>
</li>
<li>
<p>Fix: Complex conditionals over excluded lines could have incorrectly reported
a missing branch (<code>issue 1271</code>_). This is now fixed.</p>
</li>
<li>
<p>Fix: More exceptions are now handled when trying to parse source files for
reporting.  Problems that used to terminate coverage.py can now be handled
with <code>[report] ignore_errors</code>.  This helps with plugins failing to read
files (<code>django_coverage_plugin issue 78</code>_).</p>
</li>
<li>
<p>Fix: Removed another vestige of jQuery from the source tarball
(<code>issue 840</code>_).</p>
</li>
<li>
<p>Fix: Added a default value for a new-to-6.x argument of an internal class.
This unsupported class is being used by coveralls (<code>issue 1273</code>_). Although
I'd rather not &quot;fix&quot; unsupported interfaces, it's actually nicer with a
default value.</p>
</li>
</ul>
<p>.. _django_coverage_plugin issue 78: <a href="https://github-redirect.dependabot.com/nedbat/django_coverage_plugin/issues/78">nedbat/django_coverage_plugin#78</a>
.. _issue 1147: <a href="https://github-redirect.dependabot.com/nedbat/coveragepy/issues/1147">nedbat/coveragepy#1147</a>
.. _issue 1270: <a href="https://github-redirect.dependabot.com/nedbat/coveragepy/issues/1270">nedbat/coveragepy#1270</a>
.. _issue 1271: <a href="https://github-redirect.dependabot.com/nedbat/coveragepy/issues/1271">nedbat/coveragepy#1271</a>
.. _issue 1273: <a href="https://github-redirect.dependabot.com/nedbat/coveragepy/issues/1273">nedbat/coveragepy#1273</a></p>
<p>.. _changes_611:</p>
<h2>Version 6.1.1 — 2021-10-31</h2>
<ul>
<li>
<p>Fix: The sticky header on the HTML report didn't work unless you had branch
coverage enabled. This is now fixed: the sticky header works for everyone.
(Do people still use coverage without branch measurement!? j/k)</p>
</li>
<li>
<p>Fix: When using explicitly declared namespace packages, the &quot;already imported
a file that will be measured&quot; warning would be issued (<code>issue 888</code>_).  This
is now fixed.</p>
</li>
</ul>
<p>.. _issue 888: <a href="https://github-redirect.dependabot.com/nedbat/coveragepy/issues/888">nedbat/coveragepy#888</a></p>
<p>.. _changes_61:</p>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>2078c2f</code></a> docs: sample HTML report for 6.1.2</li>
<li><a href=""><code>e403155</code></a> docs: update the man page with --quiet</li>
<li><a href=""><code>27426bf</code></a> build: prep for 6.1.2</li>
<li><a href=""><code>9765493</code></a> fix: CPython 3.11 support. <a href="https://github-redirect.dependabot.com/nedbat/coveragepy/issues/1241">#1241</a></li>
<li><a href=""><code>dfa9774</code></a> style: make these macros more bullet-proof</li>
<li><a href=""><code>f3a70c9</code></a> fix: warn about more source file problems</li>
<li><a href=""><code>23f567f</code></a> build: use this setup.py command because it shows compiler errors that might ...</li>
<li><a href=""><code>049844a</code></a> docs: fix typo in source docs (<a href="https://github-redirect.dependabot.com/nedbat/coveragepy/issues/1275">#1275</a>)</li>
<li><a href=""><code>d58e136</code></a> build: one pypy wheel to rule them all</li>
<li><a href=""><code>2afc907</code></a> refactor(test): convert eight tests to one parametrized test</li>
<li>Additional commits viewable in <a href="https://github.com/nedbat/coveragepy/compare/coverage-5.5...6.1.2">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=coverage&package-manager=pip&previous-version=5.5&new-version=6.1.2)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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