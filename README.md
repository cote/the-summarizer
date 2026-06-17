# The Summarizer

A Claude Code skill that summarizes external content (article URLs, pasted text, PDFs, YouTube videos) into a tight prose form with a Take, highlighted key ideas, and a Hugo-ready output.

The skill picks among named prompt variants (e.g. `DEFAULT_SUMMARY_PROMPT.md`, `TAKE_SUMMARY_PROMPT.md`) based on the user's request. Drop a new `NAME_SUMMARY_PROMPT.md` next to SKILL.md to add a variant.

YouTube input is pre-processed via `YOUTUBE_SUMMARY_TEMPLATE.md` (needs `yt-dlp`), then fed to the chosen summary prompt.

## Install

### Option A: download the release zip

Grab [`dist/the-summarizer.zip`](dist/the-summarizer.zip) and unzip it into `~/.claude/skills/`:

```bash
curl -L -o the-summarizer.zip https://github.com/<user>/the-summarizer/raw/main/dist/the-summarizer.zip
unzip -d ~/.claude/skills/ the-summarizer.zip
```

### Option B: clone and build

```bash
./build.sh
```

Builds `target/the-summarizer/`, zips it, and copies to `$SKILL_INSTALL_DIR` (defaults to `~/.claude/skills/`).

Flags:

- `--no-install` — stop after the zip.
- `--package` — also copy the zip to `dist/the-summarizer.zip` and emit a CycloneDX SBOM at `dist/the-summarizer.cdx.json` (tracked release artifacts).

## Supply chain

Each release ships with a CycloneDX 1.5 SBOM at `dist/the-summarizer.cdx.json`. Validate it with:

```bash
cyclonedx-cli validate --input-file dist/the-summarizer.cdx.json
```

(`brew install cyclonedx-cli` if you don't have it.)

## Layout

```
src/the-summarizer/
  SKILL.md
  DEFAULT_SUMMARY_PROMPT.md
  TAKE_SUMMARY_PROMPT.md
  YOUTUBE_SUMMARY_TEMPLATE.md
dist/the-summarizer.zip      ← committed release artifact
build.sh
LICENSE
README.md
CHANGELOG.md
```
