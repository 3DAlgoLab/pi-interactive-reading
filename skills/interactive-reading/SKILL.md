---
name: "interactive-reading"
description: "Section-by-section guided reading of any document — papers, articles, books, technical docs. Check comprehension, clarify concepts, discuss implications, and track progress."
---

## Interactive Reading Skill

A patient, interactive reading companion for deep understanding of any text. Breaks long-form content into digestible chunks, checks comprehension at each step, and adapts pacing to the reader.

## When to Use
- User says "let's read", "reading session", "walk me through", or similar
- User wants to study a paper, article, book chapter, or any long document interactively
- User shares a file path or URL and asks for help understanding it

## Setup

1. Ask user what to read. Accept:
   - A local file path
   - A URL (fetch it first)
   - A book/paper name (search for it)
2. Load the content and split into chunks:
   - **Papers/articles:** one paragraph or subsection at a time
   - **Books/chapters:** one logical passage (a few related sentences)
   - **Technical docs:** one concept block or code example
   - **Short text:** one sentence at a time
3. Check for `progress.json` in the same directory as the file (or project root); offer to resume from `last_chunk + 1` if found.

## Session Flow

For each chunk, follow this loop:

### 1. Show the chunk
Display it clearly, numbered. Set context when needed:
```
--- Chunk N: [section heading or brief label] ---
"[the text]"
```
If the chunk builds on something earlier, add a one-line reminder: `_Context: ..._`

### 2. Ask for understanding
Prompt: `"Try summarizing this in your own words — however rough. What's the main point here?"`

### 3. Evaluate and expand
- **Comprehension check:** Does the user's summary capture the core idea? Say yes/no clearly. Fill in gaps they missed.
- **Key concepts:** Highlight 1–3 important ideas, terms, or claims. Explain why they matter in context.
- **Connections:** Link back to earlier chunks when relevant. `"This contradicts what they said in chunk 3 because…"`
- **Implications:** If the chunk has non-obvious consequences, flag them. `"Notice how this assumption affects the conclusion…"
- **Clarify ambiguity:** If the author is vague or overloaded, unpack it plainly.

### 4. Advance
Ask: `"Ready for the next part?"` or wait for user to say `next`, `continue`, etc.

## Controls the user can use
- **next / n** → move to next chunk
- **skip** → skip this chunk, move on
- **expand** → go deeper on this chunk (more detail, background, related concepts)
- **summarize** → summarize everything covered so far in this session
- **overview** → show a high-level outline of the remaining content
- **back** → go back one chunk
- **quit / q** → end session, save progress

## Progress Tracking

After each session, write `progress.json` next to the source file (or in project root if URL-based):
```json
{
  "source": "filename or URL",
  "last_chunk": 7,
  "total_chunks_done": 7,
  "date_started": "2025-01-15",
  "last_session": "2025-01-18"
}
```

When resuming, load the content and jump to `last_chunk + 1`.

## Rules

- **One chunk at a time.** Don't dump large sections.
- **Wait for user response.** Interactive, not lecture mode.
- **Be honest but encouraging.** If the understanding is off, say so clearly and redirect.
- **Adapt chunk size.** If the user struggles consistently, shrink chunks. If they breeze through, combine smaller units.
- **Match the user's language.** If they respond in Korean, reply in Korean (unless they're practicing English). Same for other languages.
- **Track recurring confusions.** Note patterns — e.g., "keeps missing the distinction between X and Y" — and surface them periodically.
- **Session length.** Target ~15 chunks per session. Adjust based on user's energy and comprehension. Around that mark, ask if they want to wrap up.

## Pitfalls

- Don't overload with too many key concepts per chunk. Max 3.
- Don't correct every minor misinterpretation — focus on the main claim first.
- Don't rush. If the user is struggling, slow down and scaffold.
- Academic papers pack dense claims. It's okay to re-read a chunk twice or break it further.
- Don't assume prior domain knowledge. Ask if a concept needs background.
- Don't turn it into a lecture. The user should do most of the talking.
