# Default summarization prompt

The default behavior when this skill is invoked without an override. Take the linked article or pasted text and produce a tight, prose-only summary that keeps the conceptual depth but removes bloat, repetition, drift, and filler. Do not mimic the original writer's voice; use a neutral, analytic tone. No bullet points unless they appear in the source.

## Formatting

1. Begin with a Markdown header.
2. Produce 3 to 6 paragraphs of tightened prose.
3. Highlight the key points with `<mark>the mark HTML tag</mark>` and major insights so the reader can scan quickly.
4. No bullets, no lists, no "the author argues..." style attribution. Just the distilled ideas.
5. If there is jargon or a less-known concept, use a markdown footnote to briefly describe it.

Once you do this, break the paragraphs up into just one to three sentences, with the bolder key points as their own paragraph. This helps make it easier to read without losing content from the original summary.

## Content rules

- Preserve the core arguments, tensions, and stakes.
- Clarify and compress; remove anecdotes, rhetorical flourishes, and digressions.
- Reorder ideas if it improves clarity.
- Keep it adult, direct, and concise.
- No moral disclaimers or softening language.
- Do not add judgements or editorialization of your own, only summarize what is in the original.

## Output rules

- Title is Techmeme-style, prefixed with `🤖`.
- The next line is: `_Original: [The title of the piece](URL for the piece) by AUTHOR. Summarized by AI on DATE_`
- Then `# The Take`. In one paragraph, state the single core point of the piece directly and declaratively - force a thesis even if the source hedges. No attribution ("the author argues," "Thompson says"); just assert the claim as the piece's stake. Keep it tight: what the piece is really saying and why it matters.
- For highlighting, use the `<mark>` HTML tag, not `<strong>` or `**markdown strong**`. Always the HTML mark tag.
- Make the result a markdown file the user can save.
- Do not ask for next steps or more actions at the end; just output the summary.

## Output structure

````markdown
# 🤖 Bach Copied Vivaldi for Years: Why Surface Imitation Fails and Collision Produces Originality

_Original: [Bach Copied Vivaldi for Years: Why Surface Imitation Fails and Collision Produces Originality](https://www.joanwestenberg.com/how-to-be-inspired-without-copying/) - Joan Westenberg. Summarized by Claude AI on May 19, 2026._

# The Take

[the take you come up with per above instructions]

# Summary

Paragraph 1 with highlighted key ideas.

Paragraph 2 with highlighted key ideas.

Paragraph 3 with highlighted key ideas.

...etc.

## Links

🤖 [How to be inspired without copying](https://www.joanwestenberg.com/how-to-be-inspired-without-copying/) - Surface imitation fails because it copies the visible artefact instead of the hidden process that produced it. Real influence works as collision, and LLMs have made the surface free while leaving the apprenticeship - and the judgement it builds - as the only thing that still matters.
````

## Input contract

The caller supplies the source like this:

```
<text_to_summarize>
Source: [Article title](Article URL)
Retrieved on: <date>

<markdown body of the article, or pasted text>
</text_to_summarize>
```

If the input is a URL only, fetch it and treat its rendered content as the body. If it's a PDF, YouTube video, or other non-HTML source, transcribe/extract first, then apply the same rules.
