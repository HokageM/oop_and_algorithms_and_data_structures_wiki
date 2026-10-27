---
title: C++ Strings vs. C Strings
type: concept
tags: [cpp, strings, stdlib, c-interop]
de: C++-Strings und C-Strings
status: developing
created: 2026-10-12
updated: 2026-10-12
sources: [sources/grigat-oop-teil1.md]
---

# C++ Strings vs. C Strings

Two unrelated representations of text that coexist in every C++ program.

- **C++ string** — the class `std::basic_string`, header `<string>`. Has a far
  more powerful command set.
- **C string** — a null-terminated byte string, header `<cstring>`: a `char` array
  terminated by `'\0'`.

## Side-by-side

| Erläuterung | C++-Strings | C-Strings |
|---|---|---|
| Typ | `string` | `char*` |
| Headerdatei | `<string>` | `<cstring>` |
| Terminierung | keine (none) | Zeichen `\0` |
| Vergleich | `==` | `strcmp()` |
| Zeichen zählen | `size()`, `length()` | `strlen()` |
| Zuweisung | `=` | `strcpy()` |
| String nach double | `stod()` | `atof()` |
| String nach int | `stoi()` | `atoi()` |
| Suchen | `find()` | `strstr()` |
| Adresse drucken | `&myString` | `(void*)myString` |
| Zeile einlesen | `getline()` | `getchar()` |

## String literals are `const char[]`

The literal `"Hallo"` is a constant of type `const char[6]` — six characters,
including the terminating `'\0'`.

```mermaid
graph TD
    subgraph "C string: char p2[] = \"Hallo\";  (memory layout)"
        c0["'H'"] --> c1["'a'"] --> c2["'l'"] --> c3["'l'"] --> c4["'o'"] --> c5["'\\0'"]
    end
    subgraph "std::string s = \"Hallo\";  (object + owned buffer)"
        obj["string object\n(size, capacity, data pointer)"] -->|"data()"| buf["'H' 'a' 'l' 'l' 'o' ['\\0']"]
    end
```

Consequently the operators from `<string>` do **not** work on string literals:
`"Hallo"+"Hallo"` is invalid. But for a C++ string `s`, `s+"Hallo"+"Hallo"` is
allowed, because the left-most operand supplies the `operator+`.

```cpp
const char p1[6] = "Hallo"; // Konstantes Stringliteral
char p2[] = "Hallo";        // Ok, Cast auf veränderlichen String
char* p3 = "Hallo";         // Warnung, kein ISO C++, Längeninfo nur durch \0
const char* p4 = "Hallo";   // Ok
```

## Reading input

- `getchar()`, header `<cstdio>` — delivers all characters sequentially,
  **including** RETURN.
- `getline()`, header `<string>` — delivers an STL string or C string
  **without** RETURN.
- `<conio.h>` is not standard-conformant; `getch()` from it does not work in
  Eclipse. In Eclipse, keyboard data is evaluated only after RETURN.

```cpp
#include <iostream>
#include <string>
int main() {
    std::string name;
    std::cout << "Bitte Namen und RETURN eingeben: ";
    std::getline(std::cin, name);
    for(auto& c : name)
        if (c!='e') putchar(c); // 'e' unterdrücken
}
```

## Guidance

Stroustrup's advice as quoted in the script: use `string`, `array` and `vector`
from the standard library instead of raw arrays and C strings; use `=` instead of
`strcpy()` and `==` instead of `strcmp()`.

## Related

- [[concepts/pointers-and-references]]
- [[concepts/const-and-volatile]]
- [[concepts/initialization-and-assignment]]
- [[concepts/stl-containers]]
- [[concepts/cpp-streams]] (`std::cin`/`std::cout`, `getline`)
- [[structures/vector]] (array-like storage, same decay-to-pointer issues)

## Sources

- [[sources/grigat-oop-teil1]] §0.2.1.7 (C++-Strings und C-Strings),
  §0.2.1.8 (Gegenüberstellung C++- und C-Strings),
  §0.2.1.9 (Eingabe von Einzelzeichen durch Tastatur), §0.1.3.1 (Tipps für C-Programmierer)
