---
description: Draft a YouTube script in the creator's voice for a given topic, grounded in real examples from the research bundle.
---

You're drafting a YouTube script for the {{client_name}} channel.

**Topic / hook idea:** $ARGUMENTS

## Process

1. **Read the audience profile.** Open `10-channel-research/researched/icp-avatar.md`.
   Anchor the script in what this audience actually cares about, frustrates them,
   what they're here to learn.

2. **Read the channel's voice + pillars.** Open `10-channel-research/researched/channel.md`.
   Note the documented tone phrase. Note the 4 content pillars. The script should
   live inside one of them (or explicitly bridge two).

3. **Find relevant examples.** Open `10-channel-research/researched/examples-bank.md`.
   For the topic above, identify any analogies, concrete examples, frameworks, case
   studies, credentials, or origin-story material that could ground the script.
   Don't pad — only pull what genuinely fits the topic.

4. **Sample the voice from transcripts.** Read 2–3 transcripts of high-view videos
   (`transcripts/001-*.md` through `transcripts/005-*.md`) — pay attention to:
   - The opening hook structure
   - Specific phrasing patterns / signature phrases
   - How the creator transitions between sections
   - How they handle proof / examples / receipts

5. **Check competitor positioning.** Skim `competitors/_index.md`. Identify what
   {{client_name}} does on this topic that competitors don't (or vice versa). The
   script should lean into the differentiation.

6. **Draft.** Produce a script with:
   - **Hook** (~30–60 seconds) — modeled on a top-performing real opening from
     transcripts. Cite which transcript inspired the structure.
   - **Body** — concept-by-concept. Every concept must include a concrete example
     pulled from `examples-bank.md` or `transcripts/`. Cite the source.
   - **Close + CTA** — match how the creator typically closes, based on what you
     observed in transcripts.

## Hard rules (from CLAUDE.md)

- Don't write "use a strong hook" without showing the actual hook. Don't write
  "personalize cold email" without quoting a real personalized email example.
- Don't invent quotes, frameworks, case studies, credentials, or origin-story
  fragments. Cite or skip.
- Match the documented tone. No drift into generic YouTube-script vocabulary.

## Output format

Use markdown headings: `## Hook`, `## Body`, `## Close`. Inside each section, write
the actual script content (what the creator would say to camera). Inline cite each
example with a markdown link to its source: `(see transcripts/008-cold-email.md)`.

After the script, add a brief `## Notes for the creator` section listing:
- Which examples you used and why
- Anything you couldn't find a grounded example for (so the creator can decide
  whether to record one)
