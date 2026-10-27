---
title: Log
updated: 2026-10-12
---

# Log

Append-only. Newest entries at the bottom. See `../CLAUDE.md` §5.
Back to [[index]].

## [2026-10-12] schema | Wiki initialized
- Created: CLAUDE.md, index.md, log.md
- Created directories: raw/{textbooks,course,articles,assets}, wiki/{concepts,structures,algorithms,patterns,sources,synthesis}
- Scope: OOP + algorithms & data structures study notes; sources are textbook chapters, course material, and articles

## [2026-10-12] schema | German sources + scanned-PDF workflow
- Updated: CLAUDE.md — added "Language" rule (English pages, German terms preserved, `de:` frontmatter field) and "Scanned PDFs" rule (PyMuPDF render-to-image workflow, parallel transcription)

## [2026-10-12] ingest | Grigat — Teil I: Objektorientierte Programmierung (raw/oop_klassen.pdf)
- Source had no text layer; all 82 pages rendered to grayscale PNG and transcribed page-by-page
- Created: sources/grigat-oop-teil1.md
- Created 34 concept pages (type-declaration-definition, initialization-and-assignment,
  const-and-volatile, scope-and-storage-classes, type-aliases, complex-declarations,
  strings-cpp-vs-c, chrono-time-measurement, function-declarations, function-overloading,
  parameter-passing, pointers-and-references, modularization-and-build-pipeline,
  preprocessor-and-include-guards, namespaces, abstract-data-type, encapsulation,
  class-and-object, uml-class-diagram, member-functions, this-pointer, constructor,
  destructor, memory-model, static-members, friend, composition, inheritance,
  multiple-inheritance, access-modifiers, overriding-vs-overloading, abstract-class,
  polymorphism, vtable)
- Created: structures/stack.md, synthesis/oop-core-concepts.md
- Updated: index.md (37 pages catalogued)
- Link check: 37 pages, 0 broken wikilinks, 0 orphans, frontmatter present on all
- Note: code examples are C++ for this source, overriding the Python default in CLAUDE.md
- Open questions filed in synthesis/oop-core-concepts.md (smart pointers vs. virtual
  destructors; composition-over-inheritance; templates/generics)
- Remaining uningested sources in raw/: oop_algos_and_datastructures.pdf,
  oop_cpp_concepts_and_generic_programming.pdf, oop_graphs_dynamic_programing.pdf,
  oop_java.pdf, oop_trees_and_sorts.pdf, oop_uml_and_design_patterns.pdf

## [2026-10-12] schema | Mermaid diagrams and pseudocode now mandatory

- Trigger: user instruction "make sure for all pages to ingest pseudocode and mermaid
  diagrams where possible".
- CLAUDE.md: added a "Diagrams and pseudocode" section making a Mermaid diagram
  mandatory on every page whose subject has drawable structure, and numbered
  pseudocode mandatory for every described procedure.
- CLAUDE.md: both page templates revised to include Mermaid + pseudocode slots.
- CLAUDE.md: replaced the "Python by default" code-example rule with "follow the
  language of the source (currently C++)".
- Applies retroactively: the 36 pages from ingest 1 were retrofitted (see next entry).

## [2026-10-12] ingest | Grigat - C++-Konzepte und Generische Programmierung

- Source: raw/oop_cpp_concepts_and_generic_programing.pdf (90 pp., German, scanned,
  no text layer). Printed pages 83-172, sections 0.4-0.5.12. Same lecture script as
  ingest 1 - this is the continuation, not a separate work.
- Method: rendered all 90 pages to grayscale PNG at 100 dpi with PyMuPDF, transcribed
  by 5 parallel reader agents writing notes directly to files, then filed by 5 parallel
  writer agents against a shared page plan.
- Created: sources/grigat-cpp-concepts-generic.md
- Created 27 concept pages: operators-and-precedence, operator-overloading, cpp-streams,
  arrays-and-dynamic-memory, copy-constructor, assignment-operator, value-categories,
  move-semantics, assertions, type-traits, exceptions, type-conversions, templates,
  template-specialization, variadic-templates, standard-library, smart-pointers,
  big-o-notation, complexity-classes, stl-containers, iterators, iterator-traits,
  predicates, iterator-adapters, function-objects, multithreading, lambda-expressions
- Created 5 structure pages: vector, deque, list, set-and-map, unordered-containers
- Created 2 algorithm pages: postfix-evaluation, stl-algorithms
- Created synthesis/special-member-functions.md (copy/move/destructor as one
  resource-ownership problem)
- Updated synthesis/oop-core-concepts.md: two open questions from ingest 1 are now
  ANSWERED by this source (smart pointers; templates as compile-time polymorphism).
  Struck through rather than deleted, with links to the answering pages. This is the
  compounding the wiki is for.
- Retrofit: all 36 ingest-1 pages revisited to add Mermaid diagrams, pseudocode and
  cross-links to the new material.
- Updated: index.md (73 pages, 2 sources), new groupings for Generic programming,
  Concurrency and Complexity.
