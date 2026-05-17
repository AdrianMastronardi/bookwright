# Changelog

All notable changes to this project are documented in this file.

The format is loosely adapted from [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and the project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

Entries are grouped by area, in this fixed order. Sections with no entries for a given version are omitted.

- **Skill** covers the Claude-facing logic of the skill: `SKILL.md`, `workflow.md`, and `bootstrap.md`.
- **Templates** covers the files in `templates/` that the bootstrap instantiates into new projects.
- **Documentation** covers human-facing project documentation: `README.md` and `CONTRIBUTING.md`.
- **Infrastructure** covers licensing, repository plumbing, and build or release machinery: `LICENSE`, `.gitignore`, and similar.

Within each section, entries are sorted in case-insensitive alphabetical order by filename.

## [0.1.2] - 2026-05-17

Two changes in this batch.

First, a new editorial role for Phase 5 (Outline): `role-0-outliner.md`. The role takes a single source document and produces a working markdown file with a verified BibTeX entry, per-chapter working quotations bound to `CONV-002` markers, an optional quantitative appendix, an optional conceptual glossary, and editor notes. The author then commits the parts into `references.bib` and the affected chapter cards in `outline.md`. This formalizes a workflow that previously had to be improvised once per source: bibliography acquisition feeds outlining feeds drafting, and the outliner is the bridge between the first two.

Second, `CONV-002` is revised so that the analytical note about each working quotation lives inside the same block-quote as the quote, separated by a `>` continuation line and prefixed with the literal label `Analytical note:`. Previously the note lived on free lines after the block-quote with no label, which let quote and note drift apart during chapter-card reordering or copy-paste and gave a future linter nothing to anchor on. The new placement co-locates quote and note, and the label makes notes grep-able. `outline.md` examples, the new `role-0-outliner.md`, and the `role-1-draft-editor.md` precondition all use the revised format throughout.

### Skill

- `bootstrap.md`: Step 3 batch-generation step extended to include `role-0-outliner.md` alongside the other three role files. The role's outline-phase use is described inline so Step 3 is self-documenting.
- `SKILL.md`: file list extended with `templates/role-0-outliner.md`. The "What the skill does on invocation" entry for editorial roles now lists `role-0-outliner.md` first, and the operational-modes section names source extraction as one of the things the user can ask for inside Resume mode.
- `workflow.md`: Phase 5 (Outline) describes `role-0-outliner.md` as the optional per-source role authors can invoke to keep extraction discipline consistent across a long corpus.

### Templates

- `templates/conventions.md`: `CONV-002` Decision section revised to specify that the analytical note about each working quotation lives inside the block-quote on a `>` continuation line and is prefixed with the literal label `Analytical note:`; multi-paragraph notes permitted via additional `>` lines, with the label appearing only on the first paragraph. Context paragraph notes the co-location requirement; Consequences paragraph adds that co-location keeps quote and note bound through chapter-card reordering and copy-paste. Marker variants and TBD-resolution policy are unchanged.
- `templates/outline.md`: four examples and one HTML comment brought into compliance with the revised `CONV-002`. "Quotation marker format" subsection example extended from marker-only to the full marker-plus-`Analytical note:` form. "Author commentary on quotations" subsection example updated to the in-block-quote placement with the literal label. Per-chapter card "Working Quotations" block: the HTML-comment brief, the Do example, and the optional-cluster-label pattern all updated. The "Don't" form is unchanged — its point (missing marker) is independent of note placement.
- `templates/role-0-outliner.md`: new generic role file with placeholders for project brief and primary language. Sections: Identity and Mission, Inputs You Need, Output and Integration, Extraction Logic (seven steps: BibTeX entry, TOC mapping, end-to-end read and selection, CONV-002 quotation format with the analytical note inside the block-quote and locator variants, optional quantitative appendix, optional conceptual glossary, editor notes), Editorial Stance, What Not to Do, Response Format with the output skeleton, Pre-delivery Checklist, Final Reminder. The role consults `manifesto.md`, `voice.md`, `toc.md`, `outline.md`, `references.bib`, and `conventions.md`; its output respects the revised `CONV-002` so chapter cards advanced via the outliner pass the draft-editor handoff in `role-1-draft-editor.md`.
- `templates/role-1-draft-editor.md`: "Citation discipline (CONV-002)" precondition in "Inputs You Need" extended with a second paragraph covering the new in-block-quote analytical note. The paragraph tells the drafter the note is guidance (how the quote is meant to land in the chapter argument), not chapter prose, and frames the choice of integration form — verbatim, paraphrased, abridged, or brief citation — as the drafter's editorial judgment. The invariant is that the citation marker accompanies the source whatever form it takes, and the `Analytical note: …` line never appears in the chapter prose.

### Documentation

- `CLAUDE.md`: "Pipeline architecture" extended with a paragraph noting that Phase 5 has an optional per-source role, `role-0-outliner.md`, that the author invokes one source at a time. The paragraph explicitly states that the `[DRAFT-READY]` gate remains per-chapter; role-0 does not participate in that gate.
- `README.md`: file tree under `templates/` extended with `role-0-outliner.md` in alphabetical order between `references.bib` and `role-1-draft-editor.md`.

## [0.1.1] - 2026-05-14

This batch closes a citation-discipline gap surfaced by auditing a real consumer project: `outline.md` declared a pandoc-citeproc quotation-marker format in its own working-conventions section, but the format had no anchor in the project's authoritative ledger (`conventions.md`), no enforcement in the chapter-card template, and no precondition check at the draft-editor handoff. The result was that working quotations drifted to free-form prose attribution ("Author argues...", `**X integration (Y):**`), citekey renames in `references.bib` no longer surfaced as broken references in `outline.md`, and typos in source-author attribution could propagate to the draft undetected.

### Templates

- `templates/conventions.md`: new `CONV-002 · Working quotation format in outline.md`. Records the pandoc-citeproc marker rule as project law in the authoritative ledger, with locator variants (whole-work, verse, online, scan-pending, working-paper-pending) and the TBD-resolution policy. `CONV-001` and `CONV-002` are now the seeded conventions for new projects.
- `templates/outline.md`: top-of-file "Quotation marker format" subsection rewritten to reference `CONV-002` as authoritative rather than redeclaring the rule. Per-chapter "Working Quotations" block refactored: the `**[Thematic cluster label].**` header pattern (which invited prose-attribution drift) is replaced by a `Do` / `Don't` contrast block followed by an italicised cluster-label form and analytical-note lines following the block-quote. The meta-instruction is explicit that prose attribution can accompany a marker but cannot replace it.
- `templates/role-1-draft-editor.md`: new "Citation discipline (CONV-002)" precondition under "Inputs You Need." Before drafting, the role verifies that every working quotation in the chapter card begins with a `[@citekey, p. X]` marker; chapter cards with unbound quotations are returned to the research/quotation-gathering phase rather than drafted from.
- `templates/role-2-development-line-editor.md`: new "Citation Integrity (CONV-002)" subsection under "Developmental Responsibilities." The development pass verifies that every in-prose citation in the draft resolves to a citekey present in `references.bib`. Scope is internal integrity between draft and bibliography; cross-checking against `outline.md` is explicitly out of scope (author responsibility).

## [0.1.0] - 2026-05-13

Initial release. Six-phase pipeline for long-form nonfiction (manifesto, voice, structure, bibliography, outline, writing) packaged as a Claude Code skill. The bootstrap procedure interviews the author through two completeness gates (manifesto, voice) before generating any artifact, then scaffolds the rest of the project's files. Three editorial roles (draft, development-and-line, copy) drive the writing phase.

### Skill

- `SKILL.md`: Claude-facing skill manifest. Declares trigger conditions (new project bootstrap, resume work, run editorial role), three operational modes, the mandatory-interview override that forbids drafting `manifesto.md` or `voice.md` from "reasonable defaults" and instructs Claude to override session-level "no clarifying questions" preferences inside the bootstrap, the substitution-variable set used by the bootstrap, and the relative-path conventions inside the skill versus inside an instantiated project.
- `bootstrap.md`: bootstrap protocol with two completeness gates. Opens with an operating-principle section establishing that the procedure is an interview, not an inference task, and that session-level "no clarifying questions" preferences must be overridden for its duration. Step 0 reads the user's natural-language seed; Step 1 runs the manifesto interview (ten-item checklist with three-to-four-question blocks, summary, and explicit confirmation before file generation); Step 2 runs the voice interview (ten-item checklist with the same rhythm); Step 3 scaffolds `toc.md`, `references.bib`, `outline.md`, `conventions.md`, and the three role files; Step 4 offers optional deepening. The failure-modes section explicitly forbids drafting from "reasonable defaults" and honoring "no clarifying questions" preferences inside the bootstrap. Includes a note that the example phrases are in English while Claude conducts the actual interview in the user's language.
- `workflow.md`: human-facing description of the pipeline. Documents each of the six phases with its exit criterion, the iteration patterns between phases (TOC drift, bibliography accretion, manifesto refinement), the gates between phases, and the relationships between artifacts.

### Templates

- `templates/conventions.md`: ADR-style conventions file seeded with `CONV-001` (line wrapping in paragraphs). Identifiers are stable and never reused.
- `templates/manifesto.md`: ten-section manifesto template with HTML-comment briefs for each section. Substitution variables for project title, subtitle, genre, gap argument, audience treatments, scope, methodological model, research division, priority sources, format and distribution, positioning against existing work, and decisions taken.
- `templates/outline.md`: chapter-card template with status flags (`[SKELETON]` through `[FINAL]`), per-chapter fields for function, argument, narrative beats, cross-references, source integration, working quotations, and gaps-and-queries. Top-of-file sections for Core Thesis, Method and Voice Anchors, Evidence Ladder, Source Notes, and Working Conventions. Closing sections for Citation Scaffolding (pending slots) and Research Priorities.
- `templates/references.bib`: empty BibTeX database with a header comment documenting the citation-key convention (`firstcreatorYYYYshorttitle`, lowercase ASCII, no accents) and the UTF-8 policy.
- `templates/role-1-draft-editor.md`: generic draft-editor role file with placeholders for project-specific register, evidence rules, voice reminders, terminology, and source conventions. Consults `manifesto.md`, `voice.md`, `toc.md`, `conventions.md`, the chapter card in `outline.md`, and `references.bib`.
- `templates/role-2-development-line-editor.md`: generic development-line-editor role file combining developmental and line-editing passes, with placeholders for project-specific quality standard, evidence flags, technical integrity, key distinctions, rhetoric-to-avoid, and punctuation notes. Consults the same six files.
- `templates/role-3-copy-editor.md`: generic copy-editor role file with placeholders for voice qualities, spelling rules, quotation rules, dash rules, number-and-date rules, terminology, source-convention checklist, and specialized-apparatus checks. Consults the same six files.
- `templates/toc.md`: minimal scaffold for the project table of contents with one-sentence function statements per chapter.
- `templates/voice.md`: twelve-section voice and style guide template with HTML-comment briefs. Substitution variables for primary language and variant, spelling and punctuation rules, foreign-vocabulary treatment, personal-name treatment, place-name treatment, institutional-name treatment, citation system, footnote usage, bibliography structure, archival citation rules, foreign-source citation rules, register, grammatical voice, numbers and dates, field-specific standards, specialized apparatus, reproduction standards, indexes, length and pace, author's voice, and editorial process.

### Documentation

- `CHANGELOG.md`: this file. Keep-a-Changelog adapted format with four fixed sections (Skill, Templates, Documentation, Infrastructure) and case-insensitive alphabetical ordering by filename within each section.
- `CONTRIBUTING.md`: scope statement (what fits and what does not), pre-PR issue convention, what a good change looks like, local testing procedure, and license-of-contributions clause.
- `README.md`: project description focused on long-form nonfiction, three-commitment philosophy (decisions before drafting, outline as meeting point, three editorial passes), who-it-is-for and who-it-is-not-for sections, six-phase summary, installation instructions, usage instructions clarifying that `/bookwright` is a Claude Code slash command invoked inside an interactive session, after-bootstrap reminder that artifacts are first drafts the author owns, alphabetical case-insensitive file tree, and license-and-contributions section with a reference to the changelog.

### Infrastructure

- `.gitignore`: editor swap files and macOS metadata.
- `LICENSE`: MIT License, copyright 2026 Adrian Mastronardi.
