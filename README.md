# Bookwright

A structured pipeline for writing long-form nonfiction, packaged as a Claude Code skill.

## What this is

A workflow for writing book-length nonfiction — monographs, scholarly books, reference works, dissertations, long-form essays, and similar projects that combine substantial research with sustained prose. It scaffolds the project as a set of plain-markdown artifacts that the author owns and that Claude reads on every interaction, so the project's commitments stay coherent across the many sessions a real book takes.

The workflow exists because long-form nonfiction has structural problems that single-session writing tools do not solve: drafting begins before scope and voice are settled, voice drifts across chapters written months apart, the boundary between research notes and manuscript prose blurs, and an AI collaborator cannot keep the project's commitments straight across hundreds of exchanges without an explicit anchor. The pipeline addresses these by making the project's central decisions (purpose, audience, voice, scope, citation system) into explicit artifacts that Claude consults on every step.

Three commitments shape the workflow:

- **Decisions before drafting.** The bootstrap interview enforces two completeness gates (manifesto, voice) before any artifact is written. Premature drafting is the most common failure mode in long-form nonfiction; the gates make it harder.
- **Outline as the meeting point.** Research and structure converge in `outline.md`. Sources are integrated against specific chapters, working quotations cluster around specific arguments, and a chapter does not enter drafting until its outline card reaches `DRAFT-READY` status.
- **Three editorial passes per chapter.** Drafting (role 1), development-and-line editing (role 2), and copyediting (role 3) run sequentially. The roles are kept distinct because the work they do is distinct.

### Who it is for

Researchers writing monographs, authors working on long-form essays or trade nonfiction, doctoral candidates writing dissertations, practitioners producing reference works or catalogs. More broadly: any writer of substantial nonfiction who wants Claude Code to assist coherently across the months or years a real book takes.

### What it is not for

- **Fiction.** Fiction has structural needs (character development, plot architecture, scene work) that this workflow does not address.
- **Short-form writing.** A single article, blog post, or email does not need this much scaffolding.
- **Code or technical documentation.** Other tools fit better.

## The six phases

1. **Idea** — `manifesto.md`: what the project is and why it exists.
2. **Voice** — `voice.md`: how it is written.
3. **Structure** — `toc.md`: the spine of the work.
4. **Bibliography** — `references.bib`: the sources.
5. **Outline** — `outline.md`: where research becomes drafting raw material.
6. **Writing** — three editorial roles run in sequence per chapter (draft, develop, copyedit).

The full pipeline is documented in `workflow.md`. The bootstrap procedure is in `bootstrap.md`. The templates that get copied into new projects are in `templates/`.

## Installation

Clone the repo directly into the Claude Code skills directory:

```sh
git clone <remote> ~/.claude/skills/bookwright
```

That registers the workflow as a Claude Code skill available globally. Claude Code finds it in any project.

To update later: `cd ~/.claude/skills/bookwright && git pull`.

## Use

Start a Claude Code session in your project directory. Inside the session, you can either invoke the skill explicitly with the slash command `/bookwright`, or simply describe what you want to write and let Claude propose the bootstrap.

### Bootstrap a new project

In an empty (or nearly empty) project directory, tell Claude:

> "I want to start a book about [topic]."

Claude will detect that the directory does not contain `manifesto.md`, enter bootstrap mode, and run the guided interview defined in `bootstrap.md`. The interview has two completeness gates (manifesto, voice) before any file is written. When both gates close, the full set of project artifacts is generated.

### After bootstrap

The bootstrap produces first drafts of `manifesto.md` and `voice.md`, and scaffolds for the rest of the artifacts. These are starting points, not finished documents. Read them carefully and refine them in your own voice before moving on to research and outlining. The skill scaffolds the project; the author owns it.

### Resume work on an existing project

In a directory that already contains `manifesto.md`, ask Claude to draft, develop-edit, or copyedit a chapter. Claude reads `manifesto.md`, `voice.md`, and the corresponding role file before working.

## Files

```text
bookwright/
├── bootstrap.md                           # bootstrap protocol with completeness gates
├── CHANGELOG.md                           # version history
├── CONTRIBUTING.md                        # contribution guidelines
├── LICENSE                                # MIT
├── README.md                              # this file
├── SKILL.md                               # Claude-facing skill instructions
├── templates/
│   ├── conventions.md                     # ADR-style with seed convention
│   ├── manifesto.md                       # template with meta-instructions
│   ├── outline.md                         # chapter-card template
│   ├── references.bib                     # empty BibTeX with header
│   ├── role-1-draft-editor.md             # generic draft editor
│   ├── role-2-development-line-editor.md  # generic development-line editor
│   ├── role-3-copy-editor.md              # generic copy editor
│   ├── toc.md                             # minimal scaffold
│   └── voice.md                           # template with meta-instructions
└── workflow.md                            # human-facing pipeline description
```

## License and contributions

Licensed under the MIT License. See [LICENSE](LICENSE).

Issues and pull requests are welcome. See [CONTRIBUTING.md](CONTRIBUTING.md) before opening anything beyond a typo fix.

See [CHANGELOG.md](CHANGELOG.md) for version history.
