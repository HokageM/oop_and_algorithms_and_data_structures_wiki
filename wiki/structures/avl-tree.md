---
title: AVL Tree
type: structure
tags: [trees, balanced, ordered, search, dictionaries]
de: AVL-Baum
status: developing
created: 2026-10-12
updated: 2026-10-12
sources: [sources/grigat-algorithms-data-structures.md]
---

## One-sentence definition

An **AVL tree** (*AVL-Baum*) is a self-balancing [[structures/binary-search-tree]]
— named after Adelson-Velskii and Landis — that guarantees **O(log n)** for
all three [[structures/dictionary]] operations by restoring balance via
rotation after every insertion or deletion (§0.11.5.2).

## Balanced trees (§0.11.5.1)

**Definition.** A tree is **balanced** (*balanciert*) if, for every node,
the heights of its two subtrees differ by at most 1.

Unbalanced trees (Abbildung 81) can degenerate into a list-like chain, or
fan out wide at the top and then collapse into a long chain:

```mermaid
graph TD
    subgraph "(a) unbalanced: list-like chain"
    a1-->a2-->a3-->a4-->a5
    end
    subgraph "(b) unbalanced: fan then chain"
    b1-->b2
    b1-->b3
    b2-->b4
    b3-->b5
    b5-->b6
    b6-->b7
    end
```

Balanced trees are **not** always complete — height balance only constrains
the *difference* between subtree heights, not their shape (Abbildung 82):

```mermaid
graph TD
    subgraph "(a) balanced, fuller"
    c1-->c2
    c1-->c3
    c2-->c4
    c2-->c5
    c3-->c6
    c3-->c7
    end
    subgraph "(b) balanced, not complete"
    d1-->d2
    d1-->d3
    d2-->d4
    d2-->d5
    d4-->d6
    end
```

An AVL tree is a balanced BST; because it cannot degenerate into a list, the
cost of `insert`, `delete`, and `member` is **guaranteed O(log n)**
(§0.11.5.2). This lecture considers only AVL trees **without duplicate
keys** — the duplicate-key case is more complex and left to the specialized
literature (*Fachliteratur*) (§0.11.5.3).

## The AVL invariant and balance factor (§0.11.5.8)

Each node stores a **balance value** `b`, defined as:

```
b = height(left subtree) − height(right subtree)
```

| `b` | Meaning |
|---|---|
| `b ∈ {-1, 0, 1}` | node is **balanced** (*balanciert*) |
| `b ∈ {-2, 2}` | node is **unbalanced** (*unbalanciert*) — rebalancing required |

An AVL implementation stores either the height or the balance value in each
node (§0.11.5.8).

## Update operations (§0.11.5.3)

**Update** = inserting or deleting a node `p_e`; either can destroy balance.

- **Insert:** insert `p_e` exactly as in a plain BST. `p_e` now belongs to
  every subtree whose root lies on the path from the AVL tree's root to
  `p_e`; the height of each of these subtrees can grow by 1.
- **Delete:** delete `p_e` exactly as in a plain BST. The affected subtrees
  are those with root on the path from the AVL tree's root to `p_v`, the
  parent of the deleted node; the height of each of these subtrees can
  **decrease** by 1.

## Rebalancing after insertion vs. after deletion (§0.11.5.4)

Rebalancing is necessary whenever an update violates balance. Two cases are
treated separately because they have different consequences for the ancestor
chain:

- **(a) Thrown off balance by insertion:** restoring balance at the
  deepest unbalanced node is always *sufficient* — no further ancestors need
  checking.
- **(b) Thrown off balance by deletion:** restoring balance at one node may
  *change that subtree's height*, which can propagate the imbalance further
  up — ancestors may also need rebalancing (§0.11.5.8).

```mermaid
flowchart TD
    Insert["insert(node)"] --> R1["Rebalance at deepest unbalanced node\n(1 rotation or double rotation)"]
    R1 --> Done1["Done — no cascading needed"]
    Delete["delete(node)"] --> R2["Rebalance at parent\n(1 rotation or double rotation)"]
    R2 --> Check{"Did subtree height change?"}
    Check -->|yes| Up["Propagate rebalancing check up to ancestor subtrees"]
    Check -->|no| Done2["Done"]
    Up --> Check
```

## Single vs. double rotation: how to choose (§0.11.5.5)

Terminology:

- **Pivot** `P` (or `P1`, `P2`): the deepest node without balance.
- **Rotator** `R`: the child of the pivot that is the root of the pivot's
  **larger** subtree.
