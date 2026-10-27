---
title: Lambda Expressions
type: concept
tags: [lambda, closures, functors, cpp, generic-programming]
de: Lambda-Ausdrücke
status: developing
created: 2026-10-12
updated: 2026-10-12
sources: [sources/grigat-cpp-concepts-generic.md]
---

A **lambda expression** (*Lambda-Ausdruck*, colloquially "lambda") is a local, anonymous [[concepts/function-objects|function object]] that can access objects from its surrounding environment.

## Problem it solves

Writing a named [[concepts/function-objects|functor]] class just to pass a small, one-off operation to an [[algorithms/stl-algorithms|algorithm]] like `for_each` or `sort` is verbose. Lambda expressions let such an operation be written inline, at the call site, while still behaving exactly like a function object — including the ability to capture and carry state from its environment.

## Lambda expressions are syntactic sugar for functors

Every lambda expression defines an anonymous class with a unique type, the **Closure Type**, and represents an object of this class, the **closure object** or *Closure*. The call operator `operator()` is overloaded correspondingly to the lambda's body.

```cpp
[&](int a){return a<x;}
```

Here the lambda introduction `[&]` accesses local variables of the environment (here `x`) via references. The lambda introduction supplies the call parameters of the Closure Type's (hidden) constructor.

## Syntax of lambda expressions

```
[capture] (parameter-list) mutable noexcept -> return-type { body }
```

- **capture** — the *lambda introduction* (*Lambda-Einführung*); the call parameters of the Closure Type's constructor. `[]` = no access to local environment; `[=]` = access by copy; `[&]` = access by reference; `[=,&var]` = everything by copy except `var`, which is by reference.
- **(parameter-list)** — declarations of the function parameters, if any exist.
- **mutable** (optional) — non-reference variables captured in the introduction are `const` by default inside the body, unless `mutable` is specified.
- **noexcept** (optional) — declares that the function does not throw an exception.
- **-> return-type** (optional) — without a trailing return type, the return type is deduced from the type of the return expression, or is `void` if there is no return statement.

## 0.5.12.1 Lambda introductions (capture clauses)

Lambda introductions with and without a capture list (CL, *Erfassungsliste*, EL):

| Form | Meaning |
|---|---|
| `[ ]` | captures no local environment variables |
| `[EL]` | explicit capture of named local variables by value; by reference if the name is preceded by `&`; may contain `this` and names followed by `...` |
| `[& ]` | implicit capture of **all** local environment variables by reference |
| `[= ]` | implicit capture of **all** local environment variables by value (copy) |
| `[&,EL]` | implicit by reference; explicit names in `EL` by value; `&` is **not** allowed before those explicit names; may contain `this` (always captured as reference) |
| `[=,EL]` | implicit by value; `&` **must** precede all explicit names in `EL`; must **not** contain `this` |

## 0.5.12.2 Lambda expression and functor

Example (source: Stroustrup), printing elements of a vector that are divisible by `m`:

```cpp
// v[i] an os ausgeben, wenn v[i]%m==0
void print_modulo(const vector<int>& v, ostream& os, int m){
  for_each(begin(v),end(v),[&os,m](int x) {if(x%m==0) os<<x<<'\n';} );
}
```

Named lambda expression (*Benannter Lambda-Ausdruck*) — storing the lambda in a named variable via `auto` before passing it on:

```cpp
// Benannter Lambda-Ausdruck
void print_modulo(const vector<int>& v, ostream& os, int m){
  auto Modulo_print = [&os,m](int x) {if(x%m==0) os<<x<<'\n';};
  for_each(begin(v),end(v), Modulo_print); // Benannter Lambda-Ausdruck
}
```

Equivalent function object **without** a lambda expression — this is the compiler-generated shape a lambda desugars to:

```cpp
// Äquivalentes Funktionsobjekt ohne Lambda-Ausdruck
class Modulo_print {
ostream& os; int m;
public:
Modulo_print(ostream& s, int mm) :os(s), m(mm) {}
void operator()(int x) const{ if (x%m==0) os << x << '\n'; }
};
void print_modulo(const vector<int>& v, ostream& os, int m){
for_each(begin(v), end(v), Modulo_print{os,m}); } // Aufruf des Funktors
```

The capture-by-reference `os` becomes a reference member; the capture-by-value `m` becomes a plain value member; the constructor parameters correspond to the lambda introduction's captured names; `operator()` is `const` by default (matching the "captures are const unless `mutable`" rule above), and takes the lambda's declared parameter list.

