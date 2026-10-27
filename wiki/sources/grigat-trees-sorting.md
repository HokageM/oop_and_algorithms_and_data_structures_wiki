---
title: "Grigat — String Trees and Sorting"
type: source
tags: [source, lecture-script, trees, sorting, compression, german]
de: Vorlesungsskript — Spezielle Baumstrukturen und Sortieren
author: Prof. Dr.-Ing. Rolf-Rainer Grigat (TUHH)
language: de
file: raw/oop_trees_and_sorts.pdf
pages: 59
printed_pages: 341-399
sections: 0.12-0.13
ingested: 2026-10-12
status: ingested
---

# Grigat — String Trees and Sorting

Printed pp. 341–399, sections §0.12 and §0.13. Scanned, no text layer;
transcribed from page images.

## Scope

| § | Title | Printed pp. |
|---|---|---|
| 0.12 | Spezielle Baumstrukturen für Zeichenketten | 341–380 |
| 0.12.2 | Radix-Bäume (Tries) | 342–347 |
| 0.12.3 | Ternary Search Tries | 347–349 |
| 0.12.4 | LZW-Kompression | 349–355 |
| 0.12.5 | Codierung: FLC/VLC, Präfixcodes | 355–358 |
| 0.12.6 | Huffman-Codierung | 358–364 |
| 0.12.7 | Patricia-Bäume | 364–375 |
| 0.12.8 | String Matching, Suffix-Index | 375–378 |
| 0.13 | Sortieren | 378–399 |
| 0.13.1 | Problem definition, classification, cost model | 378–380 |
| 0.13.2 | Selectionsort | 380–381 |
| 0.13.3 | Insertion Sort | 381–383 |
| 0.13.4 | Bubble Sort | 383–385 |
| 0.13.5 | Divide and Conquer | 385–386 |
| 0.13.6 | Merge Sort | 386–389 |
| 0.13.7 | Quicksort | 389–392 |
| 0.13.8 | Heapsort | 392–395 |
| 0.13.9 | Tree Sort | 395–396 |
| 0.13.10 | Bucket Sort, Radix Sort | 396–398 |
| 0.13.11 | Comparison table | 399 |

## Why this source matters

Two halves with little in common except that both are classical.

**§0.12** is the most applied material in the whole script: Tries, Patricia trees,
LZW and Huffman are not abstract exercises but the actual machinery of text
indexing and file compression. It is also where the wiki acquires its first
*information-theoretic* content — [[concepts/prefix-codes]] and mean codeword
length have no counterpart anywhere else in the script.

**§0.13** is the sorting canon, and it is the best-instrumented section in the
entire source: every algorithm gets a worked trace, and §0.13.11 closes with both
an asymptotic table *and* measured runtimes. That empirical table is the only place
the script puts real numbers against its own O-notation, which makes it the natural
anchor for [[synthesis/complexity-cheatsheet]].

## Key takeaways

- **Tries trade memory for alphabet-independent lookup.** The script's
  Trie-vs-hash-table comparison is the first time two structures in the wiki are
  compared on *memory* rather than time.
- **Patricia trees are the payoff of §0.12** — the compressed Trie, with the
  script's most elaborate worked examples (insert and delete traced node by node).
- **Huffman is where the earlier chapters cash out**: greedy construction driven by
  a [[structures/priority-queue]], giving O(n log n) because of
  [[structures/heap]]. A reader who skipped §0.11.8 cannot follow it.
- **Heapsort and Tree Sort are structural sorts** — they are the heap and the AVL
  tree used as sorting engines, not new algorithms. They connect §0.13 back to
  §0.11 directly.
- The script is careful about **stability and in-place-ness**, not just asymptotics,
  which is exactly the distinction [[algorithms/stl-algorithms]] needs to explain
  why `std::sort` and `std::stable_sort` are different functions.

## Pages created from this source

Structures: [[structures/trie]], [[structures/ternary-search-trie]],
[[structures/patricia-tree]]

Concepts: [[concepts/prefix-codes]], [[concepts/divide-and-conquer]]

Algorithms: [[algorithms/lzw-compression]], [[algorithms/huffman-coding]],
[[algorithms/string-matching]], [[algorithms/sorting-overview]],
[[algorithms/selection-sort]], [[algorithms/insertion-sort]],
[[algorithms/bubble-sort]], [[algorithms/merge-sort]], [[algorithms/quicksort]],
[[algorithms/heapsort]], [[algorithms/tree-sort]], [[algorithms/bucket-sort]],
[[algorithms/radix-sort]], [[algorithms/sorting-comparison]]

## Open questions

- No lower-bound proof for comparison sorting (the Ω(n log n) decision-tree
  argument) appears, even though bucket and radix sort are presented as beating it.
- Boyer–Moore and Knuth–Morris–Pratt are not covered; string matching stops at the
  naive matcher plus suffix indexing.
- Introsort / the hybrid strategy real `std::sort` implementations use is not
  mentioned, so [[algorithms/stl-algorithms]] and [[algorithms/quicksort]] do not
  fully line up.

## Related

- [[sources/grigat-algorithms-data-structures]] — immediately precedes this part
- [[sources/grigat-graphs-dynamic-programming]] — immediately follows (§0.14–0.16)
- [[synthesis/complexity-cheatsheet]]