- Uncertainty flagged, not invented: one partially illegible annotation in
  concepts/function-objects.md is marked uncertain; concepts/iterator-traits.md omits
  a category-hierarchy diagram because the source notes do not contain that material.
- Remaining uningested sources in raw/: oop_algos_and_datastructures.pdf,
  oop_graphs_dynamic_programing.pdf, oop_java.pdf, oop_trees_and_sorts.pdf,
  oop_uml_and_design_patterns.pdf

## [2026-10-12] ingest | Grigat script, parts 3-7 (printed pp. 173-449)

Batch ingest of the five remaining sources, completing the script.

**Sources.** `oop_uml_and_design_patterns.pdf` (40 pp.), `oop_java.pdf` (44 pp.),
`oop_algos_and_datastructures.pdf` (84 pp.), `oop_trees_and_sorts.pdf` (59 pp.),
`oop_graphs_dynamic_programing.pdf` (50 pp.) - 272 scanned pages, no text layer.
Confirmed that all seven PDFs are one continuous script, printed pp. 1-449; built
a document map before filing anything.

**Process.** Rendered all 272 pages to 100 dpi grayscale PNG in one pass, then ran
13 reader agents in parallel (each writing its transcription to its own notes
file), then wrote a consolidated 75-page plan with exact link targets and
per-agent page ownership, then ran 9 writer agents in parallel. Zero cross-agent
link collisions and zero broken links resulted from the ownership rules.

**Produced.** 75 new pages: 6 UML, 6 design patterns (filling the previously empty
`patterns/`), 11 Java, 9 list/tree, 9 search structures, 7 string trees, 12
sorting, 7 graph, 6 DP/B-tree. Extended `concepts/uml-class-diagram` and
`structures/stack`. Wrote 5 source pages plus `synthesis/complexity-cheatsheet`
and `synthesis/choosing-a-data-structure` as the two cross-cutting hubs.

**Naming decision (do not merge).** `structures/list`, `set-and-map`,
`unordered-containers` and `vector` document the **STL containers**;
`structures/linked-list`, `set`, `dictionary` and `hash-table` document the
**ADTs and their implementations**. The split is deliberate and is recorded on
the source pages.

**Java** is the one non-C++ language in the wiki, per the CLAUDE.md rule that code
follows the language of the source. Every Java page carries a
"Compared with C++" section.

**Gaps recorded, not filled.** Printed p. 271 and pp. 440-443 are missing from the
scans. More importantly, **no shortest-path algorithm - no Dijkstra, no MST, no
Prim - appears anywhere in the 449 pages**, although section 0.14.4 foreshadows
them. Writers were explicitly instructed not to supply this from their own
knowledge; it is filed as an open question on `structures/graph` and
`algorithms/breadth-first-search`.

**State after ingest.** 153 pages, 7 sources, ~300 Mermaid diagrams.
0 broken links, 0 orphans, 0 pages missing frontmatter, 0 pages missing a diagram.
`index.md` rebuilt with new groupings for UML, Java, patterns, graphs, sorting,
string structures and dynamic programming.

## [2026-10-12] schema | index.md and log.md moved into wiki/

`index.md` and `log.md` now live inside `wiki/` rather than at the repository
root. They are wiki pages like any other, so the whole wiki layer is one
self-contained Obsidian vault: open `wiki/` and the graph view, backlinks and
`[[...]]` resolution all work without the vault containing `raw/` or the schema.
`CLAUDE.md` is now the only markdown file at the repository root, which also
keeps the agent-facing schema clearly outside the LLM-owned layer.

Wikilink targets were unaffected - they were already written relative to `wiki/`.
`CLAUDE.md` section 1 (directory layout), sections 4 and 5 (now `wiki/index.md`
and `wiki/log.md`) and the session-start checklist were updated to the new paths,
including the greppable-log tip, which is now
`grep "^## \[" wiki/log.md | tail -5`.

Also fixed in this pass: a UTF-8 BOM that had crept into `index.md`, three files
dated 2026-10-13 corrected to 2026-10-12, and the source author expanded from
"R.-R. Grigat" to the full "Prof. Dr.-Ing. Rolf-Rainer Grigat" across all seven
source pages and `index.md`.

State: 155 pages (153 content + index + log), 302 Mermaid diagrams,
0 broken links, 0 missing frontmatter.

## [2026-10-13] schema | Figure captions stay in German

Audited the wiki for untranslated German. Result: all prose, headings, tables,
diagram labels and pseudocode are English; German survives only as the `de:`
glossary field (153 of 155 pages), as italicised source quotations that always
carry an English gloss, and in two source-page titles that reproduce the
script's own German title.

One heading carried German with no gloss -
`concepts/standard-library.md` -> `Abbildung 12 - Komponenten der
Standardbibliothek`. Decision: leave it. A figure caption is a citation; it has
to match the printed script so the figure can be found. The `Language` section
of CLAUDE.md now states this explicitly, so a future session does not translate
captions away. Same section now also records the source-page title rule.
