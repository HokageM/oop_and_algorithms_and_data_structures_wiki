---
title: Assertions
type: concept
tags: [cpp, assertions, compile-time-checks, runtime-checks, fault-tolerance]
de: Zusicherungen
status: developing
created: 2026-10-12
updated: 2026-10-12
sources: [sources/grigat-cpp-concepts-generic.md]
---

## Definition

An **assertion** (*Zusicherung*) is an assumption about the relationship of variables to one another, expressed as a **predicate** (*Prädikat*) — i.e. a boolean expression that the programmer believes must always hold at a given point in the program. C++ offers two distinct assertion tools: `static_assert()`, checked at **compile time** (*Übersetzungszeit*), and `assert()`, checked at **run time** (*Laufzeit*).

## Problem it solves

Software fails either through faulty program code (*falscher Programmcode*) or faulty usage/operation (*fehlerhafte Bedienung*). **Fault-tolerant software** (*fehlertolerante Software*) detects and handles faulty computations (*fehlerhafte Berechnungen*) and faulty data (*fehlerhafte Daten*), preventing **undefined behavior** (*undefiniertes Verhalten*). Two of the available tools for this are assertions and [[concepts/exceptions]] (§0.4.5.1).

> [!note] What assertions can and cannot prove
> An assertion can show the **presence** of an error (if the predicate is false, something is definitely wrong), but it can never show the **absence** of errors — a passing assertion only means that particular check did not catch anything this time.

## A manual realization in C++ (§0.4.5.2)

Before dedicated language facilities, a simple boolean flag can serve as a hand-rolled assertion:

```cpp
bool allesGut = true;
/* Code, bei Problemen allesGut=false setzen */
if(!allesGut) exit(-1);
```

## `static_assert()` vs. `assert()` (§0.4.5.4)

| | `static_assert()` | `assert()` |
|---|---|---|
| Checked | at compile time (Übersetzungszeit) | at run time (Laufzeit) |
| Header | language built-in | `<cassert>` |
| What it can check | anything expressible as a constant expression (e.g. `sizeof`, type traits — see [[concepts/type-traits]]) | any runtime boolean expression |
| Disabling | not applicable (always a compile error if false) | can be disabled via the preprocessor in shipped ("Endprodukt") builds — faster execution, smaller binary |

**Compile time:**

```cpp
// Alles prüfen, was in Form konstanter Ausdrücke darstellbar ist,
// hier: Größe von Ganzzahlen prüfen; Meldung, falls Bedingung false
static_assert(4<=sizeof(int), "Ganzzahl zu klein");
template<typename T> void f(T& a) {
static_assert(std::is_floating_point<X>::value,"Gleitkommatyp erwartet");
//...
}
```

**Run time:**

```cpp
#include <cassert>
bool allesGut = true;
/* ... hier kann allesGut=false gesetzt werden ... */
assert(allesGut);
```

```mermaid
flowchart LR
    S["Source code\n(static_assert + assert)"] --> C["Compile time\n(Übersetzungszeit)"]
    C -->|"static_assert condition false"| CF["Build fails\n(compiler error)"]
    C -->|"static_assert condition true"| R["Runtime\n(Laufzeit)"]
    R -->|"assert condition false"| RA["Program aborts"]
    R -->|"assert condition true"| N["Program continues normally"]
    R -. "preprocessor: NDEBUG /\nrelease (\"Endprodukt\") build" .-> D["assert() calls compiled out entirely\n(faster execution, smaller binary)"]
```

```
Choosing between static_assert and assert:
1. If the condition can be fully evaluated from types/constants known to the
   compiler (sizes, type traits, template parameters) -> use static_assert(),
   catching the problem before the program ever runs.
2. If the condition depends on runtime data (user input, computed values,
   dynamic state) -> use assert(), catching the problem during execution.
3. Before shipping, assert() may be compiled out entirely (NDEBUG) for speed
   and size; static_assert() has no such switch since it never costs runtime.
```

## Consequences / trade-offs

- `static_assert` shifts error detection as early as possible (compile time), at zero runtime cost — the ideal place to check any invariant that is knowable statically, including [[concepts/type-traits]] on a template parameter.
- `assert` catches runtime-only problems, but by design is meant to be strippable for production, so it must never be used to perform work with side effects the program depends on (e.g. `assert(doSomething())` where `doSomething()` must always run).

## Misuse & anti-patterns

- Relying on `assert()` alone for input validation that must also run in release builds (since it may be compiled out) — use [[concepts/exceptions]] for recoverable, always-active error handling instead.
- Treating a passing assertion as proof of correctness rather than merely "no violation detected by this particular check."

## Related

- [[concepts/type-traits]]
- [[concepts/exceptions]]
- [[concepts/templates]]
- [[concepts/type-declaration-definition]]

## Sources

- [[sources/grigat-cpp-concepts-generic]] §0.4.5.1, §0.4.5.2, §0.4.5.4
