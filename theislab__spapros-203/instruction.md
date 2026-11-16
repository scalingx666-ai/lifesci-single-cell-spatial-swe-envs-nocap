# Issue

**Title:** [DEPENDABOT]: Bump coverage from 6.1.2 to 6.2

## Description

Bumps [coverage](https://github.com/nedbat/coveragepy) from 6.1.2 to 6.2.
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/nedbat/coveragepy/blob/master/CHANGES.rst">coverage's changelog</a>.</em></p>
<blockquote>
<h2>Version 6.2 — 2021-11-26</h2>
<ul>
<li>
<p>Feature: Now the <code>--concurrency</code> setting can now have a list of values, so
that threads and another lightweight threading package can be measured
together, such as <code>--concurrency=gevent,thread</code>.  Closes <code>issue 1012</code>_ and
<code>issue 1082</code>_.</p>
</li>
<li>
<p>Fix: A module specified as the <code>source</code> setting is imported during startup,
before the user program imports it.  This could cause problems if the rest of
the program isn't ready yet.  For example, <code>issue 1203</code>_ describes a Django
setting that is accessed before settings have been configured.  Now the early
import is wrapped in a try/except so errors then don't stop execution.</p>
</li>
<li>
<p>Fix: A colon in a decorator expression would cause an exclusion to end too
early, preventing the exclusion of the decorated function. This is now fixed.</p>
</li>
<li>
<p>Fix: The HTML report now will not overwrite a .gitignore file that already
exists in the HTML output directory (follow-on for <code>issue 1244</code>_).</p>
</li>
<li>
<p>API: The exceptions raised by Coverage.py have been specialized, to provide
finer-grained catching of exceptions by third-party code.</p>
</li>
<li>
<p>API: Using <code>suffix=False</code> when constructing a Coverage object with
multiprocessing wouldn't suppress the data file suffix (<code>issue 989</code>_).  This
is now fixed.</p>
</li>
<li>
<p>Debug: The <code>coverage debug data</code> command will now sniff out combinable data
files, and report on all of them.</p>
</li>
<li>
<p>Debug: The <code>coverage debug</code> command used to accept a number of topics at a
time, and show all of them, though this was never documented.  This no longer
works, to allow for command-line options in the future.</p>
</li>
</ul>
<p>.. _issue 989: <a href="https://github-redirect.dependabot.com/nedbat/coveragepy/issues/989">nedbat/coveragepy#989</a>
.. _issue 1012: <a href="https://github-redirect.dependabot.com/nedbat/coveragepy/issues/1012">nedbat/coveragepy#1012</a>
.. _issue 1082: <a href="https://github-redirect.dependabot.com/nedbat/coveragepy/issues/1082">nedbat/coveragepy#1082</a>
.. _issue 1203: <a href="https://github-redirect.dependabot.com/nedbat/coveragepy/issues/1203">nedbat/coveragepy#1203</a></p>
<p>.. _changes_612:</p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>7a01882</code></a> docs: prep for 6.2</li>
<li><a href=""><code>7c128a6</code></a> docs: sample html report</li>
<li><a href=""><code>fbd3c71</code></a> docs: tweak the description of --concurrency</li>
<li><a href=""><code>fb7b0e5</code></a> docs: tweak the latest changelog entry</li>
<li><a href=""><code>9162ad0</code></a> test(refactor): avoid full commands to speed tests</li>
<li><a href=""><code>8ca306e</code></a> test(perf): shave a few seconds off the FailUnder tests</li>
<li><a href=""><code>c9d821d</code></a> feat: multiple --concurrency values. <a href="https://github-redirect.dependabot.com/nedbat/coveragepy/issues/1012">#1012</a> <a href="https://github-redirect.dependabot.com/nedbat/coveragepy/issues/1082">#1082</a></li>
<li><a href=""><code>97fdd55</code></a> build(docs): a target for running cog on the docs</li>
<li><a href=""><code>eff683c</code></a> test(fix): keep SourceIncludeOmitTest's from clobbering each other</li>
<li><a href=""><code>0865590</code></a> test(build): i've had the wrong -r character this whole time</li>
<li>Additional commits viewable in <a href="https://github.com/nedbat/coveragepy/compare/6.1.2...6.2">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=coverage&package-manager=pip&previous-version=6.1.2&new-version=6.2)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b9c46f0a14ef`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.