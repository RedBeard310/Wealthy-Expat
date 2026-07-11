# 30-call-transcripts — User-Managed

Sales calls, onboarding calls, discovery calls, strategy sessions — anything
the writing agent should know about how the client talks to prospects and clients
in conversation.

The data-gathering agent never reads from or writes here. You add files manually.

## Filename convention

`{type}-{YYYY-MM-DD}-{name-or-prospect}.md`

Where `type` is one of:
- `sales` — sales call with a prospect
- `onboarding` — onboarding session with a new client
- `discovery` — discovery / scoping call
- `strategy` — strategy session with an existing client
- `qa` — internal Q&A or interview the client recorded

Examples:
- `sales-2026-04-15-john-doe.md`
- `onboarding-2026-04-22-acme-corp.md`
- `discovery-2026-05-01-prospect-name.md`

## Each file should contain

- Call date, type, attendees (with anonymization if needed)
- A 1–2 sentence summary at the top of what the call was about
- The transcript itself (or the parts of it that matter — not every "ums" and "uhs")
- Optional: tagged moments — the writing agent will read these but it's also
  useful to surface what's worth remembering

## What's currently here

- [`onboarding-2026-05-08-rafael.md`](onboarding-2026-05-08-rafael.md) — first onboarding call between Casey (scriptwriter) and Rafael. Locks the trial-engagement scope, the three trial video topics, the content-type hierarchy, voice/tone notes, and the real client material Rafael named on the call. Header section above the raw transcript is the structured summary.
