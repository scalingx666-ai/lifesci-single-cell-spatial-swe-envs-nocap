# Issue

**Title:** Fix two-sided permutation p-values in mt.waggr

## Description

<html>
<body>
<!--StartFragment--><html><head></head><body><h2><span>Problem</span></h2><p><span>In </span><code><span>mt/_waggr.py</span></code><span>, </span><code><span>_perm</span></code><span> counts how often a permuted score is at least as extreme as the observed score in absolute value:</span></p><pre><code><span>pvals += np.abs(null_dst[:, :, i]) &gt; np.abs(es)</span></code></pre><p><span>This already gives a two-sided count. However, the code then treats it as a one-sided count and folds it:</span></p><pre><code><span>pvals = pvals / times
pvals = np.where(pvals &gt;= 0.5, 1 - pvals, pvals)
pvals = pvals * 2</span></code></pre><p><span>This produces incorrect p-values for scores close to zero. When the observed score is smaller in magnitude than most permuted scores, the count approaches </span><code><span>times</span></code><span>. The folding step then turns that large count into a very small p-value, making a result with almost no enrichment appear as significant as a strongly enriched one.</span></p><p><span>The following example illustrates the problem:</span></p>
Set | wmean score | p-value on main (times=1000) | With this PR
-- | -- | -- | --
Random set | 0.32 | 0.898 | 0.551
Score exactly 0 | 0.00 | 0.002 | 1.000
Strongly enriched set | 2.96 | 0.002 | 0.001

<p><span>Under the null hypothesis, the folded p-values can still appear uniformly distributed. This likely explains why the issue went unnoticed: the overall false-positive rate remains close to the expected 5%, even though the individual results can be misleading.</span></p><p><span>In a simulation with pure noise (50 observations, 2,000 features, 100 random sets of 25 signed targets, and 1,000 permutations), 49% of the results with p &lt; 0.05 had |NES| &lt; 0.1. For results with |NES| &lt; 0.05, the median p-value was 0.048. The same issue affects </span><code><span>run_wsum</span></code><span> and </span><code><span>run_wmean</span></code><span> in </span><code><span>decoupler&lt;2</span></code><span>.</span></p><h2><span>Changes</span></h2><ul><li><p><span>Calculate two-sided p-values directly using </span><code><span>(1 + #{|ES_rand| &gt;= |ES|}) / (1 + times)</span></code><span>, following Phipson &amp; Smyth (2010). Including the observed score prevents p-values from being zero, and counting ties as at least as extreme handles equal scores correctly. This also fixes the behavior of custom functions that return a constant value, which previously received </span><code><span>p = 2 / times</span></code><span>.</span></p></li><li><p><span>Update the docstring to describe the two-sided test and add the reference to </span><code><span>references.bib</span></code><span>.</span></p></li><li><p><span>Add an entry to the changelog under Unreleased.</span></p></li><li><p><span>Leave </span><code><span>NES</span></code><span> unchanged.</span></p></li></ul><h2><span>Verification</span></h2><ul><li><p><span>Add </span><code><span>test_waggr_pvalues</span></code><span> to check that a score of exactly zero receives p &gt; 0.5, a strongly enriched set receives the minimum p-value of </span><code><span>1 / (times + 1)</span></code><span>, and a constant score receives p = 1. The test fails on </span><code><span>main</span></code><span>, where the zero score receives p = 0.002, and passes with this change.</span></p></li><li><p><span>Repeat the noise simulation described above. The proportion of p-values below 0.05 remains 5.1% before and after the change. After the fix, none of these significant results have |NES| &lt; 0.1, and 96% have |NES| &gt; 1.96.</span></p></li><li><p><span>Run </span><code><span>tests/mt</span></code><span>: all 98 tests pass.</span></p></li></ul></body></html><!--EndFragment-->
</body>
</html>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3132edcb5845`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.