- If `R` is the **right** child of the pivot, `R`'s right subtree is the
  **outer** subtree `C` and `R`'s left subtree is the **inner** subtree `B`
  (their roots are children of `R` and siblings of each other). If `R` is
  the **left** child instead, inner/outer are mirrored.

**Decision rule:**

| Condition | Rebalancing operation |
|---|---|
| outer subtree `C` is taller than inner subtree `B` | **single rotation**, pivot `P` |
| inner subtree `B` is taller than outer subtree `C` | **double rotation**, pivots `P1` and `P2` |

## The rotation operation (§0.11.5.6)

**Single rotation:** pivot `P` sinks and rotator `R` rises by one height
level each. All subtrees follow their node (pivot or rotator) — **except**
the inner subtree, which keeps its height level but switches parents, from
the rotator to the pivot. If the inner subtree was the left (right) child of
the rotator, it becomes the right (left) child of the pivot.

```mermaid
flowchart LR
    subgraph before["before"]
    R1["Rotator R"] --> P1["Pivot P"]
    R1 --> C1["outer C"]
    P1 --> A1["A"]
    P1 --> B1["inner B"]
    end
    subgraph after["after"]
    P2["Pivot P (sunk)"] --> A2["A"]
    P2 --> B2["inner B (now child of P)"]
    R2["Rotator R (risen)"] --> P2
    R2 --> C2["outer C"]
    end
```

**Double rotation:** two opposite single rotations in sequence. The first
single rotation's only purpose is to establish the precondition for the
second (real) single rotation, by giving the outer subtree the greater
height. Both single rotations share the same rotator node (`R1 = R2`), but
have *different* pivot nodes `P1` and `P2` — both of which end up as
children of the shared rotator afterward (Abbildung 86).

```mermaid
flowchart LR
    subgraph double_rotation_sequence
    direction LR
    Start["Initial unbalanced tree (pivot z deepest unbalanced node)"] -->|"1. Rotation (Pivot=z, Rotator=y)"| Mid["Intermediate tree"]
    Mid -->|"2. Rotation (Pivot=x, Rotator=y)"| Final["Balanced result: y as new local root, x and z as children"]
    end
```

Crucially, rotation preserves the **inorder sequence**: `⟨A, x, B, y, C⟩`
stays the same before and after — only the tree's shape changes, not the
sorted order it represents.

## Rebalancing after insertion, in detail (§0.11.5.7)

### Case 1 — outer subtree `C` higher than inner subtree `B`: single rotation

```mermaid
flowchart LR
    subgraph before["before: outer C higher"]
    X["x (pivot, sinks)"] --> A["A"]
    X --> B["B (inner)"]
    Y["y (rotator, rises)"] --> X
    Y --> C["C (outer, higher)"]
    end
    subgraph after["after: single rotation"]
    Y2["y (new local root)"] --> X2["x"]
    Y2 --> C2["C"]
    X2 --> A2["A"]
    X2 --> B2["B (switched to x)"]
    end
```

### Case 2 — inner subtree `B` higher than outer subtree `C`: single rotation fails, double rotation required

A single rotation does **not** restore balance in this configuration
(Abbildung 84, "Geht nicht hier!" — "doesn't work here!"):

```mermaid
flowchart LR
    subgraph counter_example["single rotation FAILS when inner B is higher"]
    direction LR
    Y2["y (rotator)"] --> X2["x (pivot)"]
    Y2 --> C2["C (outer, lower)"]
    X2 --> A2["A"]
    X2 --> B2["B (inner, higher - the problem)"]
    end
```

The fix is to split the larger inner subtree `B` into `B1` and `B2`
(Abbildung 85), then apply a **double rotation** with two sub-cases
(Abbildung 87):

```mermaid
flowchart LR
    subgraph case1["Fall 1 von 2: h(B1) > h(B2)"]
    direction LR
    Zb1["z (pivot 1)"] --> Yb1["y (rotator)"]
    Yb1 --> Xb1["x (pivot 2)"]
    Xb1 --> Ab1["A"]
    Xb1 --> B1b1["B1"]
    Yb1 --> B2b1["B2"]
    Zb1 --> Cb1["C"]
    end
    subgraph case1after["after double rotation"]
    direction LR
    Ya1["y (new local root)"] --> Xa1["x"]
    Ya1 --> Za1["z"]
    Xa1 --> Aa1["A"]
    Xa1 --> B1a1["B1"]
    Za1 --> B2a1["B2"]
    Za1 --> Ca1["C"]
    end
```

