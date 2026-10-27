---
title: Java References and Primitives
type: concept
tags: [java, references, primitives, pointers, equals]
de: Grundtypen und Referenztypen
status: developing
created: 2026-10-12
updated: 2026-10-12
sources: [sources/grigat-java.md]
---

## Definition

Java variables (§0.8.5.1) are one of two kinds:

- **Grundtyp-Variablen** (primitive-type variables), e.g. `int`, `double`,
  `boolean` — the value is stored directly in the variable.
- **Referenztyp-Variablen** (reference-type variables) — every variable that is
  not a primitive type (pointers to classes, pointers to fields/arrays). The
  variable stores a **pointer** (*Zeiger*) to the data. The script is explicit
  that calling these "References" is technically a misnomer (*fälschlich als
  Referenz*); it calls them **Referenz(Java)** to distinguish them from C++
  references. There is **no address-of operator or dereference operator**
  (similar to `&` resp. `*` in C++) for a Referenz(Java) — the dot (`.`) in
  Java corresponds to `->` in C++.

## Memory diagrams: C++ value / pointer / reference vs. Java primitive / reference

```mermaid
graph TB
    subgraph CPP_VALUE["C++ value type"]
        cv["int a = 3;"] --> cvs["storage holds 3 directly"]
    end
    subgraph CPP_PTR["C++ pointer"]
        cp["CMyInt* p = &obj;"] --> cps["storage holds obj's ADDRESS"]
        cps -.dereference with *.-> cpo["obj"]
    end
    subgraph CPP_REF["C++ reference"]
        cr["CMyInt& b = a;"] -.alias, no own storage.-> cro["a's storage"]
    end
    subgraph JAVA_PRIM["Java primitive"]
        jv["int a = 3;"] --> jvs["storage holds 3 directly"]
    end
    subgraph JAVA_REF["Java Referenz(Java)"]
        jr["MyInt c = new MyInt(3);"] --> jrs["storage holds an ADDRESS\n(reassignable, type-safe pointer)"]
        jrs -.dereference with '.'.-> jro["the MyInt object"]
    end
```

## Referenz(C++) vs. Referenz(Java) — Tabelle 8 (§0.8.5.2)

| Eigenschaft (property) | Referenz(C++) | Referenz(Java) |
|---|---|---|
| Verweis enthält (reference contains) | Zielinhalt (target content) | Adresse (address) |
| Veränderung der Zuordnung (reassignment possible) | nicht möglich (not possible) | möglich (possible) |
| Referenz belegt Speicher (occupies own memory) | nein (no) | ja (yes) |
| anschaulich (intuitively) | "anderer Name" (another name) | "typsicherer Zeiger" (type-safe pointer) |

> [!warning]
> References(C++) and References(Java) are **different concepts** — the script
> explicitly flags the danger of confusion. Referenz(Java) **are pointers**.

## The canonical worked example (§0.8.5.3)

**C++ (`b` is a fixed alias for `a` forever):**
```cpp
CMyInt a(1);
CMyInt &b = a;   // Referenz(C++): b anderer Name für a
CMyInt c(6);
// a.x==1  b.x==1  c.x==6

b = c;
// entspricht: a = c;  (b is just an alias, so this is a VALUE assignment through b)
// a.x==6  b.x==6  c.x==6

c.verdoppeln();
// a.x==6  b.x==6  c.x==12

a.verdoppeln();
// a.x==12  b.x==12  c.x==12
```

**Java (`b` is a reassignable pointer):**
```java
MyInt a = new MyInt(1);
MyInt b = a;          // b ist Referenz auf a
MyInt c = new MyInt(6);
// a.x==1  b.x==1  c.x==6

b = c;
// b ist jetzt Referenz auf c  (b is REBOUND, a is untouched)
// a.x==1  b.x==6  c.x==6

c.verdoppeln();
// a.x==1  b.x==12  c.x==12
a.verdoppeln();
// a.x==2  b.x==12  c.x==12
```

### Pseudocode: C++ reference-rebinding behaviour

```
1. Create object a with x=1
2. Bind reference b to alias a (b and a are now the same storage)
3. Create separate object c with x=6
4. Assign b = c  → because b is an alias for a, this copies c's VALUE into a
   → a.x becomes 6 (NOT rebound to c)
5. Any further operation on a or b affects the same single object
```

### Pseudocode: Java reference-rebinding behaviour

```
1. Create object a with x=1 (a is a reference/pointer to this object)
2. b = a  → b now points to the SAME object as a
3. Create separate object c with x=6
4. b = c  → b is REBOUND to point to c; a is unaffected, still points to its own object
5. c.verdoppeln() → modifies the object now shared by b and c; a is untouched
6. a.verdoppeln() → modifies a's own separate object
```

This is one of the most important distinctions in the whole source: identical
C++ and Java syntax (`b = a; b = c;`) produces *completely different* observable
behavior. Readers must not assume Java "references" behave like C++ references
just because of the shared name.

## `==` vs. `equals()` (§0.8.5.4–0.8.5.6)

- For **primitive types**, `==` compares the **value** of the variables.
- For **reference types**, `==` compares the **value of the Referenz(Java)**
  (the pointer/address) — *not* the member variables' content.
