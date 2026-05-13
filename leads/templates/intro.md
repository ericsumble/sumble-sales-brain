# Intro template

First-touch email to an inbound lead (someone who signed up to Sumble and showed up in a `*-leads-new-logos` channel). Voice rules from `docs/Sumble Sales Brain.md` (Inbound canonical pattern) apply: plain text, subject under 40 chars, under 100 words, no sentence over 20 words, no bullets, no numbered lists, no em-dashes.

## Subject

`A play for {their company / their motion}`

## Body

```
Hi {first_name},

Here's the play. {Specific non-obvious signal mapped to their product — the kind of thing only Sumble MCP would surface.} That combo is your {first-meeting list / in-market list}. ZoomInfo cannot tag that. Sumble can.

{Competitor 1 frame}. {Competitor 2 frame}. {Their company} wins on {their wedge}. Sumble finds the accounts where that wedge lands.

{Low-friction reply ask, not a meeting.}

Eric
Account Executive | Sumble
https://calendly.com/eric-sumble/30min
```

## Variables to fill before sending

- `first_name` — from Slack post or LinkedIn
- `their company / their motion` — subject anchor; use what they sell, not their domain
- The non-obvious signal — pulled via Sumble MCP (FindJobs, EnrichOrganization, etc.) before drafting
- Their competitive wedge — diagnose using the 6-question prospect diagnostic in `docs/Sumble Sales Brain.md`
- BCC: Salesforce email-to-record drop address (lives in Eric's local Claude memory)

## Hard rule: no warm-receipt openers

Drop "Welcome aboard." / "Welcome back." / "Saw you in this week." entirely. Salutation goes directly to the pitch. Ratified 2026-05-13 after reviewing the first 26 inbound intros — the warm line burns ~10 words of the 100-word budget on warmth that the signal-mapped play does better.
