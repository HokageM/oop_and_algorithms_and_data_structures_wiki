---
title: "Grigat — UML 2.0 and Design Patterns"
type: source
tags: [source, lecture-script, uml, design-patterns, german]
de: Vorlesungsskript — UML und Entwurfsmuster
author: Prof. Dr.-Ing. Rolf-Rainer Grigat (TUHH)
language: de
file: raw/oop_uml_and_design_patterns.pdf
pages: 40
printed_pages: 173-212
sections: 0.6-0.7
ingested: 2026-10-12
status: ingested
---

# Grigat — UML 2.0 and Design Patterns

Part three of the continuous TUHH lecture script. Picks up directly where
[[sources/grigat-cpp-concepts-generic]] ends (printed p. 172) and runs to printed
p. 212. Scanned, no text layer; transcribed from page images.

## Scope

| § | Title | Printed pp. |
|---|---|---|
| 0.6 | UML 2.0 | 173–192 |
| 0.6.1 | Overview, purpose, forward/reverse/round-trip engineering | 173–175 |
| 0.6.2 | Klassendiagramme — notation in depth | 176–186 |
| 0.6.3 | Other diagram types (use case, activity, state machine, interaction) | 186–188 |
| 0.7 | Entwurfsmuster (design patterns) | 188–208 |
| 0.7.1 | The pattern concept, GoF, classification | 188–190 |
| 0.7.2 | Singleton | 190–192 |
| 0.7.3 | Adapter (Wrapper) | 192–196 |
| 0.7.4 | Proxy | 196–200 |
| 0.7.5 | Strategy | 200–204 |
| 0.7.6 | Observer | 204–208 |
| — | Versionsverwaltung (SVN, Mercurial) | 208–212 |

## Why this source matters

It is the first source in the wiki that is primarily about **design** rather than
language mechanics. The C++ sources explain what the language can express; this
one explains what to express. The five patterns it covers are all demonstrated
with the same running example domain (`CAuto`, `CHupe`, `CTaxi`, `CAmpel`) used
in part I, so the patterns land on classes the wiki already documents.

It is also overwhelmingly diagrammatic — roughly two thirds of the pages are UML
figures. That made it the best fit for the Mermaid convention in `CLAUDE.md`.

## Key takeaways

- **Class-diagram notation is the bulk of §0.6.** The existing
  [[concepts/uml-class-diagram]] page was a stub covering only the three-compartment
  box and visibility markers; this source expanded it into the full notation
  reference (associations, navigability, multiplicity, generalization sets,
  realization, parameterized classes, dependency, notes).
- **Patterns are presented as named solutions with consequences**, following the
  GoF four-part structure. The script is explicit that a pattern is a trade-off,
  not a recipe.
- **The Proxy chapter doubles as a smart-pointer derivation.** `CAutoZeiger` is a
  hand-written proxy that does what [[concepts/smart-pointers]] does in the standard
  library — which connects this source back to §0.5.4.
- **Observer is the one pattern given a sequence diagram**, making it the natural
  home for [[concepts/uml-sequence-diagram]]'s worked example.
- The closing version-control section is tooling, not theory, and is filed as a
  single page rather than split.

## Connections to earlier sources

| This source | Connects to |
|---|---|
| Class-diagram notation | [[concepts/uml-class-diagram]], [[concepts/class-and-object]] |
| Generalization/realization | [[concepts/inheritance]], [[concepts/abstract-class]] |
| Aggregation vs. composition | [[concepts/composition]] |
| Parameterized classes | [[concepts/templates]] |
| Singleton | [[concepts/static-members]] |
| Proxy | [[concepts/smart-pointers]], [[concepts/operator-overloading]] |
| Strategy | [[concepts/polymorphism]], [[concepts/function-objects]] |
| Observer | [[concepts/polymorphism]], [[concepts/inheritance]] |

## Pages created from this source

- [[concepts/uml-overview]]
- [[concepts/uml-sequence-diagram]]
- [[concepts/uml-use-case-diagram]]
- [[concepts/uml-activity-diagram]]
- [[concepts/uml-state-machine]]
- [[concepts/version-control]]
- [[patterns/design-patterns-overview]]
- [[patterns/singleton]]
- [[patterns/adapter]]
- [[patterns/proxy]]
- [[patterns/strategy]]
- [[patterns/observer]]

Substantially extended: [[concepts/uml-class-diagram]].

## Open questions

- §0.6.3 names use-case, activity, state-machine and interaction diagrams but gives
  each only a paragraph. The corresponding wiki pages are deliberately thin and
  flagged; a second source would fill them.
- Only five of the 23 GoF patterns are covered. Factory, Decorator, Command,
  Template Method and Composite are not treated.
- The version-control section predates the repository's own use of git and covers
  SVN and Mercurial instead.

## Related

- [[sources/grigat-cpp-concepts-generic]] — immediately precedes this part
- [[sources/grigat-java]] — immediately follows this part
- [[synthesis/oop-core-concepts]]
