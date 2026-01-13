# The AI Brief — Automated Newsletter

An automated daily AI newsletter built with Make.com, OpenAI API, and custom HTML email templates.

## Overview

The AI Brief is a daily newsletter that curates AI news from RSS feeds, processes it through GPT-4o-mini, and delivers a professionally formatted HTML email. Built for Sisyfos Studios as part of the "Embracing the climb" brand.

## Architecture

```
RSS Feed → Text Aggregator → OpenAI API → Gmail
   ↓            ↓                ↓           ↓
15 items    Structured      HTML email    Delivery
            text input      generation
```

## Newsletter Structure

1. **In Focus** — One sentence synthesizing the day's theme
2. **Today's Must-Knows** — 3 curated stories with context
3. **One Concept Explained** — Technical term explained simply
4. **Rabbit Hole** — 3 additional items for deeper reading

## Tech Stack

| Component | Tool |
|-----------|------|
| Automation | Make.com |
| AI Model | GPT-4o-mini |
| Email | Gmail API |
| RSS Source | TLDR AI |

## Files

| File | Purpose |
|------|---------|
| `system-prompt.txt` | Full system prompt including HTML template |
| `user-prompt.txt` | User prompt template for Make.com |
| `learning-log.md` | Development notes and lessons learned |

## Configuration (Make.com)

- **Timeout:** 120000ms
- **Max tokens:** 4000
- **RSS items:** 15

## Usage

1. Create Make.com scenario with modules: RSS → Text Aggregator → HTTP → Gmail
2. Paste `system-prompt.txt` into HTTP module's system message
3. Paste `user-prompt.txt` into HTTP module's user message (replace variables with Make.com chips)
4. Configure Gmail module with Raw HTML body type
5. Schedule to run daily

## Design Principles

- Minimal black-and-white aesthetic
- Editorial tone — "smart friend explaining over coffee"
- Mobile-first responsive design
- Cross-client compatibility (Gmail, Outlook, Apple Mail)

## Author

**Martin Lindholm**  
Sisyfos Studios  
[sisyfos.studio](https://sisyfos.studio)

## License

MIT — Free to use and adapt.
