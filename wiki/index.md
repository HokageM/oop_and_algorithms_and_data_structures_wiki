---
title: Index
updated: 2026-10-12
pages: 153
sources: 7
---

# Index

Catalog of every page in this wiki. Maintained by the LLM — see `../CLAUDE.md`
for the schema it follows. [[log]] records how the wiki was built, in order.

All seven sources are one continuous TUHH lecture script by Prof. Dr.-Ing. Rolf-Rainer Grigat
(printed pp. 1-449). **Teil I** is C++ and OOP; **Teil II** is algorithms and data
structures. Start at [[synthesis/oop-core-concepts]] or
[[synthesis/choosing-a-data-structure]].

## Synthesis

- [[synthesis/oop-core-concepts]] - the two organising ideas of OOP, the repeated warnings, and how they interlock.
- [[synthesis/special-member-functions]] - copy/move constructor, copy/move assignment and destructor as one resource-ownership problem.
- [[synthesis/complexity-cheatsheet]] - every asymptotic bound in the wiki, in one place.
- [[synthesis/choosing-a-data-structure]] - the decision procedure the sources never state outright.

## Concepts

### Language fundamentals (C++)
- [[concepts/type-declaration-definition]] - type, declaration vs. definition, declarator operators.
- [[concepts/initialization-and-assignment]] - initializer lists, narrowing, `auto`, uninitialized-variable bugs.
- [[concepts/const-and-volatile]] - `const` vs. `volatile`; pointer-to-constant vs. constant pointer.
- [[concepts/scope-and-storage-classes]] - storage duration, `static`/`extern`, internal vs. external linkage.
- [[concepts/type-aliases]] - `typedef` vs. `using`, alias templates.
- [[concepts/complex-declarations]] - the right-then-left parsing rule.
- [[concepts/strings-cpp-vs-c]] - `std::string` vs. null-terminated `char*`.
- [[concepts/operators-and-precedence]] - operands, arity, associativity, the precedence table.
- [[concepts/arrays-and-dynamic-memory]] - static vs. dynamic arrays, `new[]`/`delete[]`, array decay.
- [[concepts/type-conversions]] - implicit conversions and the four named casts.
- [[concepts/value-categories]] - lvalue, rvalue, xvalue; why `T&&` exists.
- [[concepts/assertions]] - `assert` vs. `static_assert`, `NDEBUG`.
- [[concepts/chrono-time-measurement]] - `time_point`, `duration`, clocks; benchmarking.

### Functions
- [[concepts/function-declarations]] - prototypes vs. definitions, `main()`, variadic arguments.
- [[concepts/function-overloading]] - signature vs. return type, overload resolution.
- [[concepts/parameter-passing]] - call by value vs. call by reference.
- [[concepts/pointers-and-references]] - `&`/`*`, function pointers, dangling pointers.
- [[concepts/function-objects]] - functors: classes with `operator()`.
- [[concepts/lambda-expressions]] - capture lists, closures as anonymous functors.
- [[concepts/predicates]] - unary/binary predicates, strict weak ordering.

### Program structure
- [[concepts/modularization-and-build-pipeline]] - compiler, linker, translation units, object files.
- [[concepts/preprocessor-and-include-guards]] - `#include`/`#define`, `#ifndef` guards.
- [[concepts/namespaces]] - `::`, using-declaration vs. using-directive.
- [[concepts/standard-library]] - what the STL contains and how it composes.
- [[concepts/cpp-streams]] - `iostream`, manipulators, file and string streams.
- [[concepts/exceptions]] - `try`/`catch`/`throw`, stack unwinding, `noexcept`.

### Classes and objects
- [[concepts/abstract-data-type]] - specifying behaviour by axioms, independent of implementation.
- [[concepts/abstraction-levels]] - mathematics / algorithmics / programming; algebra vs. ADT vs. class.
- [[concepts/encapsulation]] - separating interface from implementation.
- [[concepts/class-and-object]] - `class` vs. `struct`, declaration/definition split.
- [[concepts/member-functions]] - access via `.` and `->`, const member functions.
- [[concepts/this-pointer]] - the implicit `this`, method chaining.
- [[concepts/constructor]] - delegation, member initializer lists, `=delete`/`=default`.
- [[concepts/destructor]] - `~Class()`, when it runs, the virtual-destructor rule.
- [[concepts/copy-constructor]] - deep vs. shallow copy.
- [[concepts/assignment-operator]] - self-assignment, returning `*this`.
- [[concepts/move-semantics]] - move constructor/assignment, `std::move`.
- [[concepts/operator-overloading]] - member vs. free operators, `operator<<`.
- [[concepts/memory-model]] - static vs. automatic (stack) vs. dynamic (heap).
- [[concepts/smart-pointers]] - `unique_ptr`, `shared_ptr`, `weak_ptr`; RAII ownership.
- [[concepts/static-members]] - class-level variables and functions.
- [[concepts/friend]] - deliberately breaking encapsulation.

