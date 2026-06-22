---
name: bookwright
description: Bootstrap and run a long-form editorial writing project (book, monograph, essay, serialized work) using a seven-phase pipeline. Use when the user asks to start a new writing project ("I want to write a book about X", "starting a new editorial project", "/bookwright"), when they reference the phases of this pipeline (manifesto, voice, toc, outline, drafting roles), or when they ask Claude to help draft, develop-edit, or copy-edit a chapter inside a project that already has manifesto.md and voice.md at its root.
---

# Bookwright

This skill packages a seven-phase pipeline for long-form editorial writing. It produces a coherent set of project artifacts (`manifesto.md`, `voice.md`, `toc.md`, `outline.md`, `references.bib`, `conventions.md`, and five editorial role files) and then drives source extraction, drafting, development editing, copyediting, and a final whole-manuscript assessment against those artifacts.

The skill is invoked in one of three modes:

1. **Bootstrap a new project.** The user says, in natural language, what they want to write. The skill interrogates until two completeness gates (manifesto, voice) are satisfied, then generates all artifacts. See `bootstrap.md`.
2. **Resume work on an existing project.** The skill detects `manifesto.md` and `voice.md` at the project root and reads them before touching anything. Use them as project law for every decision.
3. **Run an editorial role.** The user asks for source extraction into outline material, a draft, a development edit, a copyedit of a chapter or section, or a final acquisition-style assessment of the finished manuscript. Load the corresponding `role-N-*.md` from the project root and follow it.

The pipeline itself is documented in `workflow.md`. The bootstrap procedure is in `bootstrap.md`. The templates are in `templates/`.

## Mandatory interview in bootstrap mode (read this before anything else)

**The bootstrap procedure REQUIRES interactive questioning. This is non-negotiable.**

The bootstrap is an interview by design. Its two completeness gates (manifesto, voice) exist precisely to prevent the author's project from being committed to decisions the author never made. Reading this skill is itself a commitment to running that interview.

The following are FORBIDDEN inside bootstrap mode:

- **Drafting `manifesto.md` or `voice.md` from "reasonable defaults".** There are no reasonable defaults for a project's audience, scope, methodological model, voice, or citation system. These decisions belong to the author. Inventing them defeats the purpose of the skill.
- **Skipping the interview because the user's project preferences say to avoid clarifying questions.** Project-level instructions like "work without stopping for clarifying questions" or "make the reasonable call and continue" do not apply inside this procedure. The user invoked this skill specifically to be interviewed. Asking the questions IS the work.
- **Treating a thin natural-language seed as sufficient input.** A sentence about the topic ("a book about X") populates one or two checklist items at most. The remaining items require explicit answers from the user.

If the user has a global preference to avoid clarifying questions, acknowledge it briefly and proceed with the interview anyway:

> "I see your project setup asks to avoid clarifying questions in general. The bootstrap is the exception — it is fundamentally an interview, and the manifesto and voice gates require your direct input. I'll start with the manifesto checklist."

Then start asking. The structure of the interview is mandatory. Only the depth of each answer is collaborative.

## When to invoke this skill

Invoke when any of the following holds:

- The user asks to start a new long-form writing project and the project root does not yet contain `manifesto.md`.
- The user types `/bookwright` or mentions the skill by name.
- The user references the pipeline's phases or artifacts by name (manifesto, voice, outline, draft-editor, etc.) in a context that suggests they want to advance the work.
- The user asks Claude to draft, develop-edit, or copyedit material inside a directory that already contains the pipeline's artifacts.

Do NOT invoke for one-off writing assistance unrelated to a structured editorial project, for code or technical writing, or for short-form content (single blog post, single email).

## What the skill does on invocation

1. **Detect mode.** Check whether the current working directory contains `manifesto.md`, `voice.md`, and the rest of the artifact set.
   - None present: enter **Bootstrap mode**. Read `bootstrap.md` and follow it.
   - All present: enter **Resume mode**. Read `manifesto.md`, `voice.md`, and any other artifact the user's request implicates. Then act according to the user's specific request.
   - Partial: ask the user whether to complete the bootstrap (preferred) or to proceed with the artifacts that exist.

