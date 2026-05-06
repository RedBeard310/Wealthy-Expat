---
description: Find concrete examples for a specific concept from the research bundle. Returns verbatim quotes with transcript citations.
---

Find concrete examples in the {{client_name}} research bundle that ground this concept:

**Concept:** $ARGUMENTS

Process:

1. Open `10-channel-research/researched/examples-bank.md`. Look for items in any of
   the 6 sections (analogies, concrete examples, frameworks, case studies,
   credentials, origin story) that match the concept.
2. If the bank has 3+ relevant items, return the best 3.
3. If the bank has 0–2, also `Grep` `10-channel-research/researched/transcripts/`
   for keywords from the concept and surface anything you find.
4. Read the cited transcript for full context around each quote.

For each example you return, give:
- **The verbatim quote** (with light cleanup of fillers — no rewriting)
- **Source:** markdown link to the transcript file
- **Why it grounds the concept:** one sentence

If you genuinely can't find any real example for this concept in the research,
say so explicitly. **Don't invent examples and don't fall back to generic ones.**
The writer needs to know honestly whether this concept is or isn't already grounded
in {{client_name}}'s content.
