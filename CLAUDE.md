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

Default cleverness = **level 2 (Dry)** unless the task names a level. The 1-5 levels and their golden examples live in `casey-assistant/brain/content-strategy/cleverness-scale.md` (same folder). Where this repo and the Law differ, the Law wins (the old "stricter wins" tie-breaker was retired 2026-07-28). Its clarity core is Clear Writing, in the managed block below.

Fallback (ONLY if the canonical file is unreachable): zero em dashes; level-2 dry style (plain, direct, no ornament, no imagery); every line passes the read-aloud listener gate; and state in your output that the full firewall was not loaded.

<!-- LLM-SPEND-GUARD v1 — managed block; keep identical in every repo -->
## LLM Spend Guard (house law — applies in every repo)

**Subscription chat is fine.** Work billed to a subscription plan (Claude Code on the Max plan, Codex on a ChatGPT plan, whatever the tool) needs no disclosure — just do the task.

**LLM API credits require disclosure BEFORE starting.** If a task will spend metered LLM API credits from ANY provider (Anthropic, OpenAI, OpenRouter, Gemini, Groq, etc.) — including launching a script, pipeline, or service that makes LLM SDK/API calls — the output must state, before the task begins:

- that it will spend API credits, and which provider/key (key by NAME only, never the value)
- a rough dollar estimate

**Estimated ≥ $1 → hard stop.** Do not start the task until Casey explicitly approves the spend.

**Scope: LLM usage only.** Non-LLM paid APIs (Deepgram, Apify, SmartLead, YouTube, etc.) are exempt from this rule.

**Limitation:** this governs chat-initiated work. Headless automation that is already running doesn't re-read this file mid-run; the rule applies at the moment a session starts, modifies, restarts, or triggers that automation.
<!-- /LLM-SPEND-GUARD -->

<!-- SUBSCRIPTION-NOT-API v1 — managed block; writing-agent slim variant -->
## Subscription, not API (house law)

Headless `claude -p` in automation bills Casey's Max subscription, never the Anthropic API. Never let `ANTHROPIC_API_KEY` into a spawned claude's environment, and never pass `--bare`. Full law with the three protection layers: `~/Claude/casey-assistant/CLAUDE.md`, same section.
<!-- /SUBSCRIPTION-NOT-API -->

## Model Policy (house law)

If an LLM call is ever added to this repo, its model comes from a committed `models.json`, never from code or env. Full standard: `~/Claude/casey-assistant/brain/infrastructure/model-policy.md`.

<!-- REPORTS-AND-ARTIFACTS v1 — managed block; writing-agent slim variant -->
## Reports & Artifacts (house law)

An HTML report never lives only as an artifact URL. Save it under `casey-assistant/reports/<domain>/`, publish, and open it with the share-link banner; a client report also mirrors byte-identical to this repo's `50-reports/`, with casey-assistant canonical. Full standard: `~/Claude/casey-assistant/brain/infrastructure/reports-and-artifacts.md`.
<!-- /REPORTS-AND-ARTIFACTS -->

<!-- CLEAR-WRITING v1 — managed block; keep identical in every repo -->
## Clear Writing (house law — wired 2026-08-06)

**Every piece of prose a person will read passes through Clear Writing.** Chat replies, emails, docs, reports, READMEs, notes, commit messages, slide text, Notion pages, client deliverables. No exceptions, in any repo.

**The one bar:** *if a smart high-schooler couldn't follow the idea on the first pass, rewrite it.* Assume the reader knows nothing about the business, hasn't read your other work, and won't read the sentence twice.

The rules, short version:

1. **Read it cold as the person who'll read it.** If a line needs the thinking behind it explained, it fails.
2. **Define at first use, then restate simpler.** The definition can't contain the confusion. Defining jargon with jargon fails.
3. **Bridge anything unfamiliar** to something they already know ("it's kinda like..."), then retire the bridge. One analogy per idea, taught in full sentences, connected back once, then back to literal words.
4. **Zero em dashes.** Commas for asides, periods for full thoughts. Carve-outs: the "— Casey" sign-off and structural separators in a locked template.
5. **No corporate filler** (unlock, leverage, elevate, move the needle), **no strategist vocabulary** in reader-facing text (funnel, ICP, pain point, install a belief), **no LLM dialect** ("here's the kicker"), **no hedging** (maybe, I think, sort of).
6. **No "not X, it's Y" as decoration.** Legal only when swapping an old belief the reader actually holds.
7. **Unpack compressed phrasing.** "A see-it-coming cost" becomes "a cost you can see coming." If a phrase squeezes an action into a metaphor or a hyphen stack, say the action.
8. **No bumper-sticker closers.** End on the actual mechanic in literal words, never an aphorism.
9. **Two links is the ceiling on a causal chain.** State the conclusion and trust the reader.
10. **Contractions on.** Talk TO the reader. Contraction-free essay prose is its own AI tell.
11. **Concrete beats abstract.** Specifics over adjectives, a worked example over an elegant abstraction, the believable number over the impressive one.
12. **Never present an invented specific as a real fact.** Ask for it instead.

**Cleverness runs at level 2 (Dry) by default**, everywhere. Plain and direct, no ornament. A format skill may name a different default for its own format (long-form scripts run at 3).

**Full standard** (read it before any substantial writing or rewrite job):

- Mac: `~/Claude/casey-assistant/brain/content-strategy/clear-writing.md`
- VPS: `/home/casey/repos/casey-assistant/brain/content-strategy/clear-writing.md`
- Skill: `clear-writing` (invoke it for rewrite jobs; it carries the linter at `scripts/lint.mjs`)

**Scope note.** Clear Writing is a clarity standard, not a persuasion standard. It carries none of the YouTube machinery: no proof stacking, no multiple analogies per idea, no Give Then Gap hook, no CTA rules, and no abrupt ending. **A normal conclusion is allowed.** That machinery stays in `script-writing-long-form-writing-skill-v3`. For writing another person will read, the Voice Firewall still outranks this block, and format skills add structure on top. Neither may loosen the bar above.
<!-- /CLEAR-WRITING -->

<!-- NOTION-ACCESS v1 — managed block; writing-agent slim variant -->
## Notion Access (house law)

`NOTION_API_TOKEN` in the shared env reaches Notion from any repo, machine, or headless run. The claude.ai connector is a per-session convenience, not the way in; never report Notion unreachable because a connector isn't signed in. Never print or commit the token. Full recipe (pagination, version pin, ID parsing, 404 = not shared): `~/Claude/casey-assistant/brain/infrastructure/notion-access.md`.
<!-- /NOTION-ACCESS -->

<!-- YOUTUBE-KEY-POOL v1 — managed block; writing-agent slim variant -->
## YouTube API Key Pool (house law)

Read `YOUTUBE_API_KEY_1..N` out of the shared env and use however many are there; never hard-code a key count, and never copy keys into a local `.env` (a local copy freezes the pool). RapidAPI is retired; if every direct key is exhausted, the answer is more keys. Rotate past dead keys: `quotaExceeded` and `keyInvalid` retire a key for the run, other 403s (like `commentsDisabled`) propagate without burning one. Full law, pool history, and the Notion source of truth: `~/Claude/casey-assistant/brain/infrastructure/youtube-api-key-pool.md`.
<!-- /YOUTUBE-KEY-POOL -->
