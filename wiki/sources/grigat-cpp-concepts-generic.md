---
title: "Grigat — C++-Konzepte und Generische Programmierung"
type: source
tags: [cpp, templates, stl, generic-programming, lecture-script, german, tuhh]
de: Vorlesungsskript
status: developing
created: 2026-10-12
updated: 2026-10-12
author: Prof. Dr.-Ing. Rolf-Rainer Grigat
source_type: lecture script (scanned PDF, 90 pages, image-only)
language: German
copyright: © Rolf-Rainer Grigat 2003–2019
path: raw/oop_cpp_concepts_and_generic_programing.pdf
printed_pages: 83–172
---

# Grigat — C++-Konzepte und Generische Programmierung

The direct continuation of [[sources/grigat-oop-teil1]] — same author, same
script, printed pages 83–172. Where part I built up object orientation, this part
covers the C++ machinery that makes it practical (operators, resource management,
exceptions, casts) and then generic programming (templates, the STL, complexity,
concurrency).

Image-only scan; read by rendering all 90 pages (see `CLAUDE.md` § Scanned PDFs).

## Structure

| § | Topic |
|---|---|
| 0.4.1 | Operatoren — notation, precedence table, postfix evaluation, operator overloading |
| 0.4.2 | Ein- und Ausgabe mit C++-Streams — predefined streams, manipulators |
| 0.4.3 | Arrays — memory layout, `argc`/`argv`, automatic vs. dynamic arrays |
| 0.4.4 | Kopierkonstruktor, Zuweisungsoperator, Move-Semantik — value categories, `move`/`forward` |
| 0.4.5 | Assertions — `assert`, `static_assert`, type functions |
| 0.4.6 | Ausnahmen — throw/catch, derived exception types, `noexcept` |
| 0.4.7 | Typumwandlungen — implicit/explicit casts, converting constructors, `explicit` |
| 0.5.1–0.5.2 | Generische Programmierung, C++ Templates — specialization, variadic templates |
| 0.5.3 | C++-Standardbibliothek — separation of data structures and operations |
| 0.5.4 | Smart Pointers — `unique_ptr`, `shared_ptr`, `weak_ptr` |
| 0.5.5 | Komplexitäten und O-Notation |
| 0.5.6 | Container — sequential, associative, unordered |
| 0.5.7 | Iteratoren |
| 0.5.8 | Traits — `iterator_traits` |
| 0.5.9 | Algorithmen der Standardbibliothek — ranges, `for_each`, `transform`, predicates |
| 0.5.10 | Iterator-Adapter — insert, stream, reverse |
| 0.5.11 | Funktionsobjekte (Funktoren) |
| 0.5.12 | Multithreading und Lambda-Ausdrücke |

## Key takeaways

- **Operators are functions.** An n-ary operator is equivalent to a free function
  with n parameters, or a member function with n−1. Overloading them is what lets
  user-defined types read like built-in ones.
- **Postfix (reverse Polish) notation removes the need for precedence** entirely:
  evaluation is a single stack pass. This connects §0.4.1 back to
  [[structures/stack]].
- **Resource management is the spine of §0.4.4.** Copy constructor, assignment
  operator, move constructor and move assignment are a single design problem —
  what happens to the pointees. See [[synthesis/special-member-functions]].
- **`std::move` moves nothing.** It is a cast to an rvalue reference. The move
  happens in the constructor or assignment operator that the cast selects.
- **Templates are compile-time instantiation, not runtime dispatch.** The
  contrast with [[concepts/polymorphism]] is the central idea of §0.5.2.
- **The STL's architecture is a deliberate decoupling**: containers know storage,
  algorithms know procedure, and iterators are the only thing both agree on. This
  is why an algorithm written once works on every container.
- **Complexity is stated formally** (§0.5.5.4): f ∈ O(g) :⇔ ∃n₀,c>0: ∀n≥n₀
  f(n) ≤ c·g(n), with the full o/O/Θ/Ω/ω family — and with the explicit warning
  that writing `f = O(g)` is an abuse of notation readable only left-to-right.
- **Container choice is a complexity decision**, and the script presents it that
  way rather than as a style preference.
- **Smart pointers answer the open question left by part I**: `unique_ptr` and
  `shared_ptr` make the `new`/`delete` discipline of §0.3.3 largely unnecessary.

## Relationship to previously ingested material

This source **resolves two open questions** filed in
[[synthesis/oop-core-concepts]]:

1. *"How do `unique_ptr`/`shared_ptr` change the virtual-destructor rule?"* —
   §0.5.4 covers smart pointers in full. See [[concepts/smart-pointers]].
2. *"How do templates and generic programming interact with these rules?"* —
   §0.5.1–0.5.2 is the answer. See [[concepts/templates]].

No contradictions with existing pages were found. The material is strictly
additive: part I's §0.3.2.11 promised more on constructors, and §0.4.4 delivers
the copy and move variants.

## Pages created from this source

§0.4: [[concepts/operators-and-precedence]], [[algorithms/postfix-evaluation]],
[[concepts/operator-overloading]], [[concepts/cpp-streams]],
[[concepts/arrays-and-dynamic-memory]], [[concepts/copy-constructor]],
[[concepts/assignment-operator]], [[concepts/value-categories]],
[[concepts/move-semantics]], [[concepts/assertions]], [[concepts/type-traits]],
[[concepts/exceptions]], [[concepts/type-conversions]]

§0.5: [[concepts/templates]], [[concepts/template-specialization]],
[[concepts/variadic-templates]], [[concepts/standard-library]],
[[concepts/smart-pointers]], [[concepts/big-o-notation]],
[[concepts/complexity-classes]], [[concepts/stl-containers]],
[[structures/vector]], [[structures/deque]], [[structures/list]],
[[structures/set-and-map]], [[structures/unordered-containers]],
[[concepts/iterators]], [[concepts/iterator-traits]],
[[algorithms/stl-algorithms]], [[concepts/predicates]],
[[concepts/iterator-adapters]], [[concepts/function-objects]],
[[concepts/multithreading]], [[concepts/lambda-expressions]]

Synthesis: [[synthesis/special-member-functions]]

## Caveats

- A lecture script, not the C++ standard. Where it simplifies or predates a
  standard revision, pages say so.
- Scan legibility is mixed; a few listings were partially cut off and the pages
  concerned flag reconstructed content.
- The multithreading section (§0.5.12) is an introduction; it does not cover
  `std::async`, futures, or the memory model.
