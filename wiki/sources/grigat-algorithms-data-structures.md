---
title: "Grigat — Teil II: Algorithms and Data Structures"
type: source
tags: [source, lecture-script, data-structures, algorithms, german]
de: "Vorlesungsskript — Teil II: Datenstrukturen und Algorithmen"
author: Prof. Dr.-Ing. Rolf-Rainer Grigat (TUHH)
language: de
file: raw/oop_algos_and_datastructures.pdf
pages: 83
printed_pages: 257-340
sections: 0.9-0.11
ingested: 2026-10-12
status: ingested
---

# Grigat — Teil II: Algorithms and Data Structures

The opening of **Teil II** of the lecture script, printed pp. 257–340. Where Teil I
and the C++ sections taught a language, Teil II teaches the classical
data-structures canon. Scanned, no text layer; transcribed from page images.

## Scope

| § | Title | Printed pp. |
|---|---|---|
| 0.9 | Einleitung — literature, symbols, abstraction levels | 257–266 |
| 0.9.2 | Abstraction levels; specifying a data structure | 259–266 |
| 0.10 | Grundlegende Datentypen | 266–299 |
| 0.10.1 | Listen — ADT models, linked and array implementations | 266–283 |
| 0.10.2 | Stacks | 283–285 |
| 0.10.3 | Queues | 285–287 |
| 0.10.4 | Binäre Bäume | 287–295 |
| 0.10.5 | Allgemeine Bäume | 295–299 |
| 0.11 | Mengen, Dictionaries und Priority Queues | 299–340 |
| 0.11.1 | Mengen — bit vector, unordered list, ordered list | 299–304 |
| 0.11.2 | Dictionaries | 304–305 |
| 0.11.3 | Hashing — functions, collisions, open/closed, probing | 305–314 |
| 0.11.4 | Binäre Suchbäume | 314–317 |
| 0.11.5 | AVL-Bäume — rotations and rebalancing | 317–320 |
| 0.11.6 | Optimale binäre Suchbäume (dynamic programming) | 321–330 |
| 0.11.7 | Priority Queues | 330–331 |
| 0.11.8 | Heaps — SiftUp, Sift, correctness | 331–339 |
| 0.11.9 | Übersicht Baumstrukturen | 340 |

## Why this source matters

It changes the wiki's centre of gravity. Everything before it describes **how C++
expresses an idea**; this source describes **which idea to express**, and it does so
in a notation deliberately independent of any language — ADTs specified
axiomatically, algorithms given as pseudocode, costs given as asymptotic bounds.

The payoff is that the wiki's existing STL pages acquire a foundation underneath
them. [[structures/vector]], [[structures/list]], [[structures/set-and-map]] and
[[structures/unordered-containers]] document what the standard library *provides*;
[[structures/linked-list]], [[structures/set]], [[structures/dictionary]] and
[[structures/hash-table]] now document what those containers *are* and what they
cost. The complexity tables on the STL pages stop being assertions and become
consequences.

Note the deliberate naming split, recorded here so a future session does not
"helpfully" merge them: pages named after the STL type are about the C++ container;
pages named after the structure are about the ADT and its implementations.

## Key takeaways

- **§0.9.2 is the conceptual spine**: mathematics (algebra) → algorithmics (ADT) →
  programming (class/type/module). It maps directly onto
  [[concepts/abstract-data-type]] and gives [[concepts/encapsulation]] a reason
  beyond style: the ADT *is* the interface, the data structure is one of several
  legal implementations.
- **One ADT, many data structures** is the repeated pattern. Sets get three
  implementations, dictionaries get five, and the script's habit is always to give
  the specification first and the cost table last.
- **Hashing gets more space than any other topic** (ten pages), including collision
  probability and the birthday paradox — unusually probabilistic for a programming
  script.
- **The optimal-BST section is a full dynamic-programming derivation** in four
  explicit steps, prefiguring §0.16. It is filed as
  [[algorithms/optimal-binary-search-tree]] with the methodology in
  [[concepts/dynamic-programming]].
- Most of this source is **pseudocode and mathematics, not C++**. The pages say so
  rather than inventing implementations; the script instead references companion
  code files (`KP33_2_priorityQueue`, `KP36_12_heap`, `KP21_4_einfachVerketteteListe`)
  that are not part of the scan.

## Pages created from this source

Concepts: [[concepts/abstraction-levels]]

Structures: [[structures/linked-list]], [[structures/queue]],
[[structures/binary-tree]], [[structures/general-tree]],
[[structures/expression-tree]], [[structures/set]], [[structures/dictionary]],
[[structures/hash-table]], [[structures/binary-search-tree]],
[[structures/avl-tree]], [[structures/priority-queue]], [[structures/heap]],
[[structures/tree-structures-comparison]]

Algorithms: [[algorithms/linear-search]], [[algorithms/binary-search]],
[[algorithms/tree-traversal]], [[algorithms/optimal-binary-search-tree]]

Extended: [[structures/stack]] gained the axiomatic ADT specification and the
array implementation.

## Open questions

- **Printed page 271 is missing from the scan set** (the images jump from 270 to
  272). It falls inside §0.10.1, the linked-list material. Worth re-scanning.
- Binary search is named and given its O(log n) bound but not developed; the
  [[algorithms/binary-search]] page is correspondingly thin.
- The companion C++ example files referenced throughout are not in `raw/`.

## Related

- [[sources/grigat-java]] — immediately precedes this part
- [[sources/grigat-trees-sorting]] — immediately follows (§0.12–0.13)
- [[sources/grigat-cpp-concepts-generic]] — the STL containers these structures underlie
- [[synthesis/complexity-cheatsheet]], [[synthesis/choosing-a-data-structure]]
