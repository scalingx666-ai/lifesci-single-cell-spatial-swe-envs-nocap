# Issue

**Title:** Fix clinical trial sample sizes for unequal allocation

## Description

With --allocation set to anything other than 1, the clinical-trial-protocol
skill's sample_size_calculator.py returned the wrong group sizes. It asked
for too few participants at ratios above about 1.6:1 for continuous
endpoints and above 1:1 for binary endpoints, and for too many at ratios
below 1:1 (at 1:2, about six times too many for continuous endpoints and
about twice too many for binary ones). The default 1:1 group sizes were
correct, and the commands written in the skill never pass --allocation.

Examples, at two-sided alpha 0.05 and 80% target power, before dropout:

```
  Difference of 1 standard deviation, 2:1
    before: 18 + 9 = 27, fewer than the 32 needed at 1:1; real power 65%
    now:    24 + 12 = 36; real power 78% (see the second known limit)
  Response rate 60% vs 75%, 2:1
    before: 110 + 55 = 165; real power 51%
    now:    224 + 112 = 336; real power 80%
```

What changes:

- Both endpoint types now size the control group with the standard
  formula, round it up, and multiply by the ratio to get the treatment
  group. The main result and both sensitivity rows use the same code.
- At 1:1 the only number that moves is the binary "effect size reduced
  by 10%" sensitivity row, which now pools the rates using the reduced
  treatment rate (60% vs 75%: 378 becomes 380).
- One-line errors replace crashes or meaningless results when the
  allocation ratio is not a positive number, the effect size is zero,
  the standard deviation is not positive, p1 equals p2, or --alpha,
  --power or --dropout is out of range (--dropout 15 used to give
  negative enrollment numbers).
- The calculator refuses non-inferiority designs under either spelling,
  with a one-line error and exit 1, so a run that reaches it still takes
  the skill's similar-trials fallback.
- The skill's instructions now say not to run the calculator for
  non-inferiority designs: tell the user why, and use enrollment numbers
  from similar trials with the existing disclaimer instead. That is
  where the written instructions already led, because their commands
  passed "noninferiority" and the script rejected it. They also say to
  tell the user when the protocol's study design section and the user's
  answer name different designs.
- When the calculation fails or is skipped, the instructions now also
  say not to use a result file left from an earlier run, and to report
  the calculation as not performed.
- SKILL.md no longer calls the calculator "validated" or "accurate".
  Unit tests are added next to it, with expected values from published
  examples and from the standard formulas. Run them with:
  python3 clinical-trial-protocol-skill/scripts/test_sample_size_calculator.py

Known limits, not changed here:

- Non-inferiority has no margin option, so the script refuses those
  designs rather than sizing them.
- Continuous sizes use the normal approximation, so they come out one or
  two participants per group short of an exact t-test calculation (at a
  1 SD difference, 16 per group gives 78% power, not 80%; at 2 SD, 4 per
  group gives 66%).
- For continuous endpoints, a ratio and its inverse (3:1 and 1:3) can
  differ by a few participants, because the control group is the one
  rounded first.
- The v1.1.0 and v1.1.1 tags contain the old script.

## Test plan

The 10 unit tests pass. Ran the old and new scripts side by side at 1:1, 2:1 and 1:2, and the group sizes match the examples above. Invalid allocation, effect size, standard deviation and p1 = p2 each give a one-line error with exit 1, as do either non-inferiority spelling and out-of-range --alpha, --power and --dropout. The published sources cited in the tests and the real-power figures were not independently rechecked, and the updated skill instructions were not run end to end.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6aab04111074`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.