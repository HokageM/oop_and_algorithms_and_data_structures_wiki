---
title: Graph
type: structure
tags: [graph, discrete-structures, nodes, edges]
de: Graph
status: developing
created: 2026-10-12
updated: 2026-10-12
sources: [sources/grigat-graphs-dynamic-programming.md]
---

## One-sentence definition

A graph (*Graph*) **G** combines a set **V** of nodes with a relation
**E ⊆ V × V** into a structure **G = (V, E)** [[sources/grigat-graphs-dynamic-programming]] §0.14.1.1.

## Core idea / invariant

- **v ∈ V**: *Knoten* (node, vertex).
- **e = (v, w) ∈ E**: *Kante* (edge, arc) between nodes v and w.
- If the edge (v, w) exists, v and w are *adjazent* (adjacent).
- **|V|**: number of nodes; **|E|**: number of edges — these are the two
  parameters used throughout for running-time estimates (*Laufzeitabschätzung*)
  §0.14.1.1.
- **Grad** (degree) of a node: number of incoming and outgoing edges.
  - *Eingangsgrad* (in-degree): number of incoming edges.
  - *Ausgangsgrad* (out-degree): number of outgoing edges.
- **Pfad / Weg** (path): a sequence of nodes v₁,…,vₙ such that (vᵢ, vᵢ₊₁) ∈ E
  for all i. Its *Länge* (length) is the number of edges it contains.
- **Einfacher Pfad** (simple path): all nodes pairwise distinct, except that
  v₁ = vₙ is allowed.
- **Zyklus** (cycle): a simple path with v₁ = vₙ and n > 1 §0.14.2.2.
- **Gewichteter Graph** (weighted graph): a graph whose edges carry values
  (*Gewichte*, weights), e.g. distances/travel times in a transportation
  network, or currents/voltages in an electrical network §0.14.2.3.
- A **key teaching point** of the source: the geometric layout of nodes/edges
  on paper is *ohne Bedeutung* (without meaning) — only which pairs of nodes
  are connected, and in which direction, matters §0.14.1.2.

```mermaid
graph LR
    subgraph Left_Layout["Same graph, layout 1"]
    d --> a
    a --> c
    c --> b
    end
```

```mermaid
graph TD
    subgraph Right_Layout["Same graph, layout 2 — identical edges, different drawing"]
    a2[a] --> b2[b]
    a2 --> c2[c]
    a2 --> d2[d]
    c2 --- d2
    end
```

## Classification of graphs (§0.14.1.3–0.14.2)

| Criterion | Definition |
|---|---|
| *symmetrisch* (symmetric) | ∀v, w ∈ V, v ≠ w: edge (v,w) exists ⇒ edge (w,v) exists |
| *asymmetrisch* (asymmetric) | ∃v, w ∈ V, v ≠ w: edge (v,w) exists ∧ edge (w,v) does **not** exist |
| *reflexiv* (reflexive) | every node is connected to itself |
| *irreflexiv* (irreflexive) | edge (v,v) is excluded for all nodes |
| *transitiv* (transitive) | ∀v,w,z ∈ V: edges (v,w) and (w,z) exist ⇒ edge (v,z) exists |

**Gerichteter Graph** (*Digraph*, directed graph) vs. **ungerichteter Graph**
(undirected graph) §0.14.1.4–0.14.2.1:

- A **digraph**: edges have direction, drawn with arrows; may be symmetric or
  asymmetric; self-loops (v,v) are allowed.
- An **undirected graph**: a special case of a symmetric graph — the pair of
  edges {(v,w),(w,v)} is represented by **one** undirected edge; self-loops
  are **not** allowed. The source notes that algorithms are first discussed
  for digraphs (the more general case), with undirected graphs following
  later.

```mermaid
graph TD
    subgraph a_Gerichteter_Graph["(a) Gerichteter Graph (digraph)"]
    b2x[b] --> a2x[a]
    a2x --> c2x[c]
    b2x --> c2x
    c2x --> d2x[d]
    end
```

```mermaid
graph TD
    subgraph b_Ungerichteter_Graph["(b) Ungerichteter Graph (undirected)"]
    a3x[a] --- b3x[b]
    a3x --- c3x[c]
    a3x --- d3x[d]
    b3x --- c3x
    c3x --- d3x
    end
```

### Worked example digraph (used throughout this page family)

```
V = {a, b, c, d}
E = {(a,b), (a,c), (b,c), (c,d), (d,a)}
```

```mermaid
graph TD
    a110[a] --> b110[b]
    a110 --> c110[c]
    b110 --> c110
    c110 --> d110[d]
    d110 --> a110
```

in-degree(c) = 2, out-degree(c) = 1; `(a,b,c,d)` is a path; `(a,b,c,d,a)` is a
cycle §0.14.2.2.

### Weighted graph example

```mermaid
graph TD
    a111[a] -->|3| b111[b]
    b111 -->|0| b111
    a111 -->|5| d111[d]
    c111[c] -->|1| a111
    b111 -->|7| c111
    d111 -->|2| c111
    c111 -->|4| d111
```

## Related
- [[structures/graph-representations]] — adjacency matrix and adjacency list
- [[algorithms/depth-first-search]]
- [[algorithms/breadth-first-search]]
- [[structures/spanning-tree]]
- [[structures/dag]]
- [[algorithms/topological-sort]]
- [[concepts/big-o-notation]]
- [[concepts/complexity-classes]]
- [[structures/tree-structures-comparison]]

## Open questions
- The script foreshadows Dijkstra's shortest-path algorithm and Prim's
  minimum-spanning-tree algorithm as BFS-like generalizations
  (§0.14.3.1, "ähnlich den Algorithmen von Dijkstra, Prim"), but no worked
  content for either algorithm appears anywhere in the pages scanned for this
  ingest (printed pp. 400–422). Is this material covered later in the script
  (beyond p. 422), or in a different source entirely, and should
  `algorithms/dijkstra` / a minimum-spanning-tree page be created once such a
  source is found?

## Sources
- [[sources/grigat-graphs-dynamic-programming]] §0.14.1.1, §0.14.1.2, §0.14.1.3,
  §0.14.1.4, §0.14.2.1, §0.14.2.2, §0.14.2.3
