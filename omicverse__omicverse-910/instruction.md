# Issue

**Title:** fix(flow): make the Gating-ML we write actually Gating-ML

## Description

`ov.flow.write_gatingml` produces documents that round-trip through `read_gatingml` perfectly and that **no other tool will accept**. FlowKit validates against the ISAC XSD before it parses, so the whole file comes back as one opaque line:

```
ValueError: File is neither Gating-ML 2.0 compliant nor a FlowJo workspace.
```

Writing something only we can read defeats the purpose of an interchange format. Our own reader could not notice, because it uses `find`/`findall` — which happily locate misplaced and misnamed elements.

### Four independent violations

Each confirmed against the XSD that ships with FlowKit 1.3.2 (`_resources/Gating-ML.v2.0.xsd`).

| | Violation | XSD says |
|---|---|---|
| 1 | `compensation-ref` never written on `dimension` (or on `divider`) | `Dimension_Type/@compensation-ref` is `use="required"`. `QuadrantGateDivider_Type` extends `Dimension_Type`, so it applies there too. |
| 2 | `custom_info` appended **last** | It comes from `Custom_Group` on `AbstractGate_Type`; in an XSD `complexContent` extension the base's content precedes the extension's sequence — so it must **lead**. `"Element 'custom_info': This element is not expected. Expected is ( gating:dimension )"` |
| 3 | `custom_info` in the `gating` namespace | It is declared in **DataTypes**. `gating:custom_info` is a different, undeclared element. |
| 4 | `QuadrantGate` emitted **no** `Quadrant` elements | `QuadrantGate_Type` is `divider+` **then** `Quadrant+`. A consumer had the dividers and no way to know which region carried which name. |

For (1), the schema allows `'uncompensated'`, `'FCS'`, or a spillover matrix id. A gate carries no binding to a matrix, so `'uncompensated'` is the only one we can state truthfully.

For (4), quadrants are emitted with **dimension 0 as the low bit**, matching `QuadrantGate.masks`. Reversing it would silently swap two populations on export — the reader would restore names attached to the wrong regions.

### A semantic fix that also unblocked FlowKit

A `BooleanGate` no longer writes `gating:parent_id`. In Gating-ML that attribute means *"evaluated within the parent"*, and `ov.flow`'s boolean deliberately is not — measured on a 4-event fixture with a parent keeping 2:

```
P    = 2 of 4
A    = 1
notA = 3        # == n - A: the boolean ignores its parent, by design
```

Claiming the restriction was simply untrue. It also killed the consumer: FlowKit builds its tree from `parent_id` **and** the `gateReference`s, and the contradiction produced `NetworkXNoPath: No path between root and DP`. The tree placement now travels in `custom_info` and still round-trips.

### Verified

On a four-gate strategy — rectangle, polygon, 1-D threshold, quadrant:

```
XSD valid: True
FlowKit ACCEPTS — and reconstructs the full hierarchy,
  including all four quadrant sub-populations
ov.flow round trip: display names and parents unchanged
```

Backwards compatible: the reader still accepts the old `gating:custom_info` spelling, so documents written before this keep their display names.

### Tests

Five new cases in `tests/flow/test_gatingml.py`. The XSD check `importorskip`s — FlowKit is not a dependency (it pins `numpy>=2`) — so **each violation is also pinned with stdlib-only assertions** that run in the default CI:

- every `dimension`/`divider` names its compensation
- `custom_info` is the first child, in the DataTypes namespace
- a quadrant gate emits 2ⁿ `Quadrant`s, each a distinct combination of sides
- a boolean does not claim a parent it does not honour, and the placement survives the round trip

All four mutation-checked — reintroducing any one turns a test red.

`tests/flow`: 196 passed before, **201 passed, 0 failed** after.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6ed23a9d8584`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.