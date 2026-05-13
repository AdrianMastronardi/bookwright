# Contributing

Issues and pull requests are welcome.

## Scope

This repo is a six-phase editorial pipeline packaged as a Claude Code skill. Contributions that fit the project:

- Template improvements that make the artifacts more useful across disciplines.
- Workflow refinements based on real use.
- Clarifications, typo fixes, and improvements to the documentation.
- Bug fixes in the bootstrap procedure or in template substitution.

Contributions that probably do not fit:

- Domain-specific content (a template tuned to one discipline, a vocabulary specific to one field).
- New features that do not serve the six-phase pipeline.
- Major restructuring of the workflow itself, unless discussed first.

## Before opening a PR

For anything beyond a typo or a small clarification, open an issue first to describe what you want to change and why. This saves you work if the change is out of scope, and gives me a chance to suggest a smaller path if there is one.

## What a good change looks like

- It serves writers using the skill, not the skill itself.
- It does not add complexity that future users will have to learn.
- It is consistent with the voice of the existing documentation (precise, unhurried, not decorative).
- The diff is as small as the change requires.

## Testing a change

To validate a change locally:

1. Clone or symlink the repo into `~/.claude/skills/bookwright/`.
2. Create an empty directory for a test project.
3. Start a Claude Code session inside it and run the bootstrap.
4. Confirm the affected behavior (gates, templates, role files) works as expected.

## License

By contributing, you agree that your contributions will be licensed under the MIT License, the same license that covers the rest of the project.