### Reuse: composition, inheritance, polymorphism
- [[concepts/composition]] - "has-a", member objects.
- [[concepts/inheritance]] - "is-a", base class initialization.
- [[concepts/multiple-inheritance]] - the diamond problem and `virtual` base classes.
- [[concepts/access-modifiers]] - `public`/`private`/`protected` on members and base classes.
- [[concepts/overriding-vs-overloading]] - overriding, overloading and the hiding trap.
- [[concepts/abstract-class]] - pure virtual functions, interfaces.
- [[concepts/polymorphism]] - `virtual`, late vs. static binding, up/downcasts.
- [[concepts/vtable]] - the hidden `_vptr` and the per-class function-pointer table.

### Generic programming
- [[concepts/templates]] - function and class templates, instantiation.
- [[concepts/template-specialization]] - full and partial specialization.
- [[concepts/variadic-templates]] - parameter packs, recursive expansion.
- [[concepts/type-traits]] - compile-time type queries and transformations.
- [[concepts/iterators]] - the generalized pointer; the five categories.
- [[concepts/iterator-traits]] - `value_type`, `difference_type` and friends.
- [[concepts/iterator-adapters]] - reverse, insert, stream and move iterators.
- [[concepts/stl-containers]] - sequence vs. associative vs. unordered.

### Concurrency
- [[concepts/multithreading]] - `std::thread`, `join`/`detach`, data races, mutexes.

### Complexity and algorithm design
- [[concepts/big-o-notation]] - asymptotic upper bounds.
- [[concepts/complexity-classes]] - O(1) to O(n!), with growth comparison.
- [[concepts/divide-and-conquer]] - the divide/conquer/combine pattern.
- [[concepts/dynamic-programming]] - optimal substructure, overlapping subproblems, the four-step method.
- [[concepts/prefix-codes]] - fixed- vs. variable-length coding, the prefix property.
- [[concepts/hidden-markov-model]] - states, transitions, emissions, the forward formula.

### UML and process
- [[concepts/uml-overview]] - UML 2.0, its purpose, and the diagram taxonomy.
- [[concepts/uml-class-diagram]] - the full class-diagram notation reference.
- [[concepts/uml-sequence-diagram]] - lifelines, activation bars, messages.
- [[concepts/uml-use-case-diagram]] - overview level only; gap flagged.
- [[concepts/uml-activity-diagram]] - overview level only; gap flagged.
- [[concepts/uml-state-machine]] - overview level only; gap flagged.
- [[concepts/version-control]] - centralized vs. distributed, locking models, SVN, Mercurial.

### Java (contrast with C++)
- [[concepts/java-vs-cpp]] - **the master comparison table**; start here.
- [[concepts/java-bytecode-and-jvm]] - javac, bytecode, the JVM, CLASSPATH.
- [[concepts/java-packages]] - packages and import vs. namespaces.
- [[concepts/java-nested-classes]] - static nested, inner, local, anonymous.
- [[concepts/garbage-collection]] - the GC and the absence of destructors.
- [[concepts/java-references-and-primitives]] - primitives vs. references, `==` vs. `equals()`, wrappers.
- [[concepts/java-classes-and-members]] - constructors, visibility, statics, call-by-value.
- [[concepts/java-inheritance-and-interfaces]] - `extends`, `super`, interfaces, virtual-by-default.
- [[concepts/java-exceptions]] - checked exceptions, `finally`, the Throwable hierarchy.
- [[concepts/java-object-copying]] - `clone()`, `Cloneable`, shallow copy.
- [[concepts/java-generics]] - generics vs. templates, wildcards, type erasure.

## Data structures

### Sequences
- [[structures/linked-list]] - the list ADT and its linked and array implementations.
- [[structures/stack]] - LIFO: ADT axioms, array implementation, complexity.
- [[structures/queue]] - FIFO: ring-buffer implementation.
- [[structures/vector]] - contiguous dynamic array; amortized O(1) `push_back`.
- [[structures/deque]] - double-ended queue; O(1) at both ends.
- [[structures/list]] - `std::list`; O(1) splice given an iterator.

### Trees
- [[structures/binary-tree]] - nomenclature, recursive definition, height bounds, implementations.
- [[structures/general-tree]] - degree, forest, left-child/right-sibling representation.
- [[structures/expression-tree]] - operator trees; infix/prefix/postfix via traversal order.
- [[structures/binary-search-tree]] - the BST invariant, search/insert/delete.
- [[structures/avl-tree]] - balance factor, single and double rotations.
- [[structures/heap]] - min-heap property, SiftUp/Sift, O(log n).
- [[structures/b-tree]] - multiway search tree sized to a disk block.
- [[structures/tree-structures-comparison]] - BST vs. AVL vs. heap vs. B-tree, side by side.

### String structures
- [[structures/trie]] - radix search; O(k) in key length, independent of n.
- [[structures/ternary-search-trie]] - 3-way branching, lower memory overhead.
- [[structures/patricia-tree]] - the compressed trie; bit-position nodes and threads.

