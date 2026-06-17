# YouTube summary template

Pre-processing recipe for summarizing a YouTube video. This is not a summarization prompt - once the transcript is extracted, hand it to `DEFAULT_SUMMARY_PROMPT.md` (or whichever variant the user asked for) as the body of the `<text_to_summarize>` block.

## Requirements

`yt-dlp` must be installed:

```bash
brew install yt-dlp
```

If it's not available, tell the user and stop. Do not silently fall back to summarizing the video page's HTML - the description is not the video.

## Steps

1. Try human-written subtitles first:

   ```bash
   yt-dlp --write-sub --sub-lang en --sub-format srt --skip-download \
       -o "~/.cache/io.cote.ai.skill.the_summarizer/yt-transcript" <URL>
   ```

2. If no human subs exist, fall back to auto-generated:

   ```bash
   yt-dlp --write-auto-sub --sub-lang en --sub-format srt --skip-download \
       -o "~/.cache/io.cote.ai.skill.the_summarizer/yt-transcript" <URL>
   ```

3. If neither is available, report the error and stop.

4. Read the resulting `.srt` file. Strip the timestamps and cue numbers to get plain transcript text.

5. If the `.srt` is not in English, translate it to English first. If that's not possible, report back and stop - do not summarize.

6. Hand the cleaned transcript to the selected summarization prompt (default: `DEFAULT_SUMMARY_PROMPT.md`) wrapped in the standard input contract:

   ```
   <text_to_summarize>
   Source: [<video title>](<video URL>)
   Retrieved on: <today's date>

   <cleaned transcript text>
   </text_to_summarize>
   ```

## Notes

- The video's title and channel name go in the `Source:` line. Pull these from `yt-dlp --get-title` / `--get-uploader` if not obvious from the URL.
- Cache files in `~/.cache/io.cote.ai.skill.the_summarizer/` are disposable; safe to overwrite each run.
