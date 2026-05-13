# Source Conventions

<!--
Rules for writing the markdown source of {{PROJECT_TITLE}}. These rules
are mechanical: they govern how the source is structured, named, and
labeled, not what the prose says or how it reads. The voice and style of
the written content live in voice.md.

Each convention is recorded as a numbered entry with a stable identifier
(CONV-001, CONV-002, ...) and follows a fixed structure: Status,
Context, Decision, Consequences. Identifiers are stable: they are never
reused or renumbered. The order of entries in this file may be changed
for readability without affecting identifiers. New conventions take the
next available identifier.
-->

## CONV-001 · Line wrapping in paragraphs

**Status:** Accepted · {{TODAY}}

**Context.** Hard line breaks at fixed columns are a relic of fixed-width terminals. Modern editors handle long lines transparently with soft wrapping, modern diff tools highlight changes within long lines, and the markdown engine reflows everything on render. Hard wrapping creates spurious diffs whenever a sentence is edited and serves no rendering purpose.

**Decision.** Do not break paragraph lines in the source. One paragraph is one source line. The rule applies to prose paragraphs only. Tables, code blocks, footnote definitions, list items, raw LaTeX environments, and any other construct that requires structural newlines remain wrapped per their own syntax.

**Consequences.** Diffs become accurate at the prose level. Word-level search-and-replace works reliably across whole sentences. The source is harder to read in editors that lack soft wrapping; this is an acceptable trade given that all modern editors support soft wrapping by default.

<!--
Add further conventions as the project requires them. Common examples
in long-form projects:

- Bibliography database organization and citation keys
- Footnote labels (a scheme that prevents cross-file collisions in
  multi-chapter pandoc builds)
- Version metadata in changelog entries
- UTF-8 versus LaTeX accent macros in references.bib
- Index entry marking in source

When you add a convention, use the next available CONV-NNN number, and
follow the same Status / Context / Decision / Consequences structure.
-->
