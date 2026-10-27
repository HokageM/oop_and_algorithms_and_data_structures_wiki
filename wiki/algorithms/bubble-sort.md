---
title: Bubble Sort
type: algorithm
tags: [sorting, simple-sort, in-place, comparison-sort]
de: Sortieren durch Austauschen
status: developing
created: 2026-10-12
updated: 2026-10-12
sources: [sources/grigat-trees-sorting.md]
---

**Bubble sort (*Sortieren durch Austauschen*)** repeatedly scans the unsorted suffix of an array from the back towards a fixed front index, swapping adjacent out-of-order elements so the smallest remaining element "bubbles" forward into its sorted position each pass.

## Idea

For each outer index `i` from `0` to `N-2`, the invariant `a[0..i-1]` is fertig sortiert and `a[i-1] <= a[i..N-1]`; the inner loop scans `j` from `N-1` down to `i+1`, swapping `a[j]` and `a[j-1]` whenever they are out of order, so that `a[j]` always holds the minimum of `a[j..N-1]` seen so far by the end of the pass, which ends up fixing `a[i]`.

## Algorithm

```
1. for i = 0 to N-2:
2.     for j = N-1 down to i+1:
3.         if a[j] < a[j-1]:
4.             swap(a[j], a[j-1])
```

Invariants stated in the source:
- Outer loop (for i>0): `a[0..i-1]` fertig sortiert und `a[i-1] <= a[i..N-1]`.
- Inner loop: `a[j]` ist Minimum von `a[j..N-1]`.

## Worked example

Example trace for sorting `<6,2,4,1,8,7,5,3>` by exchanging (Tabelle 28). Each row is one swap step; bold rows mark the end of a completed outer-loop pass:

| a0 | a1 | a2 | a3 | a4 | a5 | a6 | a7 |
|---|---|---|---|---|---|---|---|
| 6 | 2 | 4 | 1 | 8 | 7 | 5 | 3 |
| 6 | 2 | 4 | 1 | 8 | 7 | *3* | 5 |
| 6 | 2 | 4 | 1 | 8 | *3* | 7 | 5 |
| 6 | 2 | 4 | *1* | 3 | 8 | 7 | 5 |
| 6 | 2 | *4* | 1 | 3 | 8 | 7 | 5 |
| 6 | *2* | 1 | 4 | 3 | 8 | 7 | 5 |
| *1* | 6 | 2 | 4 | 3 | 8 | 7 | 5 |
| **1** | 6 | 2 | 4 | 3 | 8 | 7 | 5 |
| 1 | 6 | 2 | 4 | 3 | 8 | *5* | 7 |
| 1 | 6 | 2 | 4 | *3* | 5 | 8 | 7 |
| 1 | 6 | 2 | *4* | 3 | 5 | 8 | 7 |
| 1 | *6* | 2 | 3 | 4 | 5 | 8 | 7 |
| 1 | *2* | 6 | 3 | 4 | 5 | 8 | 7 |
| **1** | 2 | 6 | 3 | 4 | 5 | 8 | 7 |
| 1 | 2 | 6 | 3 | 4 | 5 | *7* | 8 |
| 1 | 2 | 6 | 3 | 4 | *5* | 7 | 8 |
| 1 | 2 | 6 | 3 | *4* | 5 | 7 | 8 |
| 1 | 2 | *6* | 3 | 4 | 5 | 7 | 8 |
| **1** | 2 | 3 | 6 | 4 | 5 | 7 | 8 |
| 1 | 2 | 3 | 6 | 4 | 5 | *7* | 8 |
| 1 | 2 | 3 | 6 | 4 | *5* | 7 | 8 |
| 1 | 2 | 3 | 6 | *4* | 5 | 7 | 8 |
| **1** | 2 | 3 | 4 | 6 | 5 | 7 | 8 |
| 1 | 2 | 3 | 4 | 6 | *5* | 7 | 8 |
| **1** | 2 | 3 | 4 | 5 | 6 | 7 | 8 |
| 1 | 2 | 3 | 4 | 5 | 6 | *7* | 8 |
| **1** | 2 | 3 | 4 | 5 | 6 | 7 | 8 |
| 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 |

Final sorted result: `1,2,3,4,5,6,7,8`. (Italic = element just swapped; bold row = pass boundary, per the source transcription.)

```mermaid
flowchart LR
    A["pass i=0: scan from a7 down to a1"] -->|bubbles 1 to front| B["a0 fixed = 1"]
    B -->|pass i=1: scan down to a2| C["a1 fixed = 2"]
    C -->|pass i=2: scan down to a3| D["a2 fixed = 3"]
    D -->|...| E["a[0..N-1] fully sorted"]
```

## Implementation

```cpp
template<typename T>
void bubbleSort(T *a){
    for (i=0; i<N-1, i++)
    {
    // Invariante fuer i>0:
    // a[0..i-1] fertig sortiert und a[i-1]<=a[i..N-1]
        for (j=N-1; j>i; j--)
        {
        // Invariante: a[j] ist Minimimum von a[j..N-1]
            if (a[j] < a[j-1]) swap(a[j], a[j-1]);
        }
    }
}
```

> [!note]
> The scan shows `for (i=0; i<N-1, i++)` with a comma instead of `;` before `i++`, transcribed verbatim from the source — almost certainly an OCR/typo artifact of the original script; logically it should read `for (i=0; i<N-1; i++)`.

## Complexity

| | Best | Average | Worst | Extra space | Stable | In-place |
|---|---|---|---|---|---|---|
| Comparisons `C(n)` | O(n²) | O(n²) | O(n²) | — | — | — |
| Exchanges `X(n)` | O(n²) | O(n²) | O(n²) | — | — | — |
| Total `T(n) = C(n)+X(n)` | O(n²) | O(n²) | O(n²) | O(1) | not addressed in source (textbook-standard: stable) | yes |

The source states `C(n) ∈ O(n²)` and `X(n) ∈ O(n²)`, giving `T(n) = C(n) + X(n) ∈ O(n²) + O(n²) = O(n²)`, uniformly (no separate best case given).

## Related

- [[algorithms/sorting-overview]]
- [[algorithms/sorting-comparison]]
- [[algorithms/selection-sort]]
- [[algorithms/insertion-sort]]
- [[concepts/big-o-notation]]
- [[concepts/complexity-classes]]
- [[structures/vector]]
- [[algorithms/stl-algorithms]]

## Sources

- [[sources/grigat-trees-sorting]] §0.13.2.7, §0.13.2.8, §0.13.2.9

## Open questions

- Stability is not explicitly asserted by the source (only implied generally by the "stable methods" classification criterion in §0.13.1.2); textbook bubble sort is stable because it only swaps strictly-less-than pairs, but this source makes no explicit stability claim for bubbleSort.
- The empirical runtime table in [[algorithms/sorting-comparison]] (§0.13.5.5) only reports bubble sort timings for *vorsortiert* (presorted) input, leaving unsorted-input timings blank in the source table — reproduced as-is, not filled in.
