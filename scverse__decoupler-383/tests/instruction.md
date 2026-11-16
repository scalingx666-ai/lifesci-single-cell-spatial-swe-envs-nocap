# Issue

**Title:** Prevent permutation p-values of 0 in mt.gsea

## Description

<html>
<body>
<p>This follows up on #373, which made the permutation p-values of <code>mt.waggr</code> never 0. <code>mt.gsea</code> has the same issue in <code>_nesrank</code>: when no permuted score reaches the observed one, the p-value is</p>
<pre><code class="language-python">pval = (null[pos_null_msk] &gt;= es).sum() / pos_null_sum   # = 0
</code></pre>
<p>With <em>P</em> permutations, a p-value of 0 is not supported by the data, since the observed score could itself have been one of the permutations. In practice, all strongly enriched sets end up with the same p-value of exactly 0. They cannot be ranked against each other, their adjusted p-values stay 0, and −log10(padj) is infinite.</p>
<p>For example, with 20 observations of increasing enrichment for one set of 30 genes (1,000 permutations):</p>

  | main | this PR
-- | -- | --
observations with padj = 0 | 17 of 20 | 0 of 20
range of padj for these 17 | 0 | 0.0016–0.0021

<p><strong>Change</strong></p>
<p>The observed score is counted as one of the permutations (Phipson &amp; Smyth, 2010), separately for each sign, as in fgsea:</p>
<pre><code class="language-python">pval = ((null[pos_null_msk] &gt;= es).sum() + 1) / (pos_null_sum + 1)   # and the analogue for ES &lt; 0
</code></pre>
<p>The smallest possible p-value is therefore about <code>1 / (times + 1)</code>. ES and NES are unchanged, and the reference is the <code>phipson2010</code> entry already in <code>references.bib</code>. The docstring formula now describes the sign-specific test, and the changelog has an entry under Unreleased.</p>
<p><strong>Verification</strong></p>
<ul>
<li>On a ranked list of 1,000 genes, ES from <code>mt.gsea</code> are identical to <code>gseapy.prerank</code> (<code>weight=1</code>), and NES agree within permutation noise. Only the p-values change.</li>
<li><code>test_nesrank</code> now checks the p-value of the hand-worked permutation example (3/7). <code>test_gsea_pvalues_not_zero</code> checks that a strongly enriched set gets exactly <code>1 / (P₊ + 1)</code> and not 0. Both fail on <code>main</code> and pass with this change.</li>
<li><code>tests/mt</code> passes (99 tests).</li>
</ul></body></html><!--EndFragment-->
</body>
</html>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f78f5be6f3f3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.