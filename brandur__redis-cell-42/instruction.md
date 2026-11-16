# Issue

**Title:** Explicitly don't support zero rates

## Description

Be explicit on not supporting zero rates within the limiter by erroring
when the user tries to specify such a configuration.

A zero in the denominator (e.g. 10 actions over 0 seconds) is nonsense
and we shouldn't support that in any universe.

A zero the numerator (e.g. 0 actions over 10 seconds) makes a little
more sense to me in that a user may just be trying to specify a bucket
that never refills, but unfortunately the current GCRA system in use
does a very poor job of handling this -- it stores only a single number
in the data store and relies entirely on durations calculated from rates
to determine when things are allowed and when they're not. Multiplying
by zero means that we never calculate any sane durations, and therefore
the results produced aren't sane.

Therefore, I've also disallowed this for the time being since it doesn't
work. We could probably workaround this problem by either moving off of
GCRA or storing a special value that indicates "rate never expected to
refill", but it doesn't seem worth it for now.

.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bc9ec01f389d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.