# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repository is

This repo *is* a Claude Code skill. It is not a normal software project: there is no build, no test runner, no linter. The "code" is `SKILL.md` (the Claude-facing instructions), `bootstrap.md` and `workflow.md` (the protocol and pipeline definition), and `templates/` (markdown files the bootstrap instantiates into a user's book project).

When working here, you are *editing the skill itself*, not running it. The skill is exercised by being installed at `~/.claude/skills/bookwright/` and invoked from a separate Claude Code session in an author's project directory.

## Two execution contexts — do not mix paths

The single most common source of confusion when editing this skill:

- **Inside the skill** (this repo), template paths are relative to the skill root: `templates/manifesto.md`, `templates/voice.md`, etc.
- **Inside an instantiated project** (a book the skill has bootstrapped), the same files live at the project root with no `templates/` prefix: `manifesto.md`, `voice.md`, etc.

`SKILL.md`, `bootstrap.md`, and the role templates carry instructions that cross this boundary. When you edit them, check which context each path reference is in. The skill reads `templates/manifesto.md` to generate `manifesto.md`; the role files at the project root read sibling files like `voice.md`, not anything in `templates/`.

## The mandatory-interview override (load-bearing)

The bootstrap procedure is an *interview*, not an inference task. This is enforced explicitly in `SKILL.md` and `bootstrap.md`, and it overrides session-level preferences:

- A user's global "work without stopping for clarifying questions" preference does **not** apply inside the bootstrap. The interview is the whole point of invoking the skill.
- Drafting `manifesto.md` or `voice.md` from "reasonable defaults" is forbidden. There are no reasonable defaults for audience, scope, methodological model, voice, or citation system.
- The two completeness gates (manifesto, voice) must be satisfied with concrete answers before any file is generated.

When editing `SKILL.md` or `bootstrap.md`, preserve this stance. Softening it (adding inference fallbacks, allowing partial-checklist generation, removing the "no clarifying questions" override) breaks the skill's central guarantee to the author.

## Pipeline architecture

The skill drives a six-phase pipeline. Each phase produces one artifact and gates the next:

1. **Idea** → `manifesto.md` (gated by manifesto interview)
2. **Voice** → `voice.md` (gated by voice interview)
3. **Structure** → `toc.md` (light gate: title + one-line function per chapter)
4. **Bibliography** → `references.bib` (gate: minimum viable bibliography per part)
5. **Outline** → `outline.md` (gate per chapter: status flag reaches `[DRAFT-READY]`)
6. **Writing** → three editorial roles run sequentially per chapter (`role-1-draft-editor.md`, `role-2-development-line-editor.md`, `role-3-copy-editor.md`)

Phase 5 has an optional per-source role, `role-0-outliner.md`. The author invokes it one source at a time to extract working quotations into the chapter cards in `outline.md`. The role is not part of the chapter-card gate — that gate stays per chapter.

`workflow.md` is the human-facing description; `bootstrap.md` is the protocol Claude follows. The two must stay consistent — when you change phase definitions or exit criteria, update both.

## Substitution variables

Templates use `{{DOUBLE_BRACE}}` placeholders that the bootstrap fills in from interview answers. The canonical variable set is documented in `SKILL.md` under "Substitution variables." When adding a new variable to a template, also add it to that list. Variables that remain empty after the interview are written as the literal placeholder, signalling to the author that the field is open.

## Conventions when editing templates

- **HTML-comment briefs** at the top of each template section are *instructions to the author* (or to Claude, during section deepening). They are meant to be replaced by actual content, not preserved. When editing them, write them as the author's own brief to themselves.
- **`CONV-NNN` identifiers** in `templates/conventions.md` are stable. Never renumber or reuse a CONV identifier; new conventions take the next available number. Order of entries may be changed for readability without affecting identifiers.
- **Status flags** in `templates/outline.md` (`[SKELETON]`, `[SOURCE-INTEGRATION]`, `[QUOTATIONS]`, `[DRAFT-READY]`, `[DRAFTED]`, `[FINAL]`) are referenced by name in `bootstrap.md`, `workflow.md`, and the role templates. Renaming one requires a cross-file update.
- The line-wrapping convention seeded as `CONV-001` (one paragraph = one source line, no hard wrapping in prose) applies to this repo's own markdown as well.

## Testing a change

There is no automated test suite. Validate behavioral changes by exercising the skill end-to-end:

1. Symlink or clone this repo into `~/.claude/skills/bookwright/`.
2. Create an empty directory for a test project.
3. Start a Claude Code session in it and run the bootstrap (e.g., "I want to start a book about X").
4. Confirm the affected behavior — gates fire correctly, templates substitute, role files reference the right paths.

For template-only or documentation-only changes, this can be skipped if the change is mechanical. For changes to `SKILL.md`, `bootstrap.md`, or any cross-file path reference, run the full bootstrap.

## Changelog format

`CHANGELOG.md` follows a constrained Keep-a-Changelog adaptation:

- Four fixed top-level sections in this order: **Skill**, **Templates**, **Documentation**, **Infrastructure**. Sections with no entries for a version are omitted.
- Within each section, entries are sorted case-insensitively by filename.
- The project follows SemVer.

Every user-visible change should land with a `CHANGELOG.md` entry in the right section.
