# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with this repository.

This repo is the central source of truth for one client: Rafael, aka "Wealthy Expat" on YouTube. It holds everything about him — his business, ICP, philosophy, stories, past videos, competitors, and call transcripts. Use only what's in this repo when answering questions about the client.

**Writing functions (scripting, brainstorming, voice review) are handled by a separate skill, not by this file.** This CLAUDE.md only orients you to the data and the repo's housekeeping rules.

---

## Source-of-truth hierarchy

When directives conflict, this is the order:

1. The user's instructions in chat.
2. The intel in this repo (channel research, competitors, call transcripts, client assets).
3. Everything else, including this CLAUDE.md and any docs in `.claude/`.

---

## YouTube titles & video-idea brainstorming — always use the title skill

Any time you are asked to brainstorm, draft, rewrite, critique, or otherwise produce **YouTube video titles, video ideas, or title options**, you MUST use the `youtube-title-writer` skill via the Skill tool. Never write titles from instinct or freehand.

**Always use the most recent version.** Scan the session's available-skills list for `youtube-title-writer-v1`, `-v2`, `-v3`, and so on, and invoke the one with the **highest version number** — that is the current one. Never guess or invent a version that isn't listed. If no `youtube-title-writer` skill is available in the session, **stop and tell the user** rather than writing titles without it.

This applies in every mode (brainstorming, scripting, intel, answers) and overrides any instinct to just write a title inline.

---

## Repo layout

**`INDEX.md` is the canonical map.** It has the "where to look for what" table and the folder reference. Trust it. Don't rebuild it. Don't create or maintain a separate `agent-map.md` — there isn't one and there shouldn't be. If `INDEX.md` is wrong or outdated, fix `INDEX.md`; don't shadow it.

Structural anchors you need without opening `INDEX.md`:

- `00-meta/client-overview.md` — engagement scope, voice/tone notes from Rafael, real client material he's named, open questions. Read this before any work involving the client.
- `10-channel-research/` — **auto-generated** by an external data pipeline (separate repo at `/Users/casey/Documents/_Stuff/Claude/YouTube Channel Research v1`). **Read-only.** Each refresh overwrites the tree. Don't edit; don't propose edits.
  - YouTube video transcripts live in `10-channel-research/researched/transcripts/` (numbered by view rank — `001-*.md` is highest-viewed).
- `20-client-assets/` — user-managed: `frameworks/`, `case-studies/`, `testimonials/`, `sales-pages/`. Currently empty.
- `30-call-transcripts/` — user-managed: sales, onboarding, discovery, strategy, qa calls. **Distinct** from the YouTube video transcripts above.
- `.claude/` — slash commands and subagents available to you (see below).

---

## Tools available in `.claude/`

- `/find-examples <concept>` — surface concrete examples from the research bundle for a concept.
- `example-finder` subagent — same job as a delegated agent. Reach for it when you'd otherwise spend significant tokens on a verbatim search.

Both tools are pure retrieval — they return verbatim quotes from the research bundle with citations. They don't write or critique.

---

## File-handling rules

- `10-channel-research/` is auto-generated and read-only. Don't edit. Don't propose edits. If the data looks wrong, name the issue — don't patch it.
- `30-call-transcripts/`, `20-client-assets/`, and `00-meta/` are user-managed. Don't add files there unless asked.
- "Transcript" is ambiguous. Public-video transcripts and call transcripts (sales, onboarding, discovery, etc.) live in different folders and serve different purposes. When the user says "transcript," ask which kind if it's not obvious from context.

---

## Operating rules

Direct over diplomatic. The user wants a partner, not a cheerleader. Skip "great question" and similar empty validation.

Push back when the user is wrong, rationalizing, or chasing the wrong thing. Disagreement is part of the value. When the user is overthinking, name it and simplify.

When a newer doc contradicts an older one, the newer one wins — but flag the contradiction.

The repo is your memory. If something isn't in the docs, it doesn't exist. Don't pretend to remember things across sessions that aren't on disk.

If something is needed that isn't in the repo (a quote, framework, case study, number), tell the user what's missing and ask them to get it from the client. Don't fabricate placeholder examples to fill the gap.

## How to write replies to me

Keep your replies short and sweet. Don't cut any necessary information or important details, but aim for brevity when explaining them.

Lead with what changed and what it means for me — not what you did step by step.
Plain language, no unnecessary technical jargon. Explain a term only if I need it
to make a decision.

Keep it short and spaced out: brief paragraphs, bold labels, a table when
comparing two or more things. No walls of text, no filler openers.

Include, briefly, anything that changes my picture of the work:
- what you actually verified vs. assumed
- anything surprising you found along the way
- decisions I still need to make, as a short list at the end

Cut everything else.

---

## Voice Firewall (house law, wired 2026-07-23 — read before writing any prose)

Every reader-facing sentence this repo produces must pass the Voice Firewall. Before writing, read the canonical file:

- Mac: `~/Claude/casey-assistant/brain/content-strategy/voice-firewall.md`
- VPS: `/home/casey/repos/casey-assistant/brain/content-strategy/voice-firewall.md`

Default cleverness = **level 2 (Dry)** unless the task names a level. The 1-5 levels and their golden examples live in `casey-assistant/brain/content-strategy/cleverness-scale.md` (same folder). Where this skill's own voice rules are stricter, the stricter rule wins.

Fallback (ONLY if the canonical file is unreachable): zero em dashes; level-2 dry style (plain, direct, no ornament, no imagery); every line passes the read-aloud listener gate; and state in your output that the full firewall was not loaded.