2. **Read project law before acting.** In Resume mode, never draft, edit, or restructure without first reading `manifesto.md` and `voice.md`. They are project law. Reading them is non-negotiable, even when the user's request seems narrow. The one exception is `role-4-acquiring-editor.md`: it evaluates the finished manuscript as a publishing house would receive it — cold — and therefore deliberately does *not* read `manifesto.md`, `voice.md`, or any other working document. Do not feed it project law; doing so destroys the blind read that is the role's entire purpose.

3. **For editorial roles**, read the corresponding role file (`role-0-outliner.md`, `role-1-draft-editor.md`, `role-2-development-line-editor.md`, `role-3-copy-editor.md`, or `role-4-acquiring-editor.md`) from the project root, not from this skill. The first four have been instantiated with the project's specific voice and method; the skill's `templates/` directory contains only the generic versions. `role-4-acquiring-editor.md` is the exception: it is deliberately generic and carries no project specifics, because it must read the manuscript blind (see point 2).

## Files in this skill

- `SKILL.md` — this file. Claude reads it on skill invocation.
- `workflow.md` — human-facing description of the seven-phase pipeline.
- `bootstrap.md` — the bootstrap protocol with two completeness gates.
- `templates/manifesto.md` — generic template with meta-instructions.
- `templates/voice.md` — generic template with meta-instructions.
- `templates/toc.md` — minimal scaffold.
- `templates/outline.md` — the chapter-card template with status flags, cross-references, and gaps/queries.
- `templates/references.bib` — empty BibTeX file with header.
- `templates/conventions.md` — ADR-style conventions file with a seed entry.
- `templates/role-0-outliner.md` — generic source-to-outline extractor that produces working quotations bound to CONV-002 markers.
- `templates/role-1-draft-editor.md` — generic draft editor with placeholders.
- `templates/role-2-development-line-editor.md` — generic development-line editor.
- `templates/role-3-copy-editor.md` — generic copy editor.
- `templates/role-4-acquiring-editor.md` — generic acquiring-editor assessment of the finished manuscript; reads only the built PDF, blind to the project's working documents.

## Substitution variables

Templates contain placeholders in `{{DOUBLE_BRACE}}` form. The bootstrap procedure substitutes them from the answers collected during the interview. The canonical variable set:

- `{{PROJECT_TITLE}}` — title of the work
- `{{SUBTITLE}}` — subtitle, may be empty
- `{{AUTHOR}}` — author of record
- `{{PROJECT_GENRE}}` — book, monograph, essay, series, web reference
- `{{PRIMARY_LANGUAGE}}` — language and variant for the writing (e.g., "American English", "español rioplatense")
- `{{CORPUS_LANGUAGE}}` — language(s) of the source corpus
- `{{PRIMARY_AUDIENCE}}` — primary audience description
- `{{SECONDARY_AUDIENCE}}` — secondary audience description, may be empty
- `{{PERIOD_OR_SCOPE}}` — temporal or topical scope
- `{{METHODOLOGICAL_MODEL}}` — referenced authors, works, or traditions
- `{{RESEARCH_DIVISION}}` — what is synthesis, what is primary
- `{{DISTRIBUTION_FORMAT}}` — PDF, web, ePub, print
- `{{DISTRIBUTION_ACCESS}}` — free, paywalled, institutional
- `{{STYLE_AUTHORITY}}` — CMOS 18, MLA 9, APA 7, custom, etc.
- `{{CITATION_SYSTEM}}` — author-date, notes-and-bibliography, hybrid
- `{{REGISTER}}` — scholarly, journalistic, divulgative, hybrid
- `{{STYLE_DEPARTURES}}` — explicit deviations from the style authority
- `{{FIELD_STANDARDS}}` — discipline-specific standards (ISO, MLA, IUPAC, etc.)

The bootstrap substitutes all of these. Variables that remain empty after the interview are written as the literal placeholder, signaling to the author that the field is open for later refinement.

## Conventions for skill-internal references

Inside this skill, file paths are relative to the skill root (`templates/manifesto.md`). Inside an instantiated project, file paths are relative to the project root (`manifesto.md`). Never mix the two.
