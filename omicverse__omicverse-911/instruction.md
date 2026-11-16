# Issue

**Title:** fix(flow): a quadrant's sub-populations are populations, and can be parents

## Description

`add_gate`'s own comment says each quadrant **"must be addressable as a parent"**, and `apply()` has always handled it correctly. Only the validation refused — so gating within `CD4+CD8-`, the single most ordinary thing to do after drawing a quadrant, raised:

```
KeyError: "gate 'kid' names parent 'C4', which is not in this strategy.
           Known populations: ['root', 'Q']"
```

The check looked at `self._gates`, which holds only the gate objects. The octants live in `self._parent` — the map of every known **population** — and that is what a parent reference means.

### The module could not round-trip its own output

`to_dict()` emits `"parent": "C4"` for such a gate, and `from_dict()` on that exact document raised the same `KeyError`. A strategy that evaluated perfectly could not be saved and reloaded.

### And the silent one

`masks.get(parent)` returned `None` for a parent that had simply not been evaluated yet, and `None` means *"no restriction"* three lines later. A gate declared before its parent therefore reported the **whole sample**:

```
kid declared BEFORE its quadrant parent:
   kid = 200 of 200
   C4  = 50
   -> ran UNRESTRICTED, no exception, no warning
```

A plausible number that is 4× wrong is the worst failure mode this library has, so it now raises and names both the gate and what has been computed so far. `add_gate` keeps the order right by construction; `from_dict` takes whatever order the document lists, and `_order` is reachable directly.

A parent that genuinely does not exist is still refused — and the message now lists the octants, which is what the caller was reaching for.

### Verified

| | |
|---|---|
| gate inside `C4` | `kid` = 50 of `C4`'s 50 — not 200 |
| `to_dict` → `from_dict` → `apply` | byte-identical masks for every population |
| out-of-order | raises, naming the gate and the computed set |
| unknown parent | still raises |

### Tests

Four regression cases in `tests/flow/test_gates.py` (the file whose header is already *"Gate geometry and the gating strategy tree"*). Both fixes mutation-checked — restoring either turns its test red:

- restoring the `self._gates` check → `test_a_strategy_gated_inside_a_quadrant_round_trips_through_its_own_dict` fails
- restoring `masks.get(parent)` → `test_a_gate_before_its_parent_raises_instead_of_running_unrestricted` fails

`tests/flow`: 201 passed before, **205 passed, 0 failed** after.

Found while building the omicOS flow-cytometry tool, where the gating tree needs every population the kernel reports to be selectable and gateable.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `839835f1e7a5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.