## Generic lambdas

- `auto` is allowed as the type of a lambda parameter.
- A generic lambda behaves like a template function: the compiler generates an anonymous class whose call operator `operator()` is itself overloaded as a function template, inline.

```cpp
auto twice = [](auto a){return a+a; };
cout << twice(7) << endl;     // 14
cout << twice("go") << endl;  // gogo
[](){ cout << "Direkter Aufruf" << endl; } ();
```

- `twice` works for any type supporting `operator+`, just as a template function would (see [[concepts/templates]]).
- A lambda can also be invoked immediately at its definition site (the last line above: *Direkter Aufruf*, direct call).
- In the capture clause, new local variables and references can additionally be *declared*, with their type deduced from the initializer:

```cpp
int   n = 10;
auto lf = [&n, max=n+90]()->int{...};  // max erhält den Typ int
```

## Numbered pseudocode: lambda-to-closure desugaring

```
1. given lambda expression: [capture-list](params) -> R { body }
2. compiler generates an anonymous class C with:
3.     one member variable per captured name
4.         - captured by value  -> stored as a value member, initialized from the enclosing scope
5.         - captured by reference -> stored as a reference member, bound to the enclosing variable
6.     a (hidden) constructor taking the captured values/references as parameters
7.     operator()(params) -> R, marked const unless 'mutable' was specified
8.         - if any parameter type is 'auto', operator() is generated as a function template
9. the lambda expression itself evaluates to a temporary object (the Closure) of type C,
10.    constructed with the captured values/references as constructor arguments
```

## Mermaid: lambda → generated closure class

```mermaid
classDiagram
    class LambdaExpression {
        "[&os, m](int x) { if (x%m==0) os << x; }"
    }
    class ClosureType_ModuloPrint {
        -ostream& os
        -int m
        +ClosureType_ModuloPrint(ostream& s, int mm)
        +operator()(int x) const
    }
    LambdaExpression ..> ClosureType_ModuloPrint : compiler generates
    note for ClosureType_ModuloPrint "capture [&os, m] becomes\nconstructor params + members;\noperator() body = lambda body"
```

## Table of capture forms

| Capture | By value | By reference | Notes |
|---|---|---|---|
| `[]` | — | — | no access to enclosing scope |
| `[=]` | all used names | — | implicit copy capture |
| `[&]` | — | all used names | implicit reference capture |
| `[x]` | `x` only | — | explicit value capture of `x` |
| `[&x]` | — | `x` only | explicit reference capture of `x` |
| `[=, &x]` | all except `x` | `x` | mixed: default copy, `x` by reference |
| `[&, x]` | `x` | all except `x` | mixed: default reference, `x` by value; no `&` allowed before `x` here |
| `[this]` / implicit in `[&]`, `[&,x]` | — | `this` (always as reference-like access) | `[=,EL]` must not contain `this` |

## Consequences / trade-offs

- Lambdas remove the boilerplate of hand-writing a functor class for simple, local operations, while being exactly as powerful (state-carrying via captures, usable anywhere a [[concepts/function-objects|function object]] is expected, e.g. in [[algorithms/stl-algorithms|for_each/transform]]).
- Generic lambdas (`auto` parameters) give template-like genericity without writing an explicit template, at the cost of the usual deduction surprises (e.g. implicit conversions per call site).
- By-reference capture (`[&]`) risks dangling references if the closure outlives the captured variables — a concern shared with returning references in general (see [[concepts/pointers-and-references]]).

## Misuse & anti-patterns

- Capturing by reference (`[&]`) in a lambda that is stored and invoked after its enclosing scope has ended (e.g. stored for later execution in another [[concepts/multithreading|thread]]) leads to dangling references.
- Mixing `[=,&x]` ordering incorrectly (e.g. putting `&` before explicit names in a `[=, EL]` form, or omitting it in a `[&, EL]` form) is rejected by the grammar rules above.
- Assuming captured-by-value variables are mutable inside the lambda body without `mutable` — they are implicitly `const`.

## Related

- [[concepts/function-objects]]
- [[algorithms/stl-algorithms]]
- [[concepts/templates]]
- [[concepts/pointers-and-references]]
- [[concepts/multithreading]]
- [[concepts/value-categories]]

## Sources

- [[sources/grigat-cpp-concepts-generic]] §0.5.12.1, §0.5.12.2
