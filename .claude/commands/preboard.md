Generate the Day -7 → Day 0 preboarding task list with owners and draft artifacts.

**Usage:** `/preboard [hire]`
Example: `/preboard marcus-chen`

If the hire argument is missing, ask: "Which hire?" before continuing.
If the hire's `plan.md` does not exist, say so and suggest running `/learn-company` first.

---

**Step 1 — Read.**

1. `reference/onboarding-principles.md`
2. `companies/[company]/hires/[hire]/plan.md` — the synthesized plan
3. `companies/[company]/handbook.md` — for the tools list, benefits enrollment, compliance training
4. `companies/[company]/hires/[hire]/intake.md` — for any personal context (new parent, accessibility, etc.)
5. `templates/welcome-email-template.md`

---

**Step 2 — Build the preboarding task list.**

For every preboarding task, four things must be present:
- **What** the task is
- **Who** owns it (HR / IT / Manager / Agent)
- **When** it happens (relative to start date, e.g., "Day -5")
- **Artifact** — the thing the task produces (e.g., "IT ticket #1234", "Pre-filled HRIS form", "Welcome email draft")

Use the company's actual tooling (from `handbook.md`) for artifacts. If the company uses Apple Business Manager for laptops, the IT artifact is "ABM order placed for [model]" not "laptop ordered."

Tasks the agent owns are tasks the agent will draft a real artifact for. Tasks owned by HR / IT / Manager are tasks the agent generates a draft request for, but does not execute.

---

**Step 3 — Draft the artifacts the agent owns.**

In a single output file, write `companies/[company]/hires/[hire]/preboarding.md` with this structure:

```
# Preboarding — [Hire Name]
Start date: [start_date]

## Task list (Day -7 → Day 0)

| Day | Task | Owner | Artifact |
|---|---|---|---|
| Day -7 | Order laptop ([model]) via [system] | Ops | [artifact name] |
| Day -7 | Send IT account provisioning request | Agent | See "IT request" below |
| Day -5 | Pre-fill HRIS in [system] | HR | [artifact name] |
| Day -3 | Send welcome email | Agent | See "Welcome email" below |
| Day -1 | Confirm Day 1 logistics | Manager | [artifact name] |
| Day -1 | Calendar holds for Week 1 | Agent | See "Week 1 calendar" below |
| Day 0  | First-day kickoff | Manager + Agent | See `/first-day` |

## Artifact: IT request

[Drafted request to the IT contractor with the exact accounts to provision based on role + handbook tools list. Specific. Includes Yubikey count, AWS access level, PagerDuty if applicable.]

## Artifact: Welcome email

[Drafted welcome email using welcome-email-template.md, fully filled in with this hire's specifics. No {{vars}} remaining.]

## Artifact: Week 1 calendar holds

[List of meetings to schedule in Week 1, with attendees, duration, suggested time. Each entry says who the agent will create the invite for.]

## Open questions for the human

[Anything the agent could not decide. E.g., "Welcome lunch venue — manager preference?"]
```

---

**Step 4 — Mock-send the agent-owned artifacts.**

After writing the file, print, in this exact format:

```
[mock] IT request submitted to jason@latticeloom-it.com
       Subject: Provisioning request for [hire_name], starts [start_date]
       Status: sent

[mock] Welcome email scheduled for [date], 9am ET
       To: [candidate_email]
       Subject: [subject_from_draft]
       Status: scheduled

[mock] Week 1 calendar holds drafted ([count] invites)
       Attendees include: [first 3 attendees]
       Status: drafts ready for human review before send
```

Note that the calendar invites are drafts only — they do not "send" without human review, because attendees include other employees. This is a judgment checkpoint by design.

Then print: "Preboarding artifacts are in [path]. Next: on the start date, run `/first-day [hire]`."
