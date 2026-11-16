# Issue

**Title:** Update tabulate requirement from <0.9 to <0.10

## Description

Updates the requirements on [tabulate](https://github.com/astanin/python-tabulate) to permit the latest version.
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/astanin/python-tabulate/blob/master/CHANGELOG">tabulate's changelog</a>.</em></p>
<blockquote>
<ul>
<li>0.9.0: Drop support for Python 2.7, 3.5, 3.6.
Migrate to pyproject.toml project layout (PEP 621).
New output formats: <code>asciidoc</code>, various <code>*grid</code> and <code>*outline</code> formats.
New output features: vertical row alignment, separating lines.
New input format: list of dataclasses (Python 3.7 or later).
Support infinite iterables as row indices.
Improve column width options.
Improve support for ANSI escape sequences and document the behavior.
Various bug fixes.</li>
<li>0.8.10: Python 3.10 support. Bug fixes. Column width parameter.</li>
<li>0.8.9: Bug fix. Revert support of decimal separators.</li>
<li>0.8.8: Python 3.9 support, 3.10 ready.
New formats: <code>unsafehtml</code>, <code>latex_longtable</code>, <code>fancy_outline</code>.
Support lists of UserDicts as input.
Support hyperlinks in terminal output.
Improve testing on systems with proxies.
Migrate to pytest.
Various bug fixes and improvements.</li>
<li>0.8.7: Bug fixes. New format: <code>pretty</code>. HTML escaping.</li>
<li>0.8.6: Bug fixes. Stop supporting Python 3.3, 3.4.</li>
<li>0.8.5: Fix broken Windows package. Minor documentation updates.</li>
<li>0.8.4: Bug fixes.</li>
<li>0.8.3: New formats: <code>github</code>. Custom column alignment. Bug fixes.</li>
<li>0.8.2: Bug fixes.</li>
<li>0.8.1: Multiline data in several output formats.
New <code>latex_raw</code> format.
Column-specific floating point formatting.
Python 3.5 &amp; 3.6 support. Drop support for Python 2.6, 3.2, 3.3 (should still work).</li>
<li>0.7.7: Identical to 0.7.6, resolving some PyPI issues.</li>
<li>0.7.6: Bug fixes. New table formats (<code>psql</code>, <code>jira</code>, <code>moinmoin</code>, <code>textile</code>).
Wide character support. Printing from database cursors.
Option to print row indices. Boolean columns. Ragged rows.
Option to disable number parsing.</li>
<li>0.7.5: Bug fixes. <code>--float</code> format option for the command line utility.</li>
<li>0.7.4: Bug fixes. <code>fancy_grid</code> and <code>html</code> formats. Command line utility.</li>
<li>0.7.3: Bug fixes. Python 3.4 support. Iterables of dicts. <code>latex_booktabs</code> format.</li>
<li>0.7.2: Python 3.2 support.</li>
<li>0.7.1: Bug fixes. <code>tsv</code> format. Column alignment can be disabled.</li>
<li>0.7:   <code>latex</code> tables. Printing lists of named tuples and NumPy
record arrays. Fix printing date and time values. Python &lt;= 2.6.4 is supported.</li>
<li>0.6:   <code>mediawiki</code> tables, bug fixes.</li>
<li>0.5.1: Fix README.rst formatting. Optimize (performance similar to 0.4.4).</li>
<li>0.5:   ANSI color sequences. Printing dicts of iterables and Pandas' dataframes.</li>
<li>0.4.4: Python 2.6 support.</li>
<li>0.4.3: Bug fix, None as a missing value.</li>
<li>0.4.2: Fix manifest file.</li>
<li>0.4.1: Update license and documentation.</li>
<li>0.4:   Unicode support, Python3 support, <code>rst</code> tables.</li>
<li>0.3:   Initial PyPI release. Table formats: <code>simple</code>, <code>plain</code>,
<code>grid</code>, <code>pipe</code>, and <code>orgtbl</code>.</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>bf58e37</code></a> version bump to 0.9.0, update README (Benchmark, Contributors), CHANGELOG</li>
<li><a href=""><code>fd0a34c</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/astanin/python-tabulate/issues/201">#201</a> from astanin/dev-pep621</li>
<li><a href=""><code>0a6554e</code></a> appveyor: upgrade setuptools before build (should fix UNKNOWN package name)</li>
<li><a href=""><code>d99d9ae</code></a> ignore ImportError when importing <strong>version</strong> number</li>
<li><a href=""><code>3e45eac</code></a> update appveyor.yml to use pyproject.toml instead of setup.py</li>
<li><a href=""><code>05e88d2</code></a> fix test_cli - change script path, do not import .version if <strong>init</strong>.py is r...</li>
<li><a href=""><code>4e2eeb1</code></a> update tox.ini - use a virtual environment to build a source dist from the so...</li>
<li><a href=""><code>6e37802</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/astanin/python-tabulate/issues/179">#179</a> from KOLANYCH-libs:pyproject.toml</li>
<li><a href=""><code>9172378</code></a> fix tests failing after PR#183 (remove 1 space from the expected values)</li>
<li><a href=""><code>930a943</code></a> reformat with black, fix flake warnings</li>
<li>Additional commits viewable in <a href="https://github.com/astanin/python-tabulate/compare/v0.3...v0.9.0">compare view</a></li>
</ul>
</details>
<br />

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e75c4a3e56ba`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.