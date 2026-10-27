---
title: "Grigat — Teil I: Objektorientierte Programmierung"
type: source
tags: [cpp, oop, lecture-script, german, tuhh]
de: Vorlesungsskript
status: developing
created: 2026-10-12
updated: 2026-10-12
author: Prof. Dr.-Ing. Rolf-Rainer Grigat
source_type: lecture script (scanned PDF, 82 pages, image-only)
language: German
copyright: © Rolf-Rainer Grigat 2003–2019
path: raw/oop_klassen.pdf
---

# Grigat — Teil I: Objektorientierte Programmierung

A German university lecture script covering imperative programming in C++ and
then object orientation from first principles. The scan has **no text layer**;
it was read by rendering all 82 pages to images (see `CLAUDE.md` § Scanned PDFs).

## Structure

| § | Topic |
|---|---|
| 0.1 | Einleitung — literature, programming-language popularity rankings, Stroustrup's tips for C and C++ programmers |
| 0.2.1 | Grundlagen — type/declaration/variable, initializer lists and `auto`, scope, assignment vs. initialization, `const`/`volatile`, for-loops, strings, keyboard input, `<chrono>` |
| 0.2.2 | Mehr über Zeiger — pointer-to-pointer, variadic arguments, function pointers, complex declarations, type aliases, matrices |
| 0.2.3 | Unterprogramme — top-down design, functions, prototypes, declarator operators, `main()` |
| 0.2.4 | Aufruf- und Rückgabeparameter — call by value vs. call by reference, const references, overloading, `auto` return types |
| 0.2.5 | Modularisierung — build pipeline, headers, preprocessor, linkage, storage classes, namespaces |
| 0.3.1 | Schnittstellen — abstract data types, the Stack ADT |
| 0.3.2 | Klassen — class vs. struct, UML, member functions, `this`, constructors, destructors |
| 0.3.3 | Objekte — static/automatic/dynamic memory, static members |
| 0.3.4 | Komposition — member objects, initializer lists |
| 0.3.5 | Vererbung — single and multiple inheritance, diamond problem, access modifiers, overriding, `final`/`override`, abstract classes |
| 0.3.6 | Friend functions and classes |
| 0.3.7 | Polymorphie — virtual functions, vtables, up/downcasts, virtual destructors, worked exercise |

## Key takeaways

- The script's through-line is **safety by construction**: initialize everything,
  prefer `const`, prefer references over pointers, prefer standard-library
  containers over raw arrays, let the compiler catch mistakes.
- C++ variables are **not** auto-initialized and the compiler does not check
  use-before-init — repeatedly flagged as the classic C++ bug source.
- A **declaration** links a name with types and may repeat; a **definition** fixes
  the entity and must occur exactly once. This single rule explains prototypes,
  header files, and linkage.
- **Encapsulation** is the organising idea of part 0.3: an interface of public
  methods over private data, formalised by the abstract data type.
- **Polymorphism costs nothing conceptually and something concretely**: a hidden
  `_vptr` per object and a vtable per class, only for classes with at least one
  virtual function.
- Three warnings are repeated emphatically: never override non-virtual functions;
  always make base-class destructors virtual; `protected` member variables are a
  design flaw.
- C++ permits **multiple inheritance** (Java does not), which brings the diamond
  problem and `virtual` base classes.

## Pages created from this source

Section 0.1–0.2:
[[concepts/type-declaration-definition]],
[[concepts/initialization-and-assignment]],
[[concepts/const-and-volatile]],
[[concepts/pointers-and-references]],
[[concepts/parameter-passing]],
[[concepts/function-declarations]],
[[concepts/function-overloading]],
[[concepts/complex-declarations]],
[[concepts/type-aliases]],
[[concepts/strings-cpp-vs-c]],
[[concepts/chrono-time-measurement]],
[[concepts/scope-and-storage-classes]],
[[concepts/modularization-and-build-pipeline]],
[[concepts/preprocessor-and-include-guards]],
[[concepts/namespaces]]

Section 0.3:
[[concepts/abstract-data-type]],
[[structures/stack]],
[[concepts/uml-class-diagram]],
[[concepts/class-and-object]],
[[concepts/encapsulation]],
[[concepts/member-functions]],
[[concepts/this-pointer]],
[[concepts/constructor]],
[[concepts/destructor]],
[[concepts/memory-model]],
[[concepts/static-members]],
[[concepts/composition]],
[[concepts/inheritance]],
[[concepts/multiple-inheritance]],
[[concepts/access-modifiers]],
[[concepts/overriding-vs-overloading]],
[[concepts/abstract-class]],
[[concepts/friend]],
[[concepts/polymorphism]],
[[concepts/vtable]]

Synthesis: [[synthesis/oop-core-concepts]]

## Contradictions with existing pages

None — this is the first source ingested into the wiki.

## Caveats

- The source is a **lecture script, not a standard**. Where it simplifies (e.g.
  the `siN` notation for standard-library duration types), the wiki says so.
- Several passages reference companion example files (`KP09_1`, `KP30_1`, …) that
  are not part of this PDF.
- The scan is of mixed legibility; a small number of code listings were partially
  cut off. Pages flag reconstructed content explicitly.

## Companion literature recommended by the script

- Ulla Kirch, Peter Prinz, *C++ Lernen und professionell anwenden*, mitp, 7th ed., 2015 ("gutes Lehrbuch")
- Bjarne Stroustrup, *Die C++ Programmiersprache*, Hanser, 2015 ("Referenz, sehr umfangreich")
- Scott Meyers, *Effektiv C++ programmieren*, Addison-Wesley, 2011
- Scott Meyers, *Effektives modernes C++*, Addison-Wesley, 2015
- Reference sites: cplusplus.com, cppreference.com, learncpp.com
