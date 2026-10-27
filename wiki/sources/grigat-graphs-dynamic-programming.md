---
title: "Grigat — Graphs, External Sorting and Dynamic Programming"
type: source
tags: [source, lecture-script, graphs, dynamic-programming, german]
de: Vorlesungsskript — Graphen, Externes Sortieren, Dynamische Programmierung
author: Prof. Dr.-Ing. Rolf-Rainer Grigat (TUHH)
language: de
file: raw/oop_graphs_dynamic_programing.pdf
pages: 46
printed_pages: 400-449
sections: 0.14-0.16
ingested: 2026-10-12
status: ingested
---

# Grigat — Graphs, External Sorting and Dynamic Programming

The final part of the lecture script, printed pp. 400–449. Scanned, no text layer;
transcribed from page images.

## Scope

| § | Title | Printed pp. |
|---|---|---|
| 0.14 | Graphen | 400–419 |
| 0.14.1 | Definitions, classification, digraphs | 400–407 |
| 0.14.2 | Adjacency matrix and adjacency list | 407–410 |
| 0.14.3 | Tiefensuche (DFS), spanning trees, edge classification | 410–415 |
| 0.14.4 | Breitensuche (BFS) | 415–417 |
| 0.14.5 | DAGs and topological sorting | 417–419 |
| 0.15 | Externes Sortieren | 419–435 |
| 0.15.1 | Motivation and the block-I/O cost model | 419–422 |
| 0.15.2 | Mehrwege-Suchbäume, B-Bäume | 422–431 |
| 0.15.3 | Direktes Mischen, Vielweg-Mischen | 431–435 |
| 0.16 | Dynamische Programmierung | 436–449 |
| 0.16.1 | The four-step method | 436–439 |
| 0.16.2 | Assembly-line scheduling | 439–444 |
| 0.16.3 | Hidden Markov Models | 444–447 |
| 0.16.4 | Viterbi-Algorithmus, Spracherkennung | 447–449 |

## Why this source matters

It closes the script with the three things the earlier parts assumed but never
justified.

**§0.14** supplies the only non-hierarchical data structure in the wiki. Every
other structure so far is a sequence or a tree; a graph is the general case, and
DFS/BFS are the first algorithms that must cope with cycles and revisiting.

**§0.15** is the only place the script questions its own cost model. Everything up
to here counts comparisons and assumes uniform memory access. External sorting
replaces that with block I/O, and the B-tree exists *because* the cost model
changed — a node is sized to a disk block. It is the clearest demonstration in the
whole wiki that "optimal" is relative to a machine model.

**§0.16** generalises the dynamic-programming derivation that §0.11.6 did once for
optimal BSTs into a stated four-step method, then applies it twice more. The
Viterbi material takes the wiki somewhere genuinely unexpected: speech recognition,
with a trellis that turns out to be a shortest-path problem on a DAG.

## Key takeaways

- **Representation determines complexity.** Nearly every graph bound in §0.14 is
  quoted twice, once for the adjacency matrix and once for the list. This is the
  cleanest instance of the wiki's recurring "one ADT, many data structures" theme.
- **DFS and BFS differ only in the container** — stack versus queue — yet induce
  different spanning trees and different edge classifications.
- **B-trees are binary search trees generalised to high fan-out** and exist to
  minimise I/O, not comparisons.
- **DP = optimal substructure + overlapping subproblems**, solved bottom-up with a
  table and then reconstructed top-down. All three examples follow the same shape.
- **Viterbi is DP on a trellis**, i.e. a longest-path computation on a DAG in the
  log domain. It ties §0.16 back to §0.14.

## Pages created from this source

Structures: [[structures/graph]], [[structures/graph-representations]],
[[structures/spanning-tree]], [[structures/dag]], [[structures/b-tree]]

Algorithms: [[algorithms/depth-first-search]], [[algorithms/breadth-first-search]],
[[algorithms/topological-sort]], [[algorithms/external-merge-sort]],
[[algorithms/assembly-line-scheduling]], [[algorithms/viterbi]]

Concepts: [[concepts/dynamic-programming]], [[concepts/hidden-markov-model]]

## Open questions

- **Printed pages 440–443 are missing from the scan set** (the images jump from
  p40 to p41), inside the assembly-line-scheduling worked example. Worth
  re-scanning.
- **No Dijkstra, no minimum spanning tree, no shortest-path algorithm appears
  anywhere in the scanned pages**, even though §0.14.4 explicitly foreshadows
  Dijkstra and Prim as BFS-like generalizations. Either the script omits them or
  they live in material not supplied. This is the single largest gap in the wiki's
  coverage of the classical canon, and it is recorded on [[structures/graph]] and
  [[algorithms/breadth-first-search]] rather than silently filled in.
- Strongly connected components, flow algorithms and graph colouring are likewise
  absent.
- Memoized top-down DP is not contrasted with the bottom-up tabulation the script
  uses throughout.

## Related

- [[sources/grigat-trees-sorting]] — immediately precedes this part
- [[sources/grigat-algorithms-data-structures]] — §0.11.6 is the first DP example
- [[synthesis/complexity-cheatsheet]], [[synthesis/choosing-a-data-structure]]
