<!--
This is the project outline. It is where research becomes drafting raw
material. For each chapter and section in toc.md, the outline records
the chapter's function, argument, narrative beats, source integration,
working quotations, and gaps. When a chapter's outline reaches DRAFT-
READY status (see Working Conventions below), the draft editor (role 1)
can begin without consulting any other artifact except manifesto.md,
voice.md, conventions.md, and the source files cited.

The outline is the project's central working file during research and
drafting. It is the longest artifact (typically the longest by a wide
margin). It evolves continuously.

Top-of-file orientation precedes the per-chapter cards.
-->

# Outline: {{PROJECT_TITLE}}

- **Subtitle:** {{SUBTITLE}}
- **Author:** {{AUTHOR}}
- **Linked artifacts:** `manifesto.md`, `voice.md`, `toc.md`, `references.bib`, `conventions.md`
- **Last revised:** {{TODAY}}

## How to use this file

The outline is a working document. Each chapter is represented as a
**chapter card** with a fixed structure:

1. **Status** — drafting readiness flag.
2. **Function in the book** — what the chapter does in the architecture.
3. **Argument** — the specific claim or distinction the chapter establishes.
4. **Narrative beats** — the moves the chapter makes, in order.
5. **Cross-references** — forward and backward dependencies.
6. **Source integration** — per-source notes about what each cited source provides and how to use it.
7. **Working Quotations** — verbatim passages clustered by analytical use.
8. **Gaps and Queries** — pending evidence, author decisions, unresolved questions.

Chapter cards are independent: a card can reach DRAFT-READY status without affecting other cards. The cards together form the working manuscript-in-waiting.

## Core Thesis

<!--
The book's central thesis, compressed to one to three paragraphs. This
mirrors manifesto.md §2 ("Why this project") but compressed to argument
form rather than positioning form. The Core Thesis appears in the
outline because it is the standard against which every chapter's
argument is checked.

When the manifesto's thesis evolves, update this section to match.
-->

{{CORE_THESIS}}

## Method and Voice Anchors

<!--
A one-paragraph compression of the manifesto's methodological model and
the voice document's register, written here so that the outline is
self-contained for drafting purposes.

This is not a summary of voice.md or manifesto.md; it is the operational
anchor a drafter needs to keep in mind while writing.
-->

{{METHOD_AND_VOICE_ANCHORS}}

## Evidence Ladder

<!--
A numbered list of source types the project uses, in descending order
of authority. Project-specific. Used by the drafter and by role-2 to
calibrate evidentiary caution.

Example (categories vary by discipline):

1. Primary authoritative sources (foundational documents of the field:
   laws, charters, canonical texts, treaties)
2. Primary institutional records (archives, official records,
   contemporary documents)
3. Contemporary diagnostic literature (reports, dispatches, period
   commentary)
4. Peer-reviewed synthesis (mainstream scholarship in the field)
5. Material or technical evidence (specimens, objects, direct
   observation)
6. Oral or testimonial evidence (interviews, oral history), always
   marked with confidence level
-->

{{EVIDENCE_LADDER}}

## Source Notes

<!--
Per-tricky-source treatment notes. Reserved for sources that require
special handling: scans with double-page issues, working-paper versions
of later-published articles, primary documents available only in
paraphrase, contested attributions, sources with reliability caveats.

Each note states:
- Which source it concerns
- What the handling issue is
- The project's editorial policy for that source until the issue is
  resolved

Sources that have no special handling do not need an entry here.
-->

{{SOURCE_NOTES}}

---

## Working Conventions for This File

<!--
This section is the same for every project. It documents the markup
conventions used inside the outline. Drafters and editors read it
before working with any chapter card.
-->

### Status flags

Each chapter card carries a **Status** line at the top. The status flag indicates how ready the chapter is for drafting:

- `[SKELETON]` — chapter exists in `toc.md`, but the outline card has only function and argument. No source integration yet.
- `[SOURCE-INTEGRATION]` — sources have been identified and per-source notes drafted. Quotations not yet gathered or only partially gathered.
- `[QUOTATIONS]` — working quotations gathered. Thematic clusters defined. Gaps and queries identified.
- `[DRAFT-READY]` — function, argument, beats, source integration, quotations, and cross-references are all in place. Major gaps and queries either resolved or explicitly registered. The draft editor can start.
- `[DRAFTED]` — chapter has been drafted (role 1 complete). Outline is now reference material for role-2 and role-3 passes.
- `[FINAL]` — chapter has cleared role 3. The outline card is preserved as research record but no longer active.

### Quotation marker format

Working quotations follow **CONV-002** in `conventions.md`. Every quotation begins with a pandoc-citeproc marker on the block-quote line, followed by an analytical note on a `>` continuation line inside the same block-quote, prefixed with the literal label `Analytical note:`:

```
> [@citekey, p. X] "Quoted passage."
>
> Analytical note: how this quote lands in the chapter argument.
```

`conventions.md` carries the canonical rule, the locator variants (verse, whole-work, online, scan-pending, working-paper-pending), the policy for resolving TBD qualifiers, and the multi-paragraph note rule. Do not redeclare or paraphrase the rule here; treat CONV-002 as authoritative.

A working quotation that lacks a marker is not draft-ready. The draft editor will refuse it (see `role-1-draft-editor.md`).

### Cross-references

Forward and backward dependencies between chapters are marked with arrows:

- `→ §X.Y` — this chapter sets up material developed in §X.Y.
- `← §X.Y` — this chapter requires material established in §X.Y.

Use the section number from `toc.md`. When chapters are renumbered, update cross-references in the same revision.

### Pending evidence and queries

- `[PENDING: brief description]` — evidence that is expected but not yet in hand. Specifies what is needed.
- `[QUERY: question]` — author decision required. Specifies what must be decided.

Both are searchable; both should be tracked and resolved before DRAFT-READY.

### Author commentary on quotations

After a quotation, the author adds an analytical note inside the same block-quote, on a `>` continuation line, per `CONV-002` in `conventions.md`. The note is prefixed with the literal label `Analytical note:`:

```
> [@citekey, p. X] "Quoted passage."
>
> Analytical note: use as the chapter's opening framing of the institutional problem. Pair with [@othercitekey, p. Y] for the contrast.
```

The analytical note tells the drafter how the quote should function in prose, not what the quote means.

---

<!--
PER-CHAPTER CARDS BEGIN HERE.

The structure below is the canonical chapter card. Use one card per
chapter from toc.md. For multi-section chapters, decide whether to use
a single card with subsections or a card per section. Catalog chapters
in a reference work often benefit from a card per emitter or per
denomination; analytical chapters usually benefit from a single card.

A blank card template follows. Copy it for each new chapter.
-->

## Front matter

<!-- Optional outline entries for preface, foreword, etc. Many projects
treat these as drafting-ready without a full chapter card. -->

## Part One. {{PART_ONE_TITLE}}

### Chapter 1: {{CHAPTER_TITLE}}

**Status:** [SKELETON]

**Function in the book.**

<!--
One paragraph. What this chapter does in the architecture of the
book. Why a reader needs it before reading the next chapter. The
function statement is the chapter contract: drafting cannot start
until this is clear.
-->

{{CHAPTER_FUNCTION}}

**Argument.**

