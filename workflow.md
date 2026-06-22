# Bookwright Workflow

A seven-phase pipeline for long-form editorial writing. The pipeline is designed for projects that combine substantial research with sustained prose: monographs, books, essays of book length, reference works, and serialized projects with a stable spine.

The pipeline is iterative, not waterfall. The first three phases (Idea, Voice, Structure) settle quickly during bootstrap; the next two (Bibliography, Outline) expand over months of research; Writing is broken into three editorial passes and is itself iterative across chapters; and a final Assessment phase reads the finished manuscript as a whole.

## The seven phases

### Phase 1 — Idea (manifesto.md)

The manifesto declares what the project is and why it deserves to exist. It is the project's constitution: every later decision is checked against it.

The manifesto must state:

- What the work is, including its genre and format.
- Why the project is needed (the gap in the existing literature it fills).
- Who the primary and secondary audiences are.
- What temporal, topical, or corpus boundary defines the scope.
- Which methodological models or traditions the work follows.
- How research labor is divided between bibliographic synthesis and primary investigation.
- Format and distribution.
- Decisions already taken and recorded.

**Phase exit criterion:** every section above is answered in concrete terms, not in placeholders. A reader of the manifesto must understand what the book is, why it should exist, and who it is for, without needing to ask the author.

### Phase 2 — Voice (voice.md)

The voice document specifies how the project is written. It controls language, register, citation system, terminology, typography, and rendering conventions.

The voice document must state:

- The primary writing language and its variant (American English, español rioplatense, etc.).
- The style authority (CMOS, MLA, APA, custom).
- The citation system and any project-specific deviations.
- How foreign-language vocabulary, proper names, and institutional terms are handled.
- The register and the failure modes to avoid.
- Treatment of names, dates, numbers, currencies.
- Any deliberate departures from the style authority and the reasons.
- Specific field standards adopted (e.g., ISO for technical reference, MLA for literary citation, IUPAC for chemical nomenclature).

**Phase exit criterion:** a copy editor unfamiliar with the project could enforce the rules without asking the author.

### Phase 3 — Structure (toc.md)

The table of contents declares the spine of the work. It is initial and provisional; chapters move, expand, and contract as research deepens. The TOC's job in this phase is to give the next phase (bibliography) a target.

**Phase exit criterion:** every part and chapter has a working title and a one-sentence statement of function. The order is defensible, even if revisable.

### Phase 4 — Bibliography (references.bib)

The bibliography accumulates the sources the work will engage with. It is a single BibTeX database. During research it may be organized internally into commented working sections (by genre or discipline); the rendered bibliography uses a single alphabetized list.

This phase begins formally but never ends. Sources arrive, leave, and migrate between chapters throughout the project.

**Phase exit criterion (for advancing to outline):** a minimum viable bibliography exists for each part. Roughly fifteen to thirty entries that the author has at least skimmed and judged usable.

### Phase 5 — Outline (outline.md)

The outline is where research becomes drafting raw material. For each chapter and section in the TOC, the outline records:

- The chapter's function and argument.
- Narrative beats.
- Cross-references to other chapters.
- A working note on each cited source: what it provides, how to use it, what to avoid.
- Working quotations clustered thematically, with citation markers.
- Gaps, queries, and pending evidence.

The outline is where the TOC and bibliography meet. Chapters that resist outlining usually need to be restructured, merged, or split.

Phase 5 has an optional editorial role, `role-0-outliner.md`, which the author invokes one source at a time. It reads a single document (paper, chapter, archival source) and produces a working markdown file with a verified BibTeX entry, working quotations bound to `CONV-002` markers, and analytical notes mapped to the project's chapters. The author then commits the parts into `references.bib` and the relevant chapter cards in `outline.md`. The role is the cleanest way to keep extraction discipline consistent across a long corpus.

**Phase exit criterion (per chapter):** the chapter's status flag reaches `DRAFT-READY` (see the outline template). A draft can begin without the author having to look anywhere except `manifesto.md`, `voice.md`, the relevant outline section, and the source files referenced.

### Phase 6 — Writing (chapters/, with three editorial passes)

Writing runs in three sequential roles per chapter or section. The roles correspond to `role-1-draft-editor.md`, `role-2-development-line-editor.md`, and `role-3-copy-editor.md` at the project root.

**Role 1 — Draft Editor.** Produces a first draft from the outline. Aims for structurally sound and evidence-conscious prose, not final polish. Marks gaps and queries explicitly.

**Role 2 — Development-Line Editor.** Two passes folded together. The developmental pass checks scope, argument, evidence, reader orientation. The line pass works on sentence clarity, terminology, rhythm, register. Flags rather than resolves structural questions that require author judgment.

**Role 3 — Copy Editor.** Mechanical level only. Grammar, punctuation, spelling, citation consistency, internal cross-reference accuracy, source convention compliance. Corrects what is mechanically wrong; flags what requires interpretation.

