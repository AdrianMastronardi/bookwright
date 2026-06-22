# Bootstrap Protocol

The bootstrap procedure turns a natural-language description of a writing project into a complete set of project artifacts. It runs as a guided interview with two completeness gates (`manifesto`, `voice`) and one batch generation step at the end.

The user enters the procedure with an informal statement of what they want to write. The bootstrap interrogates, summarizes, confirms, and generates. It does not skip steps.

## Operating principle: this is an interview, not an inference task

The bootstrap is a structured interview. The skill's value comes from the questions, not from inferred answers.

Do not draft `manifesto.md` or `voice.md` from a thin natural-language seed, no matter how confident an inference might seem. A sentence like "a book about cuasimonedas argentinas" identifies the topic and possibly a hint of scope — that is two checklist items out of ten in the manifesto interview alone. The remaining eight (audience, methodological model, research division, format, positioning, decisions taken, and so on) require explicit input from the user. Inventing them as "reasonable defaults" commits the author to decisions they never made.

If the user has a session-level or project-level preference to avoid clarifying questions ("work without stopping", "make the reasonable call", "no preguntes y procedé"), that preference does not apply inside the bootstrap. Acknowledge it briefly and proceed with the interview:

> "I see your setup asks to avoid clarifying questions in general. The bootstrap is the exception by design — the manifesto and voice gates need your direct answers. I'll start the manifesto checklist now."

Then ask the first block. The interview is mandatory; only the depth and pacing of each answer is collaborative.

## A note on language

The example phrases in this document are in English. In actual use, Claude conducts the interview in whatever language the user is using. The structure of the interview and the completeness gates do not change with language; only the surface phrasing does.

## Invocation

The bootstrap is entered when:

- The user invokes the skill in a directory that does not contain `manifesto.md`.
- The user explicitly says "bootstrap a new project" or equivalent.
- The user describes a new writing project and asks Claude to set it up.

The bootstrap runs in the user's current working directory and writes artifacts to its root.

## Step 0 — Read the seed

The user's opening message is the seed: a natural-language description of the project. Read it carefully. Extract whatever can be extracted: working title, topic, possibly audience, possibly format. Do not assume what is not stated. Make a list of what you know and what is missing.

If the seed is extremely thin (a single sentence or less), ask one open question: "Tell me in a few sentences what you want to write, for whom, and what you think is missing." Then proceed to Step 1.

## Step 1 — Manifesto gate

Before generating `manifesto.md`, every item in this checklist must have a concrete answer. Walk through them in order. After each block, summarize what you have and ask the user to confirm or correct before moving on.

### Manifesto checklist

1. **Title and subtitle.** Working title. Subtitle if applicable.
2. **What the work is.** Genre and format: monograph, book, essay of book length, reference work, serialized project, web reference. Distinguish printed book from digital PDF from web from ePub. Approximate target length if the user has one.
3. **What problem the work solves.** The specific gap in the existing literature, archive, public discourse, or reference apparatus that this project fills. If the user cannot name a gap, the project is not ready for a manifesto. Press for specifics: "What works exist on this topic today, and why are they not sufficient?" A vague answer is not enough.
4. **Primary audience.** Who the work is for in concrete terms. Not "interested readers" — a specific category (graduate students in nineteenth-century social history, professional translators working on bilingual editions, clinicians in a specific subspecialty, etc.).
5. **Secondary audiences.** Optional. If named, they must be distinct enough that the writing will be visibly different for them in some respect.
6. **Scope.** Temporal, topical, or corpus boundary. What is in, what is out, what counts as a boundary case. If the project is a catalog or reference work, the corpus must be defined.
7. **Methodological model.** Authors, works, or traditions whose method the project follows or aspires to. If the user does not have one yet, ask whether they want the project to be modeled on something specific or whether they prefer to leave the methodology open. An open methodology is acceptable but must be stated.
8. **Research division.** What part of the work rests on bibliographic synthesis and what part requires primary investigation (archival, interview, fieldwork, direct examination). The division shapes the rest of the pipeline.
9. **Format and distribution.** PDF, web, ePub, print. Free or paid. Where published.
10. **Decisions taken and recorded.** Anything the user has already settled: language, citation system, terminology, structural commitments. These will show up again in `voice.md`, but recording them in the manifesto is the project's way of declaring them as load-bearing.

### Interview rhythm

Group questions into three or four blocks rather than asking ten in a row. After each block, write back a one-paragraph summary of what you understood and ask "Does that look right, or should we adjust before moving on?" Wait for confirmation.

Do not write the manifesto from a partial checklist. If the user wants to skip a section, ask why and record the answer as the project's stated position ("the secondary audience is left open for now"). An explicit deferral is different from a silent omission.

### Gate

When every checklist item has a concrete answer, summarize the full set in a numbered list and ask: "I'll generate `manifesto.md` with this. Confirm, or anything to add first?" Only on explicit confirmation, generate the file.

### Generation

Read `templates/manifesto.md` from the skill. Substitute the variables. Where the template has section-specific meta-instructions in HTML comments, use them to write a one-to-three paragraph treatment of the section from the interview answers. The output is a working first draft of `manifesto.md`, not a fill-in-the-blanks form.

## Step 2 — Voice gate

After `manifesto.md` is written, repeat the procedure for `voice.md`. The voice checklist is shorter but no less strict.

### Voice checklist