### Sets, dictionaries, priority queues
- [[structures/set]] - the set ADT: bit vector, unordered list, ordered list.
- [[structures/dictionary]] - the dictionary ADT and the decision guide over its implementations.
- [[structures/hash-table]] - hash functions, collisions, open vs. closed hashing, probing.
- [[structures/priority-queue]] - the axiomatic ADT.
- [[structures/set-and-map]] - `std::set`/`std::map`; O(log n), ordered.
- [[structures/unordered-containers]] - `std::unordered_*`; O(1) average, load factor.

### Graphs
- [[structures/graph]] - nodes, edges, degree, paths, cycles, classification.
- [[structures/graph-representations]] - adjacency matrix vs. adjacency list.
- [[structures/spanning-tree]] - spanning trees and forests, root graphs.
- [[structures/dag]] - directed acyclic graphs.

## Algorithms

### Searching
- [[algorithms/linear-search]] - O(n); the `min` worked example.
- [[algorithms/binary-search]] - O(log n) on sorted random-access data.
- [[algorithms/tree-traversal]] - inorder, preorder, postorder.
- [[algorithms/string-matching]] - the naive matcher and suffix-index search.

### Sorting
- [[algorithms/sorting-overview]] - the problem, the classification, the cost model.
- [[algorithms/selection-sort]] - O(n^2), O(n) exchanges.
- [[algorithms/insertion-sort]] - O(n^2); recommended for nearly-sorted input.
- [[algorithms/bubble-sort]] - O(n^2).
- [[algorithms/merge-sort]] - guaranteed O(n log n), O(n) extra space.
- [[algorithms/quicksort]] - O(n log n) average, O(n^2) worst; partition and pivot strategies.
- [[algorithms/heapsort]] - O(n log n), in place.
- [[algorithms/tree-sort]] - in-order traversal of an AVL tree.
- [[algorithms/bucket-sort]] - distribution sort, not comparison-based.
- [[algorithms/radix-sort]] - O(n) for constant key width.
- [[algorithms/external-merge-sort]] - direct and multiway merging under a block-I/O cost model.
- [[algorithms/sorting-comparison]] - the definitive table, including the script's measured runtimes.

### Graph algorithms
- [[algorithms/depth-first-search]] - DFS, spanning tree, edge classification.
- [[algorithms/breadth-first-search]] - BFS and its spanning tree.
- [[algorithms/topological-sort]] - in-degree removal on a DAG.

### Compression and coding
- [[algorithms/lzw-compression]] - dictionary coding with a trie.
- [[algorithms/huffman-coding]] - greedy prefix-code construction, O(n log n).

### Dynamic programming
- [[algorithms/optimal-binary-search-tree]] - the four-step DP derivation, O(n^3).
- [[algorithms/assembly-line-scheduling]] - DP over a two-track DAG.
- [[algorithms/viterbi]] - the most probable state sequence; DP on a trellis.

### Standard library
- [[algorithms/stl-algorithms]] - the `<algorithm>` catalogue by effect, with complexities.
- [[algorithms/postfix-evaluation]] - evaluating reverse Polish notation with a stack.

## Patterns

- [[patterns/design-patterns-overview]] - what a pattern is, GoF, the classification.
- [[patterns/singleton]] - one instance, globally reachable.
- [[patterns/adapter]] - making an incompatible interface usable.
- [[patterns/proxy]] - a stand-in that controls access; the hand-built smart pointer.
- [[patterns/strategy]] - interchangeable algorithms behind one interface.
- [[patterns/observer]] - subject/observer notification.

## Sources

All seven are parts of one continuous German lecture script by
Prof. Dr.-Ing. Rolf-Rainer Grigat, TUHH (C) 2003-2019, scanned without a text layer.

| Source | Printed pp. | Sections | Pages produced |
|---|---|---|---|
| [[sources/grigat-oop-teil1]] | 1-82 | 0.1-0.3.7 | 36 |
| [[sources/grigat-cpp-concepts-generic]] | 83-172 | 0.4-0.5.12 | 35 |
| [[sources/grigat-uml-patterns]] | 173-212 | 0.6-0.7 | 12 + 1 extended |
| [[sources/grigat-java]] | 213-256 | 0.8 | 11 |
| [[sources/grigat-algorithms-data-structures]] | 257-340 | 0.9-0.11 | 17 + 1 extended |
| [[sources/grigat-trees-sorting]] | 341-399 | 0.12-0.13 | 19 |
| [[sources/grigat-graphs-dynamic-programming]] | 400-449 | 0.14-0.16 | 13 |

### Known gaps in the sources

- Printed page 271 and pages 440-443 are missing from the scans.
- **No Dijkstra, no minimum spanning tree, no shortest-path algorithm** appears in
  any source, though the script foreshadows Dijkstra and Prim. See
  [[structures/graph]].
- No lower-bound proof for comparison sorting.
- Only 5 of the 23 GoF patterns are covered.
