# Issue

**Title:** fix(pl): slopeplot color_by keeps a subject-constant column, + grouped paired mode; boxplot show_points

## Description

Three independent slopeplot / boxplot improvements.

## slopeplot: `color_by` keeps a subject-constant column
The wide pivot reduced the long frame to `y` indexed by subject on `x` alone, and `resolve_columns` only kept the columns it was handed — so a metadata column (e.g. a healthy/disease label) never reached `color_by` validation and colouring by it raised even though it was a real column. It is now pulled through the pivot: a subject-constant column colours one line per subject; a column that varies within a subject is a clear error; an unknown name still lists what is available.

## slopeplot: grouped paired mode via `group=`
slopeplot connected one subject across every `x` level in a single cluster; it could not express "two conditions within each of several groups" (healthy vs disease within each site), the layout where subjects are paired *inside* an outer grouping.

`group=` adds it: when given, `x` holds exactly two conditions, `subject` pairs them, and each `group` level becomes its own paired cluster along the axis — the two conditions offset either side of the group centre, one line per subject coloured by direction, x-ticks labelled by group, legend keyed to the two conditions. `group=None` leaves the existing single-cluster path untouched.

Refuses input that cannot express the layout: more than two `x` conditions, or a subject that straddles two groups.

```python
ov.pl.slopeplot(df, x="label", y="value", subject="pair", group="site",
                order=["healthy", "disease"])
```

## boxplot: `show_points`
`boxplot` always overlaid the jittered points; `show_points=False` draws the boxes alone.

## Tests
`tests/pl/test_slopeplot_colorby.py` covers the subject-constant column, the grouped layout (one line per pair, group ticks, endpoint offsets, two-condition and single-group refusals), and boxplot point toggling.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0262a5db41ac`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.