<!--
The specific claim or distinction this chapter establishes. Not the
topic ("Convertibility") but the position ("ordinary monetary policy
was unavailable when fiscal stress mounted, because of the specific
legal architecture of Convertibility plus the absence of a fiscal
adjustment channel that did not pass through the central bank").

A chapter without an argument is a chapter without a reason to exist.
If you cannot state the argument in two or three sentences, the
chapter is not ready for outlining.
-->

{{CHAPTER_ARGUMENT}}

**Narrative beats.**

<!--
The moves the chapter makes, in order. Five to ten beats is typical.
Each beat is one sentence; the prose treatment of each beat happens in
the draft.
-->

- [Beat 1]
- [Beat 2]
- [Beat 3]
- [Beat 4]

**Cross-references.**

<!--
Forward and backward dependencies on other chapters. The drafter uses
these to avoid unnecessary repetition and to confirm that the chapter
arrives with the right material from earlier and hands off the right
material to later.
-->

- → §X.Y: [forward dependency, what this chapter sets up]
- ← §X.Y: [backward dependency, what this chapter requires]

**Source integration.**

<!--
Per-cited-source notes. For each source the chapter will draw on,
state:
- What the source provides (one or two sentences)
- How to use it (which beat or which argumentative move it supports)
- Caveats (working-paper version, contested interpretation, source
  bias, missing pagination)

The source integration list is the principal output of the outlining
phase. It is where research becomes available for drafting.
-->

- `citekey1` — [what it provides, how to use it, caveats]
- `citekey2` — [...]

**Working Quotations.**

<!--
Per CONV-002 in conventions.md, every working quotation begins with a
pandoc-citeproc marker on the block-quote line. The marker is what
binds the quote to references.bib; without it, the quote is decoration
and the draft editor will refuse the card.

The analytical note about the quote (what it does for the argument,
how to pair it with another quote, caveats about its source) lives
inside the same block-quote on a `>` continuation line, prefixed with
the literal label `Analytical note:`. Prose-style attribution like
"Author argues..." inside the analytical note is fine in addition to
the marker, not as a replacement.

A working quotation is not the final form of the quote in the draft.
It is the raw material the drafter will integrate, paraphrase, or
abridge as needed. Verbatim use in the manuscript should be checked
against the source one more time at the role-2 or role-3 stage.

Optional: group quotes by analytical use under a short italicised label.
Keep the label short — it is metadata, not a prose paragraph opener.
-->

Do:

```
> [@pressfield2002war, p. 15] "Resistance is the most toxic force on the planet."
>
> Analytical note: use as the chapter's opening framing of the inner obstacle. Pair with [@burkeman2021four, p. 60] for the contrast.
```

Don't:

```
**Pressfield integration (War of Art):**

Pressfield argues that Resistance is the central obstacle the working artist faces. He returns to this in the opening pages.
```

— The "Don't" form has no marker. It cannot survive a citekey rename and gives the draft editor nothing to anchor to.

_Optional cluster label._

> [@citekey, p. X] "Quoted passage."
>
> Analytical note: how this quote lands in the chapter argument.

> [@citekey, p. Y] "Another passage."
>
> Analytical note: how this one lands.

**Gaps and Queries.**

- [PENDING: evidence expected but not yet gathered]
- [QUERY: author decision required]

---

### Chapter 2: {{CHAPTER_TITLE}}

**Status:** [SKELETON]

<!-- Copy the structure above for each subsequent chapter. -->

---

## Part Two. {{PART_TWO_TITLE}}

<!-- Continue as needed. -->

---

## Citation Scaffolding: Pending Slots and Sources to Resolve

<!--
A running list of citation slots that exist in the outline but have not
yet been resolved to specific bibliographic entries. Examples:

- A primary law cited by another work but not yet located in its
  original form
- A working-paper reference whose published version exists but has not
  been checked
- An archival document whose precise shelfmark is incomplete
- A boundary citation where the project has not yet decided which of
  two related works to use

When a slot is resolved, mark it resolved and add the resolved citation
key to references.bib. The slot's entry can then be deleted or kept as a
historical note.
-->

(no pending slots yet)

## Research Priorities

<!--
A running list of the most important pending research tasks across all
chapters. Maintain in priority order. This section serves as the project's
to-do list for source acquisition, archive visits, oral interviews, and
secondary reading.
-->

(no research priorities yet)
