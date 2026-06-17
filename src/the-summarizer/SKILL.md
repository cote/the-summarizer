---
name: the-summarizer
description: >
  The Summarizer. Summarize external content (article URLs, pasted text, PDFs,
  YouTube videos) into a tight prose form with a Take, highlighted key ideas,
  and a Hugo-ready output. Picks a named prompt variant (DEFAULT, SHORT, TAKE,
  etc.) based on the user's request. Use when asked to summarize external
  content - not when asked to summarize your own output.
compatibility: Requires bash.
metadata:
  author: cote
  version: "1.0"
---

# The Summarizer

## Actions

Summarization prompts live next to this file as `NAME_SUMMARY_PROMPT.md`. Each file is one named variant. The shipped variants:

- `DEFAULT_SUMMARY_PROMPT.md` - the standard tightened-prose Hugo-ready summary

To add a new variant, drop a `NAME_SUMMARY_PROMPT.md` file in this dir (e.g. `SHORT_SUMMARY_PROMPT.md`, `BULLETS_SUMMARY_PROMPT.md`, `EXEC_SUMMARY_PROMPT.md`). Use the same input contract as DEFAULT so the caller doesn't have to change how they supply the source.

### Picking a variant

1. If the user names a variant explicitly ("use the SHORT variant", "give me a short summary", "exec summary"), match it case-insensitively to the `NAME` part of a `NAME_SUMMARY_PROMPT.md` file. List the dir and pick the closest match.
2. If the user supplies their own ad-hoc prompt inline, use theirs instead and keep the input contract.
3. Otherwise, use `DEFAULT_SUMMARY_PROMPT.md`.

Load the selected file's contents and apply them as-is to the supplied source (URL, pasted text, PDF, or video transcript).

### Source-specific templates

Some input types need pre-processing before they can be fed to a summary prompt. Those recipes live alongside the prompts as `NAME_SUMMARY_TEMPLATE.md`:

- `YOUTUBE_SUMMARY_TEMPLATE.md` - extract a YouTube video's transcript via `yt-dlp`, then hand the cleaned text to the selected summary prompt.

When the user provides a YouTube URL, run the YouTube template first, then apply the chosen summary prompt to its output. Same pattern applies to any future template (PDF, podcast, etc.).

## XDG Paths

| What | Location |
|------|----------|
| Config | `~/.config/io.cote.ai.skill.the-summarizer/` |
| Data | `~/.local/share/io.cote.ai.skill.the-summarizer/` |
| State | `~/.local/state/io.cote.ai.skill.the-summarizer/` |
| Cache | `~/.cache/io.cote.ai.skill.the-summarizer/` |
