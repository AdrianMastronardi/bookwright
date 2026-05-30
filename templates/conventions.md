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

**Context.** `outline.md` gathers working quotations from sources before drafting begins. Each quotation must be bound to its bibliography entry unambiguously so that (a) renames of citation keys in `references.bib` surface immediately as broken references in `outline.md` rather than rotting silently, and (b) the draft editor can copy the citation marker into the rendered chapter without having to identify the citekey from prose attribution. The quote and the analytical note about it should also travel together: a note that drifts away from its quote during chapter-card reordering or copy-paste loses its referent. Free-form attribution in the analytical note ("Author argues...", "as shown in Year") is welcome, but it cannot replace the marker.

**Decision.** Every working quotation in `outline.md` is introduced by a pandoc-citeproc marker on the block-quote line, before the quoted text, and is followed by an analytical note on a `>` continuation line inside the same block-quote. The note is prefixed with the literal label `Analytical note:` so it can be located mechanically (grep, citation linter):

    > [@citekey, p. X] "Quoted passage."
    >
    > Analytical note: how this quote lands in the chapter argument.

The analytical note may span several paragraphs; each additional paragraph is introduced by another `>` continuation line and continues without the label. The note stays inside the block-quote so it remains co-located with its quote when chapter cards are reordered or copy-pasted.

Marker variants:

- Page locator dropped for whole-work citations: `> [@citekey] "..."`
- Verse: `> [@citekey, l. X] "..."`
- Online sources without pagination: `> [@citekey] "..."`
- Scan whose printed page is not yet verified: `> [@citekey, scan p. X, printed page TBD] "..."`
- Working-paper version pending replacement by the published page: `> [@citekey, working paper p. X, published page TBD] "..."`

When a TBD qualifier is resolved, update the marker in place and remove the qualifier.

**Consequences.** Renaming a citekey in `references.bib` is a single grep operation: `grep "\[@oldkey" outline.md` finds every dependent quotation. The draft editor (role 1) can refuse to draft from chapter cards whose working quotations lack markers. Co-locating the analytical note inside the block-quote keeps quote and note bound through chapter-card reordering, copy-paste, and section migrations. A future citation linter, if the project chooses to add one, can validate marker presence and citekey resolution mechanically.

## CONV-003 · Chapter file naming

**Status:** Accepted · {{TODAY}}

**Context.** Pandoc consumes chapter files in alphabetical order when building the full book, and the build (Makefile or equivalent) relies on that order. A naming scheme that sorts correctly across part dividers and chapters is therefore mandatory. A flat scheme with a single global sequence number (`NN-slug.md`) makes insertion and reordering painful: adding a chapter early in the book forces renaming every subsequent file. A hierarchical scheme `P.C-slug.md` (grouping, then chapter-within-grouping) makes the book's structure visible in the filesystem and keeps identifiers stable across edits within a grouping.

**Decision.** Chapter files in the chapters directory follow the pattern `P.C-slug.md`, where:

- `P` is the grouping number. Main-matter parts take consecutive numbers (`1`, `2`, …); reserve `0` for front matter that follows the title/copyright/ToC (preface, etc.), and reserve numbers above the last main part for back matter (acknowledgments, about the author) and the bibliography. The mapping of `P` → grouping is project-specific and documented in `toc.md`.
- `C` is the chapter number within the grouping. **Reserve `0` for the part divider** — the file that contains only the part-title command and renders as the part-title page. Groupings that have **no part divider** (front matter, back matter, bibliography) start at `1`. Use a single digit when the grouping has nine or fewer entries; pad to two digits (`01`, `02`, …) only once a grouping grows to ten or more.
- `slug` is lowercase ASCII with hyphens, derived from a stable short form of the chapter title.

Illustrative names:

- `0.1-preface.md` — front matter (no part divider; numbering starts at 1).
- `1.0-<part-i-title>.md` — Part I divider (contains only the part-title command).
- `1.1-<first-chapter>.md` — Part I, chapter 1.
- `2.0-<part-ii-title>.md` — Part II divider.
- `5.1-acknowledgments.md` — back matter (no part divider).
- `6.1-bibliography.md` — bibliography (no part divider).

Part divider files contain a single part-title command (e.g. `\part{...}` in a LaTeX build) plus a `<!-- markdownlint-disable MD041 -->` header, because the file does not start with an H1 heading. Part-page styling and the flush-left placement of part-level front/back-matter entries (Preface, Acknowledgments, About the Author) in the TOC are enforced once in the project's LaTeX template, not duplicated in each file. Record the exact macros the project uses in `toc.md` or the template alongside the grouping map.