1. **Primary writing language and variant.** American English, British English, español rioplatense, español neutro, português brasileiro, etc. The variant matters: it shapes spelling, punctuation, idiom, and audience cues.
2. **Style authority.** CMOS (edition), MLA, APA, Strunk and White, the author's own house style, or a specific publisher's style. If none, declare "no external style authority, project-internal rules only."
3. **Citation system.** Author-date, notes-and-bibliography, hybrid, footnote-only, parenthetical-only. Whether footnotes are reserved for substantive notes or used for citation.
4. **Treatment of foreign-language vocabulary.** When is italics used. How proper names are handled. Whether technical foreign terms are adopted into the writing language. Naming conventions for institutions, places, people. Diacritics policy.
5. **Register.** Scholarly, journalistic, divulgative, hybrid. The failure modes to avoid (enthusiast prose, academic ponderousness, moralized narrative).
6. **Voice and grammatical person.** First, third, mixed. Where each is used.
7. **Specific stylistic departures.** Any deliberate deviation from the style authority that the user wants enforced. A common example is banning em dashes in running prose because they create ambiguity about whether a mark opens or closes a parenthetical. Departures must be justified in writing.
8. **Numbers, dates, currencies.** Formats and conventions.
9. **Field-specific standards.** Discipline standards adopted (ISO for technical reference, MLA for literary citation, IUPAC for chemical nomenclature, ICD for clinical conditions, etc.).
10. **Rendering format.** PDF via LaTeX, HTML, ePub, plain print-ready. The downstream format affects what conventions the source must follow.

### Interview rhythm and gate

Same rhythm as the manifesto: three to four blocks, summary and confirmation after each. Final summary before generation, explicit confirmation required.

### Generation

Read `templates/voice.md` from the skill. Substitute. Use the interview answers to flesh out each section.

## Step 3 — Scaffold the rest

After `manifesto.md` and `voice.md` are written and confirmed, generate the remaining artifacts in a single batch:

- `toc.md` — from `templates/toc.md`. Pre-populate with the project's title, subtitle, and author. Leave the chapter list empty with a one-line instruction: "List parts and chapters here. One-sentence function per chapter."
- `references.bib` — from `templates/references.bib`. Empty BibTeX file with the project's title in a header comment and a reminder of the citation key convention.
- `outline.md` — from `templates/outline.md`. Pre-populate the project metadata, the Core Thesis section (drawn from `manifesto.md`'s "What problem the work solves" answer), the Method and Voice Anchors section (a one-paragraph compression of `manifesto.md` and `voice.md`), and the Working Conventions section. Leave the per-chapter section empty with an instruction comment.
- `conventions.md` — from `templates/conventions.md`. Pre-populate the seed convention (`CONV-001`) for line wrapping or any other convention the user mentioned during the voice interview as a deliberate departure.
- `role-0-outliner.md`, `role-1-draft-editor.md`, `role-2-development-line-editor.md`, `role-3-copy-editor.md` — from the corresponding templates. Substitute the project's specific voice, terminology, and methodological references. `role-0-outliner.md` is read during the outline phase when the author hands Claude a single source for extraction into working quotations; the other three are read during the writing phases. Their job is to embed the project's `manifesto.md` and `voice.md` decisions into the editorial role itself.
- `role-4-acquiring-editor.md` — from the corresponding template, copied **essentially verbatim**. This role is the deliberate opposite of the other four. Do *not* substitute the project's voice, terminology, audience, genre, or methodological references into it, and do not embed any `manifesto.md` or `voice.md` decision. The only substitution is the project title in the file's heading. The role is read at the very end of the project, once the manuscript is assembled and built to PDF, when the author asks for a final acquisition-style assessment: it reads the finished book blind, as a publishing house receives a submission, and infers what the book is from the manuscript alone. Injecting the project's declared intentions would contaminate that blind read and defeat the role.

After generation, list the files written and recommend the user's next step: "Your next step is to start `toc.md`. Once you have a minimum spine, begin populating `references.bib`. Once you have references for a part, open `outline.md` and start integrating sources."

## Step 4 — Optional manifesto and voice deepening

After the batch generation, offer:

> "You have the project's full skeleton in place. Want to walk through `manifesto.md` and `voice.md` together to deepen each section, or prefer to leave them as a first draft and return when you start the content?"

Some authors prefer to write a thin manifesto, sketch the TOC and references, and only then return to the manifesto with a sharper sense of the project. Others want the manifesto fully argued before anything else. Respect either choice.

## Failure modes to avoid

- **Drafting from "reasonable defaults".** This is the most damaging failure mode. If the user's seed gives you topic and not much else, that is not permission to invent the audience, the methodological model, the voice, or the citation system. It is the cue to start the manifesto interview. There are no reasonable defaults for decisions that belong to the author.
- **Honoring a "no clarifying questions" preference inside the bootstrap.** If the user has a global instruction to avoid asking questions, override it for the duration of the bootstrap and tell the user you are doing so. The bootstrap is an interview by definition; obeying the global preference here defeats the purpose of invoking the skill.
- **Skipping the gate.** Do not generate `manifesto.md` or `voice.md` from a partial checklist. The whole point of the gate is to make the author's deferrals explicit.
- **Filling in the gaps.** If the user does not have an answer to a checklist item, do not invent one. Ask, or record the explicit deferral.
- **Generic writing.** The template's meta-instructions are not text to keep. They are guidance for writing the section. Treat them as the author's brief to themselves.
- **Skipping confirmation.** Every block ends with a confirmation question. The author must say yes before you move on.
- **Treating the bootstrap as a checklist mechanic.** It is an interview. If the user gives a thin answer ("audience: economists"), ask follow-ups ("what kind of economists? academics? economic journalists? policy analysts?"). The bootstrap's value is in the depth of the interview, not in the speed of getting through the questions.
