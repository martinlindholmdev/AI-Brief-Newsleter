# Learning Log: The AI Brief (AI Daily Digest)

**Project:** Automated AI Newsletter  
**Dates:** 15–18 December 2025, 12 January 2026  
**Status:** Complete — Ready for 10-person test group  

---

## Project Summary

Built an automated daily AI newsletter using Make.com that fetches RSS feeds, processes them through GPT-4o-mini, generates a complete HTML email, and sends it via Gmail. The newsletter follows a professional editorial format with custom branding for Sisyfos Studios.

---

## Technical Stack

| Component | Tool |
|-----------|------|
| Automation | Make.com |
| RSS Source | TLDR AI feed (bullrich.dev) |
| AI Model | GPT-4o-mini (OpenAI API) |
| Email Delivery | Gmail |
| Template | Custom HTML (inline CSS) |

---

## Architecture

```
RSS Feed → Text Aggregator → HTTP (OpenAI API) → Gmail
   ↓            ↓                  ↓               ↓
15 items    Combine into      Generate HTML    Send email
            structured text   from prompt
```

---

## Key Problems Solved

### 1. Empty RSS Data Passing to AI
**Problem:** Text Aggregator showed empty fields — AI was inventing content.  
**Root Cause:** Field mapping used typed text instead of UI chips.  
**Solution:** Rebuilt aggregator template using Make.com's chip picker to select RSS fields correctly.  
**Learning:** In Make.com, variables must be inserted as "chips" from the UI panel, not typed manually.

### 2. Timeout Errors (40000ms exceeded)
**Problem:** HTTP module failed before AI could complete response.  
**Solution:** Increased timeout from 40000ms to 120000ms.  
**Learning:** Long prompts + large payloads + 4000 token output requires 60-90 seconds with GPT-4o-mini.

### 3. Truncated Output (Missing Footer)
**Problem:** Email cut off mid-sentence, footer missing.  
**Solution:** Increased max_tokens from default to 4000.  
**Learning:** HTML emails with inline CSS consume significant tokens. Always calculate: structure + content + styling.

### 4. Generic/Fabricated Content
**Problem:** AI output headlines like "New AI Tools Enhance Data Analysis" — completely invented.  
**Root Cause:** No RSS data reaching the AI due to field mapping issue.  
**Solution:** Fixed Text Aggregator mapping (see #1).  
**Learning:** When AI output is generic, trace data flow backwards to find where content disappears.

### 5. "Publication" Placeholder in Output
**Problem:** Meta lines showed "Publication · 2 min read" instead of actual source names.  
**Solution:** Added explicit instruction: "CRITICAL: Never output the word 'Publication' as a placeholder."  
**Learning:** GPT-4o-mini needs explicit constraints for edge cases. If something can be misinterpreted, it will be.

### 6. Inconsistent Headline Styling
**Problem:** Some headlines appeared bolder than others.  
**Root Cause:** HTML template had mixed font-weight values (400/500/600).  
**Solution:** Standardized all headlines to font-weight: 700.  
**Learning:** Email HTML requires explicit inline styles on every element — no inheritance assumptions.

### 7. Forbidden Verbs Still Appearing
**Problem:** "launches," "unveils," "ICYMI" appeared despite forbidden list.  
**Partial Solution:** Strengthened prompt language ("automatic failure if used").  
**Learning:** GPT-4o-mini is less strict at following constraints than GPT-4o. Accept some variance or upgrade model.

---

## Design Iterations

| Version | Changes |
|---------|---------|
| v1 | Basic structure, inconsistent styling |
| v2 | Fixed header contrast (#888→#aaa), standardized headlines |
| v3 | Added "One Concept" with subtitle (failed — too cluttered) |
| v4 (Final) | Section headers 15px, "One Concept Explained" with inline bold format |

---

## Final Newsletter Structure

1. **Header** — Sisyfos Studios, The AI Brief, Date
2. **In Focus** — One sentence synthesizing theme across stories
3. **Today's Must-Knows** — 3 stories with headlines + 2-3 sentence context
4. **One Concept Explained** — Technical term explained, tied to day's stories
5. **Rabbit Hole** — 3 additional items for deeper reading
6. **Footer** — Branding, tagline, generation timestamp

---

## Make.com Lessons Learned

1. **Chips not text** — Always insert variables via UI picker
2. **Timeout settings** — Increase for AI API calls (120000ms minimum)
3. **Debug by clicking bubbles** — Each module shows input/output after run
4. **Test with "Run once"** — Don't schedule until manual tests pass
5. **RSS feeds vary** — Check actual field names in output, don't assume

---

## Prompt Engineering Lessons

1. **Shorter prompts work better** — Reduced from ~1800 to ~1000 words
2. **Explicit > implicit** — "Never output X" beats "avoid X"
3. **Examples help** — Show good/bad headline examples in prompt
4. **Template in prompt** — For HTML generation, include exact structure
5. **Forbidden lists need emphasis** — Mark as "automatic failure"

---

## Email HTML Lessons

1. **Table-based layout** — Required for Outlook compatibility
2. **Inline CSS only** — Many clients strip `<style>` blocks
3. **Test multiple clients** — Gmail, Outlook, Apple Mail all render differently
4. **Mobile padding** — Add 100px+ bottom padding for phone navigation bars
5. **Contrast matters** — Grey text on dark backgrounds needs to be lighter than expected

---

## Skills Developed

- [x] Make.com scenario building
- [x] OpenAI API integration via HTTP module
- [x] RSS feed processing and aggregation
- [x] HTML email template design
- [x] Prompt engineering for structured output
- [x] Cross-client email testing
- [x] Systematic debugging of automation pipelines

---

## Metrics

| Metric | Value |
|--------|-------|
| RSS items processed | 15 per run |
| Stories in newsletter | 6 (3 Must-Knows + 3 Rabbit Hole) |
| API model | gpt-4o-mini |
| Max tokens | 4000 |
| Timeout | 120000ms |
| Estimated generation time | 30-60 seconds |

---

## Next Steps

1. Send to 10-person test group
2. Collect feedback via Google Form
3. Iterate based on real reader responses
4. Consider GPT-4o upgrade if verb compliance remains problematic
5. Add to Sisyfos Studios website when ready for public distribution

---

## Connection to AI Lead Pivot

This project demonstrates:
- **Automation design** — End-to-end workflow without code
- **API integration** — Working with LLM APIs in production
- **Prompt engineering** — Structured output generation
- **Product thinking** — UX decisions, editorial voice, brand consistency
- **Debugging methodology** — Systematic problem isolation

Portfolio-ready project showing practical AI application skills.

---

*Log created: 12 January 2026*
