---
title: "Grigat — Java"
type: source
tags: [source, lecture-script, java, german]
de: Vorlesungsskript — Java
author: Prof. Dr.-Ing. Rolf-Rainer Grigat (TUHH)
language: de
file: raw/oop_java.pdf
pages: 44
printed_pages: 213-256
sections: "0.8"
ingested: 2026-10-12
status: ingested
---

# Grigat — Java

Part four of the continuous TUHH lecture script, printed pp. 213–256, section §0.8.
Scanned, no text layer; transcribed from page images.

## Scope

| § | Title | Printed pp. |
|---|---|---|
| 0.8.1–0.8.3 | Java vs. C++, the JVM, bytecode, packages | 213–220 |
| 0.8.4 | Visibility modifiers, nested and inner classes | 220–224 |
| 0.8.5 | Constructors, garbage collection, no destructors | 224–228 |
| 0.8.6 | Primitives vs. references, `==` vs. `equals()`, wrappers, arrays | 228–232 |
| 0.8.7 | Methods, static members, parameter passing | 232–234 |
| 0.8.8 | Inheritance, `super()`, the `Object` root | 234–238 |
| 0.8.9 | Overriding, `final`, abstract classes, interfaces, polymorphism | 238–244 |
| 0.8.10 | Exceptions, checked exceptions, `finally` | 244–248 |
| 0.8.11 | `clone()`, `Cloneable`, shallow copy | 248–251 |
| 0.8.12 | Generics, wildcards, type erasure, for-each | 251–256 |

## Why this source matters

This is the only non-C++ source in the wiki, and it is **not a Java tutorial** — it
is a systematic contrast. Every section is framed as "here is what C++ does, here
is what Java does instead, here is why". That makes it unusually valuable for a
wiki that is otherwise entirely C++: it turns implicit C++ design decisions into
explicit choices by showing a language that chose differently.

Three contrasts do the most work:

1. **Memory.** C++ gives you destructors, RAII and
   [[concepts/smart-pointers]]; Java gives you a garbage collector and no
   destructor at all. The whole of [[synthesis/special-member-functions]] is a
   problem Java does not have — and the price is non-deterministic finalization.
2. **Inheritance.** C++ allows [[concepts/multiple-inheritance]] and solves the
   diamond with virtual bases; Java forbids it and substitutes interfaces.
3. **Generics.** C++ [[concepts/templates]] instantiate separate code per type;
   Java generics compile once and erase the type. Same syntax, opposite mechanism.

A fourth, smaller but sharp one: Java methods are **virtual by default**, inverting
the C++ rule documented in [[concepts/polymorphism]].

## Key takeaways

- Java references are type-safe pointers that cannot be arithmetic-ed and cannot be
  rebound to an alias the way a C++ reference is fixed — the script treats this as
  the single most common source of C++-programmer confusion.
- Everything is passed by value in Java, including references. There is no
  call-by-reference, so [[concepts/parameter-passing]] has no Java counterpart.
- Checked exceptions (`throws`) have no C++ equivalent, and `finally` has no C++
  keyword equivalent because RAII covers the same ground.
- `clone()` is shallow by default, reproducing exactly the shallow-copy trap that
  [[concepts/copy-constructor]] warns about — in a language that supposedly removed
  that class of bug.

## Pages created from this source

- [[concepts/java-vs-cpp]] — the master comparison table
- [[concepts/java-bytecode-and-jvm]]
- [[concepts/java-packages]]
- [[concepts/java-nested-classes]]
- [[concepts/garbage-collection]]
- [[concepts/java-references-and-primitives]]
- [[concepts/java-classes-and-members]]
- [[concepts/java-inheritance-and-interfaces]]
- [[concepts/java-exceptions]]
- [[concepts/java-object-copying]]
- [[concepts/java-generics]]

## Language note

Per `CLAUDE.md`, code examples follow the language of the source. These pages use
Java, with C++ shown alongside for contrast and explicitly labelled. They are the
only pages in the wiki where C++ is not the default.

## Open questions

- The script's Java is pre-modern: no lambdas, no streams, no `var`, no records,
  no sealed types. The generics treatment predates `var` and diamond inference.
- Concurrency in Java is not covered at all, even though
  [[concepts/multithreading]] covers it for C++.
- Nothing is said about the Java collections framework beyond generics examples,
  so there is no counterpart to [[concepts/stl-containers]].

## Related

- [[sources/grigat-uml-patterns]] — immediately precedes this part
- [[sources/grigat-algorithms-data-structures]] — immediately follows (Teil II)
- [[sources/grigat-oop-teil1]], [[sources/grigat-cpp-concepts-generic]] — the C++ side of every comparison
