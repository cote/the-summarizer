# cote-summarize

Simplified summarize skill - condense an article, PDF, YouTube video, or pasted text into a tight prose Hugo blog post

## Structure

```
src/cote-summarize/          # source - edit here
  SKILL.md                # skill definition (frontmatter + docs)
  scripts/                # executable scripts
  reference/              # templates, config samples
target/cote-summarize/       # built artifact - zip to deploy
tests/                    # test scripts and fixtures
CHANGELOG.md              # version history
README.md                 # this file
```

## Install

```bash
audit-skill.sh cote-summarize
build-skill.sh cote-summarize
install-skill.sh cote-summarize
```

## Usage

<!-- TODO: show 2-3 common invocations -->

## Testing

Tests live in `tests/`. Run them before committing:

```bash
bash tests/run.sh
```

Document what each test verifies so they can be repeated consistently.

## Architecture

<!-- TODO: diagram of how the skill works, data flow, dependencies -->
