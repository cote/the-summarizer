# The Summarizer

A Claude Code skill that summarizes external content (article URLs, pasted text, PDFs, YouTube videos) into a tight prose form with a Take, highlighted key ideas, and a Hugo-ready output.

The skill picks among named prompt variants (e.g. `DEFAULT_SUMMARY_PROMPT.md`, `TAKE_SUMMARY_PROMPT.md`) based on the user's request. Drop a new `NAME_SUMMARY_PROMPT.md` next to SKILL.md to add a variant.

YouTube input is pre-processed via `YOUTUBE_SUMMARY_TEMPLATE.md` (needs `yt-dlp`), then fed to the chosen summary prompt.

## Install

```bash
./build.sh
```

Builds `target/the-summarizer/`, zips it, and copies to `$SKILL_INSTALL_DIR` (defaults to `~/.claude/skills/`). Pass `--no-install` to stop after the zip.

## Layout

```
src/the-summarizer/
  SKILL.md
  DEFAULT_SUMMARY_PROMPT.md
  TAKE_SUMMARY_PROMPT.md
  YOUTUBE_SUMMARY_TEMPLATE.md
build.sh
README.md
CHANGELOG.md
```
