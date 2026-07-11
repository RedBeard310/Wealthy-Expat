# Wealthy Expat — Writing Agent Repo

Specialized Claude Code workspace for writing scripts and ideating content for the
**Wealthy Expat** YouTube channel.

This repo is one half of a two-repo system:
- **Data-gathering agent** (separate repo) scrapes the channel + competitors into
  Airtable, then exports a markdown research bundle into this repo's
  `10-channel-research/` folder.
- **This repo** (the writing agent) reads that bundle plus any client-supplied
  assets, and helps draft scripts in the creator's voice.

## Quick start (after cloning)

```bash
cd "/Users/casey/Documents/_Stuff/Claude/Rafael - Wealthy Expat - Writing Agent"
claude        # opens Claude Code with CLAUDE.md auto-loaded
```

That's it. No env vars to set, no API keys to wire up. The repo is fully
self-contained — Claude Code reads the markdown files in `10-channel-research/`
on demand.

## What's where

- [INDEX.md](INDEX.md) — human-readable navigation map
- [CLAUDE.md](CLAUDE.md) — agent character + folder map (auto-loaded by Claude Code)
- `10-channel-research/` — the auto-generated research bundle (don't edit manually)
- `20-client-assets/` — frameworks, case studies, testimonials, sales pages (you fill these in over time)
- `30-call-transcripts/` — sales calls, onboarding calls, discovery calls (you add these)
- `.claude/` — agent subagents + slash commands

## Refreshing the research

The research data is owned by the data-gathering agent at:

  `/Users/casey/Documents/_Stuff/Claude/YouTube Channel Research v1`

To re-research and refresh this bundle:

```bash
cd /Users/casey/Documents/_Stuff/Claude/YouTube Channel Research v1

# Run the pipeline (or resume an existing run)
npx tsx scripts/run-channel.ts <youtube-url> --client wealthy-expat \\
  --business-model <...> --research-purpose <...>

# Export the run into this writing repo
npx tsx scripts/export-run.ts <run_id> --client wealthy-expat \\
  --out-dir "/Users/casey/Documents/_Stuff/Claude/Rafael - Wealthy Expat - Writing Agent/10-channel-research/"
```

Then back in this repo:

```bash
cd "/Users/casey/Documents/_Stuff/Claude/Rafael - Wealthy Expat - Writing Agent"
git add 10-channel-research
git commit -m "Refresh research from <run_id>"
git push
```

The export only touches `10-channel-research/`. Your `20-client-assets/`,
`30-call-transcripts/`, and any custom edits to `CLAUDE.md` / `.claude/` are
never overwritten.

## Adding your own materials

Drop files into the user-managed folders following the conventions in each
folder's `_index.md`. Update the relevant `_index.md` so the writing agent
knows what's there. Commit + push.
