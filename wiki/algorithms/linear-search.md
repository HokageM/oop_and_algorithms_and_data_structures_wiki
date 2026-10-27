---
title: Linear Search
type: algorithm
tags: [search, array, vector, O(n)]
de: Lineare Suche
status: developing
created: 2026-10-12
updated: 2026-10-12
sources: [sources/grigat-algorithms-data-structures.md]
---

## One-sentence definition

Linear search (*lineare Suche*) finds a target value (here: the minimum) by
scanning every element of a sequence once, in order, with no assumption that
the sequence is sorted (§0.9.2.5).

## Core idea / invariant

**Invariant:** after examining the first `i` elements, the running value `m`
holds the minimum of exactly those `i` elements.

The script motivates linear search through a worked example across all three
[[concepts/abstraction-levels]] — math function, algorithmic pseudocode, C++
— for the problem "find the minimum $m$ in a set $S$ of natural numbers"
(§0.9.2.5).

## Specification as a function (math level)

Let $\mathbb{N}$ be the natural numbers and $F(\mathbb{N})$ the set of all
finite subsets of $\mathbb{N}$:

$$\min : F(\mathbb{N}) \to \mathbb{N}$$
$$\min(S) := m \quad \text{with} \quad m \in S,\ S \in F(\mathbb{N}),\ m \le x\ \forall x \in S$$

## Specification as an algorithm (pseudocode, algorithmic level)

Verbatim from the notes (1-based indexing, `S` an array of length `n`):

```
1  algorithm min(S)
2  // S ist Array der Länge n.
3  unsigned int m;
4  initalisiere m mit S[1]
5  for i:=2 to n do
6    if S[i] < m then m:= S[i] fi
7  rof
8  return m.
```

## Specification in a programming language (C++, programming level)

Verbatim from the notes:

```cpp
1  int min(vector<unsigned int>& S)
2  { // S ist als vector realisiert
3    unsigned int m = S[0];
4    vector<unsigned int>::iterator i;
5    for (i = ++S.begin(); i!= S.end(); i++)
6    {
7      if (*i < m) m = *i;
8    }
9    return m;
10 }
```

Note the index-base shift between pseudocode and C++, which the notes make
explicit: the pseudocode's `S[1]` is the first element (1-based), while the
C++ code's `S[0]` is the first element (0-based) and the loop begins at
`++S.begin()` — i.e. the *second* element, since `m` was already initialized
from the first. Both versions perform the same single linear pass.

```mermaid
flowchart LR
    Start([start: m := S first element]) --> Check{more elements?}
    Check -- yes --> Cmp{S[i] < m?}
    Cmp -- yes --> Update[m := S[i]]
    Cmp -- no --> Next[advance i]
    Update --> Next
    Next --> Check
    Check -- no --> Done([return m])
```

## Complexity

| Operation | Complexity | Note |
|---|---|---|
| `min(S)` / linear search over n elements | O(n) | See [[concepts/big-o-notation]]; the notes describe this complexity verbally for the general "search in list" example (§0.9.2.3) immediately before giving this `min` example, and it applies identically here: a single pass visits every element exactly once. |

See [[concepts/complexity-classes]] for where O(n) sits relative to O(log n)
([[algorithms/binary-search]]) and O(1).

## Reference implementation

The verbatim C++ above is the reference implementation; it uses
`std::vector` and its iterator (`vector<unsigned int>::iterator`), tying into
[[structures/vector]], [[concepts/iterators]], and
[[concepts/pointers-and-references]] (the function parameter `S` is taken by
reference, `vector<unsigned int>&`, to avoid copying the sequence).

## Trade-offs: when to use, when not to

- Use linear search when the sequence is unordered, or when a single pass is
  acceptable and the overhead of sorting first would not pay off.
- If the sequence is already sorted, the notes explicitly recommend
  [[algorithms/binary-search]] instead, trading O(n) for O(log n) — the
  script's key point is to "consider data structure and algorithm as a unit"
  (§0.9.2.3): the same function (search/minimum) admits a cheaper algorithm
  once the data structure guarantees an order.

## Common pitfalls & gotchas

- Off-by-one errors from mixing the pseudocode's 1-based indexing with
  0-based array/vector indexing, as illustrated directly by the two versions
  above.
- `S[1]` in step 4 of the pseudocode already consumes the first element as
  the initial minimum; the loop (and the C++ equivalent, `++S.begin()`)
  correctly starts from the *second* element — starting from the first again
  would just be redundant, not incorrect, but it is a common source of
  confusion when porting between the two notations.

## Related
- [[algorithms/binary-search]]
- [[concepts/abstraction-levels]]
- [[structures/vector]]
- [[concepts/iterators]]
- [[concepts/pointers-and-references]]
- [[concepts/big-o-notation]]
- [[concepts/complexity-classes]]

## Sources
- [[sources/grigat-algorithms-data-structures]] §0.9.2.3, §0.9.2.5
