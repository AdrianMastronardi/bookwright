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

## CONV-002 · Working quotation format in outline.md

**Status:** Accepted · {{TODAY}}

**Context.** `outline.md` gathers working quotations from sources before drafting begins. Each quotation must be bound to its bibliography entry unambiguously so that (a) renames of citation keys in `references.bib` surface immediately as broken references in `outline.md` rather than rotting silently, and (b) the draft editor can copy the citation marker into the rendered chapter without having to identify the citekey from prose attribution. Free-form attribution in the surrounding analytical note ("Author argues...", "as shown in Year") is welcome, but it cannot replace the marker.

**Decision.** Every working quotation in `outline.md` is introduced by a pandoc-citeproc marker on the block-quote line, before the quoted text:

    > [@citekey, p. X] "Quoted passage."

Variants:

- Page locator dropped for whole-work citations: `> [@citekey] "..."`
- Verse: `> [@citekey, l. X] "..."`
- Online sources without pagination: `> [@citekey] "..."`
- Scan whose printed page is not yet verified: `> [@citekey, scan p. X, printed page TBD] "..."`
- Working-paper version pending replacement by the published page: `> [@citekey, working paper p. X, published page TBD] "..."`

When a TBD qualifier is resolved, update the marker in place and remove the qualifier.

Analytical notes about the quote follow the block-quote on subsequent lines and are not a substitute for the marker.

**Consequences.** Renaming a citekey in `references.bib` is a single grep operation: `grep "\[@oldkey" outline.md` finds every dependent quotation. The draft editor (role 1) can refuse to draft from chapter cards whose working quotations lack markers. A future citation linter, if the project chooses to add one, can validate marker presence and citekey resolution mechanically.

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
