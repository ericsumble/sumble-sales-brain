# Leads tracker

Lightweight system to track new Sumble leads from Slack ✅ reactions through intro + two follow-ups, until reply or opt-out.

State of this system as of 2026-05-12: contains 31 contacts from the first ✅-pass across the 9 `*-leads-new-logos` channels.

## How a lead enters the system

Manual trigger: Eric reacts ✅ to a Sumble bot post in any of the nine `{sam,eric,unassigned}-p{0,1,2}-leads-new-logos` channels. That reaction is the signal to draft outreach.

To pull the current ✅'d set, ask Claude: *"Scan the 9 leads channels for messages I've reacted to with ✅."* Claude uses Slack's `hasmy::white_check_mark:` search filter against each channel ID.

## The flow per contact

1. Add to `contacts.json` with `status: not_contacted`.
2. Before any draft, scan Gmail (`to:<email>` query). If a thread exists, pivot to re-engagement angle (different play, different signal — see `templates/`).
3. Draft intro using `templates/intro.md`. Save as Gmail draft. Record `intro_sent` date, `gmail_thread_id`, `last_message_id`.
4. +4 days, no reply → draft follow-up #1 from `templates/followup-1.md`, threaded into the same Gmail thread via `replyToMessageId`. Record `followup_1_sent`.
5. +10 days from intro, still no reply → draft follow-up #2 from `templates/followup-2.md`, threaded. Record `followup_2_sent`.
6. After follow-up #2 with no reply → status moves to `paused`. No more automated drafts. Manual re-engagement only.
7. Any reply at any stage → status moves to `replied`. Continue conversation manually (no more templated drafts).
8. Opt-out at any time → add email to `opt-out.md`. Tracker will skip them on all future runs.

## Status enum

- `not_contacted` — in tracker, no email sent yet
- `contacted_no_reply` — intro sent, awaiting reply, before follow-up #1 window
- `followup_1_sent` — first follow-up sent, awaiting reply
- `followup_2_sent` — second follow-up sent, awaiting reply
- `paused` — finished cadence with no reply; manual action only
- `replied` — they replied; continue manually
- `active` — actively in conversation / meeting set
- `opted_out` — never message again

## Files

- `contacts.json` — state for every contact ever entered
- `opt-out.md` — emails to never message (authoritative; tracker honors this over `contacts.json`)
- `templates/intro.md` — first-touch template
- `templates/followup-1.md` — +4d follow-up
- `templates/followup-2.md` — +10d follow-up

## What this does not do

- **Does not auto-send.** Every email lands in Gmail as a draft for Eric to review.
- **Does not auto-detect new ✅ reactions.** Run the Slack scan manually (or on a cadence).
- **Does not run on a cron.** Claude executes the cadence checks when Eric runs the routine.

## Note on the Sales Brain doc

The root `docs/Sumble Sales Brain.md` (line 5, line 659) was written when this repo was *knowledge only* — no automation, no state machine. This tracker introduces a `contacts.json` state file, which is a deliberate departure. Voice rules and email shape are inherited from the Sales Brain unchanged; only the operational layer is new.