**Consequences.** Build order is stable and visible at a glance via a directory listing, and the hierarchy of the book is mirrored in the filesystem. Inserting a chapter within a grouping requires renumbering only within that grouping. Lexicographic sort handles up to nine chapters per grouping with single-digit numbering; switch to two-digit padding within a grouping once it grows to ten or more. When a chapter is renamed, update the file name and its cross-references in `outline.md` in the same revision.

## CONV-004 · Bibliography is a single BibTeX file

**Status:** Accepted · {{TODAY}}

**Context.** The project's bibliography is the authoritative source for every citation. Splitting it across multiple files makes deduplication and cross-checking harder, and pandoc-citeproc handles a single large file efficiently.

**Decision.** All bibliographic entries live in `references.bib` at the project root. No per-chapter bibliography files. Entries are sorted by citation key (alphabetical). Comments and section dividers inside `references.bib` are permitted for working organization but do not affect the rendered bibliography, which pandoc-citeproc emits as a single alphabetized list. The rendered bibliography in the book is the rendered form, not the source order.

**Consequences.** Adding a citation requires editing one file. Citation keys are guaranteed unique across the whole project. Working notes inside the BibTeX file are stripped at render time.

## CONV-005 · Citation keys in references.bib

**Status:** Accepted · {{TODAY}}

**Context.** Pandoc-citeproc keys must be unique, must be stable across the project's lifetime, and must be readable at the point of citation in prose. Author surname plus year is unique often enough but collides when the same author publishes multiple works in a year; adding a keyword fragment resolves collisions and makes the key self-describing.

**Decision.** Citation keys take the form `surnameYEARkeyword`, all lowercase ASCII with no accents, where `keyword` is the first significant word of the title (skipping articles). Generic examples: `surname2002keyword`, `othersurname2021keyword`. Authors with multiple works in the same year disambiguate by keyword (`surname1955notes`, `surname1963fire`, `surname1998collected`). For coauthored works, use the first listed author's surname.

**Consequences.** Keys are stable identifiers that survive title edits. Multi-author works do not encode the second author in the key. Edited volumes and book chapters use the editor's surname when there is no single author. The reference apparatus in `references.bib` is the authority — if a citation key used in prose does not resolve there, the citation fails the build. This convention is the long-form statement of the citation-key policy noted in the `references.bib` header (`firstcreatorYYYYshorttitle`); the two must stay consistent.

## CONV-006 · BibTeX entry formatting in references.bib

**Status:** Accepted · {{TODAY}}

**Context.** `references.bib` accumulates citations across the project's lifetime. Machine-generated BibTeX exports adopt varied formatting (flush `field={value}` with no trailing comma on the last field), and hand-added entries drift toward mixed conventions. The accumulated inconsistency is harmless to the build (all modern parsers — `bibtex`, `biber`, `pandoc-citeproc` — accept any of these styles) but hurts diff readability and creates an "add field, forget comma" failure mode that no parser warns about. A consistent style applied to every entry makes additions safe to write line-by-line and keeps `git blame` precise.

**Decision.** Two formatting rules for every entry in `references.bib`:

1. **Single-space around `=`.** Each field line uses the form `  fieldname = {value},` rather than `  fieldname={value},`. The space on each side of `=` is the convention of the original Patashnik documentation and the biblatex manual; it is more readable than the flush form, especially for entries with many fields.
2. **Trailing comma on the last field.** Every field line, including the last one before the closing `}`, ends with a comma. Adding a new field is therefore a single-line diff that does not modify the surrounding lines, and `git blame` attributes each field to the commit that added it rather than to the commit that adjusted the previous line's comma.

Field-name alignment (`  fieldname     = {value},`) is *not* part of this convention. Aligned formatting is more readable for entries with many fields but breaks every time a field with a longer name is added; the maintenance cost is real and no widely available BibTeX linter restores alignment automatically. Single-space is the balance the project adopts.

**Consequences.** New entries follow the convention from the start. If a project inherits entries in another style (machine-generated exports, for example), bring them into compliance in a single pass — a short script that converts `  fieldname={...}` to `  fieldname = {...},` line by line does this safely — and record that pass in `CHANGELOG.md`. Pandoc-citeproc renders identically either way, so this is a source-side convention with no rendering impact. If a future BibTeX linter is added to the build, this is the format it should enforce.

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