- The class **`Object`**: all Java classes are implicitly derived from
  `Object` (Java's universal base class — contrast with C++, which has no
  universal root class). `Object` defines `boolean equals(Object o)`, which
  initially also compares references, but is usually **overridden** in derived
  classes to compare content instead.

```java
int a = 3;
int b = a;
MyInt c = new MyInt(3);
MyInt d = c;
MyInt e = new MyInt(d.getValue());

System.out.println(a == b);       // true, comparing VALUES
System.out.println(c == d);       // true, comparing POINTERS (same object)
System.out.println(c == e);       // false, pointers differ (different objects)
System.out.println(c.equals(e));  // true, if equals() is overridden to compare content
```

```java
public boolean equals(MyInt i){
  // Methode equals() überladen, um Inhalte zu vergleichen
  return (x == i.getValue());
}
```

Since Java provides **no operator overloading** at all, content comparison for
reference types must go through a named method (`equals`) rather than through
overloading `==` the way C++ overloads `operator==`.

## Wrapper classes for primitives (§0.8.5.7)

- Every primitive type has a corresponding **Wrapper class** (e.g. `Integer`
  for `int`, `Double` for `double`).
- **Arithmetic operations with Wrapper classes are NOT possible** directly.
- Applications: converting Strings to primitive values, and storing primitives
  in **Collections** (stated to correspond to C++ **Container**/
  [[concepts/stl-containers]]) — Collections can only store **classes**, not
  primitive types.

```java
LinkedList myIntList = new LinkedList();   // a Collection...
myIntList.add(new Integer(0));             // ...can only contain Objects
Integer x = new Integer("123");            // Initialization from a String
int a = x.intValue();                      // Conversion back to int
```

## Object creation with `new` (§0.8.5.8)

An object (instance of a class) must be created with `new` and is always
stored in a reference-type variable. **Even a parameterless constructor call
requires explicit `()`:**

```java
Auto erstwagen = new Auto();       // Java requires the parentheses
Auto zweitwagen = new Auto("gelb");
```

```cpp
CAuto *auto1 = new CCabrio;  // C++ allows omitting () for a default constructor
```

## Arrays and bounds checking (§0.8.5.9)

```java
Auto[] autos;
// Auto autos[]; ist äquivalent (both declaration styles are equivalent)

autos = new Auto[5];          // Arrayelemente werden mit 0 initialisiert
Auto autos[] = new Auto[5];   // äquivalente Anweisung

Auto mehrAutos[] = {new Auto("rot"), new Auto("gelb")};
// Elementanzahl wird aus Länge der Elementliste ermittelt
```

An array is always created with `new`. Java performs runtime **bounds
checking** (*Bereichsüberprüfung*): accessing `autos[5]` on a 5-element array
(valid indices 0–4) throws `ArrayIndexOutOfBoundsException`. C++ raw arrays do
**not** bounds-check by default (undefined behavior on out-of-range access).

## Compared with C++

See [[concepts/pointers-and-references]] for the full C++ model of pointers vs.
references that this page's Tabelle 8 contrasts against, and
[[concepts/arrays-and-dynamic-memory]] for C++ array/`new`/`delete` semantics
contrasted with Java's bounds-checked, GC-managed arrays. [[concepts/operator-overloading]]
covers the C++ `operator==`/`operator+` mechanism Java deliberately omits.
[[concepts/stl-containers]] covers the C++ container side of the
primitive-vs-wrapper-class contrast. See also [[concepts/java-vs-cpp]] for the
master table.

## Consequences / trade-offs

- No address-of/dereference operators means Java references cannot do pointer
  arithmetic or be manually dereferenced — safer, but less flexible than raw
  C++ pointers.
- Mandatory boxing of primitives into Wrapper classes for Collections adds
  overhead and syntactic noise compared to C++ templates instantiated directly
  over primitive types.
- Runtime bounds checking is a safety net at a small runtime cost, vs. C++'s
  zero-cost, unchecked array access.

## Misuse & anti-patterns

- Assuming `c == d` for two Java reference variables compares object content —
  it compares pointer identity; use `equals()` for content.
- Assuming `new Auto` (without parentheses) is valid Java, by analogy with C++.
- Attempting arithmetic directly on a Wrapper class instance instead of
  unwrapping via e.g. `.intValue()` first.

## Open questions

- The script does not describe Java's autoboxing/unboxing as an automatic
  compiler feature (it only shows explicit `new Integer(...)`/`.intValue()`
  calls) — whether implicit autoboxing is covered elsewhere in the course is
  not stated here.

## Related

- [[concepts/java-vs-cpp]]
- [[concepts/pointers-and-references]]
- [[concepts/memory-model]]
- [[concepts/operator-overloading]]
- [[concepts/stl-containers]]
- [[concepts/arrays-and-dynamic-memory]]
- [[concepts/java-object-copying]]
- [[concepts/java-classes-and-members]]

## Sources

[[sources/grigat-java]] §0.8.5.1, §0.8.5.2, §0.8.5.3, §0.8.5.4, §0.8.5.5,
§0.8.5.6, §0.8.5.7, §0.8.5.8, §0.8.5.9
