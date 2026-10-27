---
title: The this Pointer
type: concept
tags: [cpp, oop, pointers, method-chaining]
de: this-Zeiger
status: developing
created: 2026-10-12
updated: 2026-10-12
sources: [sources/grigat-oop-teil1.md]
---

Every object implicitly holds a pointer (*Zeiger*) to itself, called `this`; `*this` dereferences it to yield the object itself, which lets a [[concepts/member-functions|member function]] return a reference to its own object.

```mermaid
graph TB
    subgraph z1obj["object z1 @0x1000"]
        z1data["m_re=1.0, m_im=2.0"]
    end
    subgraph z2obj["object z2 @0x2000"]
        z2data["m_re=3.0, m_im=-1.0"]
    end
    Fn["CComplex::print()\n(one shared function body)"]
    Fn -->|"this = 0x1000"| z1obj
    Fn -->|"this = 0x2000"| z2obj
```

Both `z1.print()` and `z2.print()` execute the exact same compiled function;
only the implicit `this` argument differs, pointing each call at its own
object's data.

```mermaid
flowchart LR
    A["z.add(z1)"] -->|"return *this"| B["reference to z"]
    B -->|".add(z2) called on that reference"| C["z.add(z2)"]
    C -->|"return *this"| D["reference to z, now z+z1+z2"]
```

## Problem it solves

A member function such as `z.add(z1)` should be chainable: `z.add(z1).add(z2)` should first add `z1` to `z`, then add `z2` to the *result*. For that, `add` must return something that refers back to `z` itself — it needs a way to name "the object this function was called on" (§0.3.2.9).

## The `this` pointer

The compiler supplies every (non-static) member function with an implicit pointer named `this` that points to the calling object. Its dereferenced form `*this` is the content of that object (§0.3.2.9).

> Figure 5 ("Das Objekt z mit this-Zeiger") depicts an object's private/data section containing a `this` pointer that points back to the object's own public method interface, illustrating this self-reference.

## Example: method chaining

```cpp
CComplex& CComplex::add(const CComplex& zn)
{
  m_re += zn.re();
  m_im += zn.im();
  return *this;
}
```

`add` returns `CComplex&` — a reference to the object itself. Because `*this` *is* the calling object, `z.add(z1)` returns (a reference to) `z`; calling `.add(z2)` on that result is the same as calling it on `z` directly:

```cpp
z.add(z1).add(z2); // z += z1, then z += z2
```

First `add(z1)` runs on `z`; the returned reference is just another name for `z`, so `add(z2)` runs on `z` as well (§0.3.2.10).

## Consequences / trade-offs

- Returning `*this` by reference (`ClassName&`) avoids copying the object and enables fluent, chainable APIs.
- Returning by value (`ClassName`) instead of by reference would still compile but would copy the object on every chained call, defeating the purpose and changing semantics (a new temporary would be mutated, not the original).

## Misuse & anti-patterns

- Returning `this` (the pointer) instead of `*this` (the object) from a function declared to return `ClassName&` is a type mismatch; the two are easily confused by beginners.
- Chaining methods that return `*this` on a `const` object requires the method itself to be a [[concepts/member-functions|constant member function]] returning `const ClassName&` — otherwise it cannot be called at all.

## Related

- [[concepts/member-functions]]
- [[concepts/class-and-object]]
- [[concepts/pointers-and-references]]
- [[concepts/constructor]]

## Sources

[[sources/grigat-oop-teil1]] §0.3.2.9, §0.3.2.10