```mermaid
flowchart LR
    subgraph case2["Fall 2 von 2: h(B1) < h(B2)"]
    direction LR
    Zb2["z (pivot 1)"] --> Yb2["y (rotator)"]
    Yb2 --> Xb2["x (pivot 2)"]
    Xb2 --> Ab2["A"]
    Xb2 --> B1b2["B1"]
    Yb2 --> B2b2["B2"]
    Zb2 --> Cb2["C"]
    end
    subgraph case2after["after double rotation — identical solution path"]
    direction LR
    Ya2["y (new local root)"] --> Xa2["x"]
    Ya2 --> Za2["z"]
    Xa2 --> Aa2["A"]
    Xa2 --> B1a2["B1"]
    Za2 --> B2a2["B2"]
    Za2 --> Ca2["C"]
    end
```

**Result for update-by-insertion:** one rotation or double rotation always
suffices to restore balance after inserting an element — no cascading check
up the tree is needed.

## Rebalancing after deletion, in detail (§0.11.5.8)

Unlike insertion, deletion rebalancing has **three** inner/outer cases
instead of two, because inner and outer subtrees can also tie in height.

### Case 1 — outer subtree `C` higher than inner subtree `B`: single rotation, height reduced by 1

```mermaid
flowchart LR
    subgraph before["before"]
    Y["y (pivot, sinks)"] --> A["A"]
    Y --> B["B"]
    X["x (rotator, rises)"] --> Y
    X --> C["C (outer, higher)"]
    end
    subgraph after["after single rotation — height reduced by 1"]
    X2["x (new local root)"] --> Y2["y"]
    X2 --> C2["C"]
    Y2 --> A2["A"]
    Y2 --> B2["B"]
    end
```

### Case 2 — outer `C` and inner `B` equally high: single rotation, height unchanged

```mermaid
flowchart LR
    subgraph before["before: B and C equally high"]
    Ye["y (pivot)"] --> Ae["A"]
    Ye --> Be["B (shaded, equal height)"]
    Xe["x (rotator)"] --> Ye
    Xe --> Ce["C (shaded, equal height)"]
    end
    subgraph after["after single rotation — height unchanged"]
    Xe2["x (new local root)"] --> Ye2["y"]
    Xe2 --> Ce2["C"]
    Ye2 --> Ae2["A"]
    Ye2 --> Be2["B"]
    end
```

### Case 3 — inner subtree `B` higher than outer `C`: double rotation required, 3 sub-cases, height reduced by 1

As already shown for insertion, a single rotation cannot restore balance
when the inner subtree is higher — a double rotation is required, now with
**three** sub-cases depending on the relative heights of `B1` and `B2`
(Abbildung 90):

| Sub-case | Condition |
|---|---|
| Fall 1 von 3 | `h(B1) > h(B2)` |
| Fall 2 von 3 | `h(B1) < h(B2)` |
| Fall 3 von 3 | `h(B1) = h(B2)` |

```mermaid
flowchart LR
    subgraph delete_double["double rotation after deletion (generic shape, all 3 sub-cases)"]
    direction LR
    Zd["z (pivot 1)"] --> Yd["y (rotator)"]
    Yd --> Xd["x (pivot 2)"]
    Xd --> Ad["A"]
    Xd --> B1d["B1"]
    Yd --> B2d["B2"]
    Zd --> Cd["C"]
    end
    subgraph delete_double_after["after — height reduced by 1"]
    direction LR
    Yda["y (new local root)"] --> Xda["x"]
    Yda --> Zda["z"]
    Xda --> Ada["A"]
    Xda --> B1da["B1"]
    Zda --> B2da["B2"]
    Zda --> Cda["C"]
    end
```

**Result for update-by-deletion:** one rotation or double rotation suffices
to restore balance *at that subtree*, but — unlike insertion — if this
changes the subtree's height, **ancestor subtrees may also need
rebalancing**, cascading the check upward (§0.11.5.8).

## Worked example: inserting weekdays into an AVL tree (§0.11.5.9, Abbildung 91)

Example: inserting German weekday names (alphabetical order), storing the
balance value `b` at every node.

**(a) Double rotation.** Before: root `Mi` (`b=+2`, unbalanced) with left
child `Do` (`b=-1`, whose child is `Fr`). After double rotation: new local
root `Do` (`b=0`), with `Di` and `Mo` as children.

```mermaid
graph TD
    subgraph "(a) before: unbalanced at Mi, b=+2"
    Mi_a["Mi (b=+2)"] --> Do_a["Do (b=-1)"]
    Do_a --> Fr_a["Fr (b=0)"]
    end
    subgraph "(a) after Doppelrotation"
    Do_a2["Do (b=0)"] --> Di_a2["Di (b=0)"]
    Do_a2 --> Mo_a2["Mo (b=0)"]
    end
```

