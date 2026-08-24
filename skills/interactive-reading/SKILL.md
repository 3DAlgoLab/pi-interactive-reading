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
   - **Spoken content (YouTube / podcast transcripts):** clean and rewrite first (see below), then one topic beat per chunk
3. Check for `progress.json` in the same directory as the file (or project root); offer to resume from `last_chunk + 1` if found.

## Spoken Content: Clean Before Chunking (YouTube / Podcasts)

Raw transcripts are noisy — filler words, slang, off-topic tangents, ad reads, repeated jokes. Never chunk them raw. Run two passes instead:

**Pass 1 — Clean (once, over the whole transcript):**
- Strip filler and false starts: "um, uh, so, you know, I mean, like, yeah," mid-sentence restarts, repeated sentences.
- Cut what is off the main topic: sponsor/ad reads, channel self-promo, audience banter, jokes, personal anecdotes that do not serve the topic.
- Remove slang that carries no information. If a slang term or phrase is central to the topic itself, keep it and plan to explain it as a key concept.
- For long transcripts, save the cleaned text next to `progress.json` (e.g., `<name>.cleaned.md`) so a resumed session reuses it instead of re-cleaning.

**Pass 2 — Rewrite (per chunk, at display time):**
- Rewrite each chunk as short, plain sentences — one idea per sentence — following the speaker's own structure.
- Keep every claim, example, number, and stance from the transcript. Cut only noise. Never add facts or opinions that are not there.
- Display the rewritten chunk in step 1 (not the raw transcript lines). If the source has timestamps (e.g., YouTube), label the chunk with its start timestamp so the user can jump to that moment.

## Session Flow

For each chunk, follow this loop:

### 1. Show the chunk
Display it clearly, numbered. Set context when needed:
```
--- Chunk N: [section heading or brief label] ---
"[the text]"
```
If the chunk builds on something earlier, add a one-line reminder: `_Context: ..._`

### 2. Quiz for understanding
Instead of an open-ended summary, ask **1~5 medium-difficulty multiple-choice questions** about this chunk, plus **1~2 cloze (fill-in-the-blank) questions** built from the chunk's core sentences. Medium means they can't be answered by word-matching — the user has to actually grasp the claim, see a consequence, or catch a subtle detail.

- **Question types to mix:**
  - "What is the main claim / central idea of this passage?" (only one option truly captures it)
  - "Which conclusion follows from this?" / "What does X imply?"
  - "Why does the author say X?" (reason questions)
  - "Which statement would the author most likely agree / disagree with?"
  - "What would happen if this condition were different?" (counterfactual)
- **Cloze (fill-in-the-blank):** 1~2 per chunk. Take the chunk's core sentence (central claim or key concept) and blank out one content-critical word or phrase; the user fills the blank with their own words. Only blank words with one clear expected answer — a key term, a technical word, a causal/logical word (because, therefore, so), or a decisive number — never function words or words where many paraphrases would fit. Accept semantically equivalent answers as correct.
- **Distractors:** Make wrong options plausible but clearly wrong — a misreading, an overreach, a detail from another chunk, or a half-truth. No obviously silly options.
- **No position bias:** Vary where the correct answer falls. Across the questions in one chunk, at least 3 different letters must be the correct answer, and the same letter must never be correct twice in a row.
- **No length bias:** Keep all options at roughly the same length and level of detail. The correct answer must never be the longest or most elaborately worded option — distractors must match it, or the answer is guessable without reading.
- **Format:** Number each question, give options `A) …  B) …  C) …  D) …`. Ask them one at a time or in a small batch — don't bury the reader. Let the user answer with letters or free text.
- **Keep it focused:** 3–5 questions total per chunk (multiple-choice + cloze combined), and each should test something the chunk actually said. Don't quiz trivia; quiz understanding.

### 3. Evaluate answers and expand
Go through the answers one by one:
- **Correct:** Say so briefly, explain why the right option is right and why the tempting wrong one (if they hesitated) is a trap.
- **Wrong:** Don't just mark it wrong. Explain the reasoning gap — what clue or idea they missed, and why their pick doesn't hold. Then guide them to the right answer rather than saying it flat out.
- **Key concepts:** Highlight 1–3 important ideas, terms, or claims. Explain why they matter in context.
- **Connections:** Link back to earlier chunks when relevant. `"This contradicts what they said in chunk 3 because…"`
- **Implications:** If the chunk has non-obvious consequences, flag them. `"Notice how this assumption affects the conclusion…"`
- **Clarify ambiguity:** If the author is vague or overloaded, unpack it plainly.
- **Wrap-up:** End with a quick "got it?" and invite the user to summarize in their own words if they want extra practice — but don't require it.

### 4. Advance
Ask: `"Ready for the next part?"` or wait for user to say `next`, `continue`, etc.

## Controls the user can use
- **next / n** → move to next chunk
- **skip** → skip this chunk, move on
- **expand** → go deeper on this chunk (more detail, background, related concepts)
- **explain** → skip the quiz this time; explain the chunk directly instead of testing
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
