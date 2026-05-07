Generate Day 0 morning Slack post, Week 1 calendar, and the manager handoff brief.

**Usage:** `/first-day [hire]`
Example: `/first-day marcus-chen`

If the hire argument is missing, ask: "Which hire?" before continuing.
If the hire's `plan.md` does not exist, suggest `/learn-company` first.

---

**Step 1 — Read.**

1. `reference/onboarding-principles.md`
2. `companies/[company]/hires/[hire]/plan.md`
3. `companies/[company]/hires/[hire]/intake.md`
4. `companies/[company]/hires/[hire]/preboarding.md` (if exists)
5. `companies/[company]/profile.md` — for team neighborhoods, all-hands cadence, on-call rotation if applicable
6. `templates/manager-prep-template.md`

---

**Step 2 — Generate three artifacts in one file.**

Write to `companies/[company]/hires/[hire]/first-day.md`:

```
# First Day — [Hire Name]
[start_date]

---

## Artifact 1: Day 0 morning Slack post

Channel: #general (or company equivalent)
Post time: 9:30 AM ET (after the new hire is settled)

[Draft of the Slack message. ~80-120 words. First-person from the team — "everyone, this is [name]". Specific to this hire — names the team, names what they'll work on, names something interesting from their background that the manager pre-cleared. Not generic. Includes a fun fact only if the intake mentioned something the candidate volunteered.]

## Artifact 2: Week 1 calendar

| Day | Time | Meeting | Attendees | Duration | Notes |
|---|---|---|---|---|---|
| Day 1 | 9:00 | Welcome breakfast | [hire] + [manager] | 60m | In office |
| Day 1 | 10:30 | IT setup | [hire] + Jason (IT) | 45m | |
| Day 1 | 12:30 | Team lunch | [hire] + [team] | 90m | On the company |
| Day 1 | 2:00 | Tools walkthrough | [hire] + [buddy] | 60m | |
| Day 1 | 4:00 | Day 1 debrief | [hire] + [manager] | 30m | |
| Day 2 | ... | ... | ... | ... | ... |
| Day 3 | ... | ... | ... | ... | ... |
| Day 4 | ... | ... | ... | ... | ... |
| Day 5 | ... | ... | ... | ... | ... |

[Fill in Days 2-5 with: 1:1 with each direct teammate (30m each), all-hands intro, comp/benefits walkthrough with HR, the first compliance training block (90m, calendar-blocked), buddy check-ins, end-of-week 1:1 with manager.]

[For roles with on-call: include "On-call shadow plan kickoff" by Day 5.]
[For new parents flagged in intake: avoid 8am or 6pm meetings; flag this explicitly in Notes column.]

## Artifact 3: Manager handoff brief

[Generate this using manager-prep-template.md. Fill every {{var}} from the intake and the plan. Specifically:

- candidate_summary: 4-5 lines distilled from intake
- interview_strengths: from interview notes in intake
- watch_fors: from manager's interview notes + any flags surfaced
- candidate_motivations: what they cared about in the interview process
- personal_context: anything the candidate volunteered (new parent, partner job, etc.) — only what they chose to share
- day_one_manager_ask: specific to manager (e.g., "walk through team architecture")
- week_one_manager_ask: 1:1 cadence + the comp band conversation
- day_thirty_manager_ask: the milestone from plan.md
- comp_band_walkthrough: where this hire sits in the band per profile.md
- oncall_plan: if applicable, the timeline from plan.md

This is the load-bearing artifact. It is the thing that usually doesn't get written.]

---

## Open questions for the human

[Anything the agent could not decide. Examples:
- Buddy assignment — manager picks
- Welcome lunch venue
- Whether to introduce in #general or in team channel first]
```

---

**Step 3 — Mock-send.**

After writing the file, print:

```
[mock] Day 0 Slack post drafted, scheduled for [start_date] 9:30 AM ET
       Channel: #general
       Status: draft — needs manager approval before posting (other employees see it)

[mock] Week 1 calendar drafts ready
       [count] invites drafted, manager review required before send

[mock] Manager prep brief delivered
       To: [manager_email]
       Subject: Prep brief — [hire] starts [start_date]
       Status: sent
```

The Slack post and calendar are drafts — they reach other employees, so they do not auto-send. The manager brief is for the manager only and goes through.

Then print: "First-day artifacts in [path]. Next milestone: 30 days post-start. Run `/thirty-day [hire]` then."