**(b) Single rotation.** Before: root `Mi` (`b=+1`) with left child `Do`
(`b=-2`, unbalanced), whose left child is `Fr`. After single rotation: new
local root `Do` (`b=0`), with left child `Di` (`b=0`) and right child `Mi`
(`b=0`), which in turn has right child `Mo` (`b=0`).

```mermaid
graph TD
    subgraph "(b) before: unbalanced at Do, b=-2"
    Mi_b["Mi (b=+1)"] --> Do_b["Do (b=-2)"]
    Do_b --> Fr_b["Fr (b=0)"]
    end
    subgraph "(b) after Rotation"
    Do_b2["Do (b=0)"] --> Di_b2["Di (b=0)"]
    Do_b2 --> Mi_b2["Mi (b=0)"]
    Mi_b2 --> Mo_b2["Mo (b=0)"]
    end
```

**(c) Single rotation.** Before: root `Mi` (`b=+1`) with children `Do`
(`b=0`, children `Di`, `Fr`) and `Mo` (`b=-2`, unbalanced, right child `Sa`
→ `So`). After rotation: new local root `Mi` (`b=0`), left child `Do`
(`b=0`, children `Di`, `Fr`, `Mo`), right child `Sa` (`b=0`, child `So`).

```mermaid
graph TD
    subgraph "(c) before: unbalanced at Mo, b=-2"
    Mi_c["Mi (b=+1)"] --> Do_c["Do (b=0)"]
    Mi_c --> Mo_c["Mo (b=-2)"]
    Do_c --> Di_c["Di (b=0)"]
    Do_c --> Fr_c["Fr (b=0)"]
    Mo_c --> Sa_c["Sa"]
    Sa_c --> So_c["So (b=0)"]
    end
    subgraph "(c) after Rotation"
    Mi_c2["Mi (b=0)"] --> Do_c2["Do (b=0)"]
    Mi_c2 --> Sa_c2["Sa (b=0)"]
    Do_c2 --> Di_c2["Di (b=0)"]
    Do_c2 --> Fr_c2["Fr (b=0)"]
    Do_c2 --> Mo_c2["Mo (b=0)"]
    Sa_c2 --> So_c2["So (b=0)"]
    end
```

## Complexity table

| Operation | Best | Average | Worst | Assumption |
|---|---|---|---|---|
| `member` | O(log n) | O(log n) | **O(log n)** | guaranteed — AVL cannot degenerate |
| `insert` (incl. rebalancing) | O(log n) | O(log n) | **O(log n)** | at most one rotation/double rotation, no cascade |
| `delete` (incl. rebalancing) | O(log n) | O(log n) | **O(log n)** | rebalancing may cascade up to O(log n) ancestors, each O(1) |

Compare with the plain [[structures/binary-search-tree]], whose worst case
is O(n). See [[concepts/big-o-notation]] and [[concepts/complexity-classes]].

## Trade-offs: when to use, when not to

- Use an AVL tree whenever a *guaranteed* O(log n) bound is required
  regardless of insertion order (e.g. adversarial or sorted input).
- The price is bookkeeping: every node carries a balance value/height, and
  every update may trigger rotations.
- If a hard worst-case bound is not needed and raw expected speed matters
  more, [[structures/hash-table]] may be preferable (at the cost of sorted
  enumeration).

## Common pitfalls & gotchas

- Confusing *inner* and *outer* subtree when the rotator is a left vs.
  right child — the inner/outer assignment mirrors.
- Applying a single rotation when the inner subtree is the taller one: this
  does **not** restore balance (Abbildung 84) and a double rotation is
  required instead.
- After a deletion rebalance, forgetting to check whether the ancestor
  chain also needs rebalancing — unlike insertion, this check does not stop
  at the first fixed node.

## Related
- [[structures/binary-search-tree]] — the unbalanced structure this
  refines.
- [[structures/dictionary]] — the ADT this structure implements.
- [[structures/hash-table]] — the alternative dictionary implementation.
- [[structures/tree-structures-comparison]] — cross-cutting comparison
  table.
- [[concepts/big-o-notation]]
- [[concepts/complexity-classes]]

## Sources
- [[sources/grigat-algorithms-data-structures]] §0.11.5.1, §0.11.5.2,
  §0.11.5.3, §0.11.5.4, §0.11.5.5, §0.11.5.6, §0.11.5.7, §0.11.5.8,
  §0.11.5.9
