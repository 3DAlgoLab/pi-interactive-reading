# pi-interactive-reading

A [Pi](https://pi.dev) skill for section-by-section guided reading of any document.

## What it does

Breaks papers, articles, books, and technical docs into digestible chunks. After each chunk, it checks your comprehension, highlights key concepts, makes connections to earlier material, and adapts pacing to how you're doing.

### Features

- **Chunk-by-chunk reading** — no info overload
- **Comprehension checks** — summarize in your own words after each section
- **Progress tracking** — `progress.json` so you can resume where you left off
- **Adaptive pacing** — shrinks chunks if you struggle, combines them if you breeze through
- **Multi-language** — matches whatever language you respond in

### User Controls

| Command | Action |
|---------|--------|
| `next` / `n` | Move to next chunk |
| `skip` | Skip current chunk |
| `expand` | Go deeper on the current chunk |
| `summarize` | Summarize everything covered so far |
| `overview` | Show outline of remaining content |
| `back` | Go back one chunk |
| `quit` / `q` | End session, save progress |

## Install

```bash
# From npm (once published)
pi install npm:@3dalgolab/pi-interactive-reading

# From git
pi install git:github.com/3DAlgoLab/pi-interactive-reading@v1.0.0

# Local path
pi install /path/to/pi-interactive-reading
```

## License

MIT