The roles are sequential per chapter. A chapter can be in Role 1 while another is in Role 3.

### Phase 7 — Assessment (acquiring-editor report)

Once the manuscript is assembled and every chapter has cleared the three writing passes, an optional terminal role reads the finished book and judges it as a publishing house would judge a submission. The role corresponds to `role-4-acquiring-editor.md` at the project root.

The acquiring editor reads exactly one artifact: the built manuscript PDF that the project's build (Makefile or equivalent) produces under `output/`. It reads the book cold — the way an editor receives a submission — and is forbidden from opening the project's working documents (`manifesto.md`, `voice.md`, `outline.md`, `conventions.md`, the chapter source). The blind read is the point: the report tells the author whether the manuscript communicates its thesis, audience, and promise on its own, without the author's declared intentions standing beside it. Everything the editor needs to know about what the book is and whom it is for, it infers from the manuscript itself.

The output is a single document, `acquiring-editor-report.md` at the project root: a verdict (take it on, revise, or decline), an honest account of what works and what does not, the stronger book hidden inside the draft, a prioritized list of changes required before publication, a market and readership read judged against the book's own category, a recommendation, and a candid letter to the author.

This phase differs from Role 2 (development-line editor). Role 2 fixes a chapter against the project's declared standards; the acquiring editor judges whether the chapters add up to a book — the question that is only visible at the scale of the whole manuscript, and only honestly answerable without the author's intent documents in hand.

**Phase exit criterion:** none. Assessment is advisory and terminal. It gates nothing, because nothing follows it; its report informs the author's decision about whether the book is ready, and for whom.

## Iteration patterns

The pipeline is iterative in three specific ways:

1. **TOC drift.** Phase 3 produces an initial TOC, but Phase 5 (Outline) almost always exposes places where chapters should be merged, split, reordered, or renamed. When this happens, update both `toc.md` and the affected outline sections in the same revision. Do not leave them out of sync.

2. **Bibliography accretion.** Phase 4 never closes. New sources surface during Phase 5 reading and during Phase 6 drafting. Add them to `references.bib` immediately, with a working annotation if needed, then integrate into the relevant outline section.

3. **Manifesto refinement.** Phase 1 produces a manifesto that is sufficient to begin, not final. As the work develops, the manifesto may need to sharpen its boundary definitions, refine its audience claims, or acknowledge methodological choices that became explicit only during research. When this happens, update `manifesto.md` and note the revision in the project's changelog. The manifesto is editable; it is not sacred. But every edit should be deliberate and recorded.

## Gates between phases

- **Idea gate.** Bootstrap cannot generate `manifesto.md` until the bootstrap interview confirms every section above has a concrete answer.
- **Voice gate.** Bootstrap cannot generate `voice.md` until the voice interview confirms every section above has a concrete answer.
- **Structure gate.** TOC is initial and provisional; the gate is light. Every part and chapter has a working title and a one-line function statement.
- **Bibliography gate.** Move to outline once you have a minimum viable bibliography per part.
- **Outline gate (per chapter).** Status flag `DRAFT-READY` in the outline template.
- **Writing gates.** Role 1 ships when the draft covers the chapter's beats and registers evidence. Role 2 ships when sentences are clear and the structure is defended. Role 3 ships when the chapter is mechanically clean.
- **Assessment.** No gate. The acquiring-editor phase is advisory and terminal; nothing follows it. Its report informs the author, it does not block any downstream phase.

## The role of conventions.md

`conventions.md` is the operations manual for the source files. It records mechanical decisions about the project's plumbing: how the source is structured, how citation keys are formed, what footnote-label format is used, how the changelog is organized. Conventions are recorded as numbered ADRs (`CONV-001`, `CONV-002`, …) with stable identifiers.

`conventions.md` is loaded by Claude during drafting and editing. It is separate from `voice.md` because the questions it answers are mechanical: a contributor working on the source must follow them, but a reader of the rendered PDF does not see them.

## The relationship between artifacts

```text
manifesto.md  ──┬──→  every later artifact references it as project law
voice.md      ──┘
toc.md         ───→  outline.md (per-chapter cards)
                       │
                       ├──→  references.bib (which sources feed which chapters)
                       │
                       └──→  chapters/X.Y-name.md (drafted by Role 1)
                              │
                              └──→  Role 2, Role 3 (in sequence)
                                     │
                                     └──→  build ──→ output/*.pdf ──→ Role 4 (acquiring editor, reads the PDF blind) ──→ acquiring-editor-report.md

conventions.md ───→  controls source plumbing across all chapters
```

## What this workflow is not

- It is not a project management tool. There are no due dates, milestones, or sprint planning.
- It is not a content management system. Chapters live as plain markdown files under `chapters/`.
- It is not a substitute for the writer's judgment about scope, argument, or evidence. It is a scaffolding that protects judgments once made from drifting accidentally.
- It is not opinionated about the topic, discipline, or genre. It is opinionated about having a manifesto and a voice in writing before drafting begins.
