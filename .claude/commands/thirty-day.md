Generate the 30-day check-in email, structured questions, and retention indicators (for the human, not the new hire).

**Usage:** `/thirty-day [hire]`
Example: `/thirty-day marcus-chen`

If the hire argument is missing, ask: "Which hire?" before continuing.

---

**Step 1 — Read.**

1. `reference/onboarding-principles.md`
2. `companies/[company]/hires/[hire]/plan.md`
3. `companies/[company]/hires/[hire]/intake.md`
4. `companies/[company]/hires/[hire]/first-day.md` (if exists)
5. Any other hire files in `companies/[company]/hires/` to check for pattern flags
6. `companies/[company]/profile.md`
7. `templates/thirty-day-checkin-template.md`

---

**Step 2 — Fill the check-in template.**

Substitute every `{{variable}}`. Notes:

- The two role-specific questions (positions 6 and 7 in the questions list) should be tailored to the role + intake. Examples:
  - For an engineer with on-call timeline: "How is on-call shadow week going?" or "Where are the gaps in the on-call ramp?"
  - For a hire who flagged HIPAA-naïve: "How is the HIPAA training pacing — too fast, too slow, right?"
  - For a new parent: "Is the schedule working? What needs to flex?"
- Proposed times: suggest 3 slots in the next 5 business days, 30 min each, avoiding any time the intake flagged as a conflict.
- The internal section (retention indicators + pattern flags) is for the human, not the hire. The agent surfaces. The human decides.

---

**Step 3 — Generate retention indicators (internal section).**

Read the plan.md, intake, and any signal you have. List indicators that, if true, the human should look at. Examples of the kind of indicator:

- Personal context flagged in intake (new parent, partner job change) — has the schedule held?
- Specific Day 30 milestone from plan.md — is the hire on track?
- Things the candidate cared about in the interview (comp band walk, on-call timeline) — were they delivered?

The agent never says "Marcus is a flight risk" or "we should give Marcus a raise." The agent says "Marcus asked about the comp band in the interview; the band walkthrough is scheduled for Day 7. Confirm it happened."

---

**Step 4 — Generate pattern flags.**

Look across `companies/[company]/hires/` for other recent hires in similar roles. If two or more hires have surfaced the same issue (thin training, missing context, slow access, manager unavailable), surface it. If there's only one hire in the directory, the section says: "First hire in this dataset; no pattern signal yet."

---

**Step 5 — Write the file.**

Write to `companies/[company]/hires/[hire]/thirty-day.md`. The file has two clearly labeled sections:

```
# 30-Day Check-In — [Hire Name]

## Section 1: For [Hire First Name]
[The filled-in check-in email, ready to send]

---

## Section 2: For [Manager First Name] and [HR Lead First Name] only
[Retention indicators]
[Pattern flags]
[Suggested follow-ups for the human to consider — never recommendations]
```

The file separator and section labels are non-negotiable. The internal section must never be sent to the new hire.

---

**Step 6 — Mock-send.**

Print:

```
[mock] 30-day check-in email drafted
       To: [candidate_email]
       From: [hr_lead_email]
       Cc: [manager_email]
       Subject: [subject_from_draft]
       Proposed times: [3 slots]
       Status: draft — needs HR review before send

[mock] Internal retention brief delivered
       To: [hr_lead_email], [manager_email]
       Subject: Internal — [hire] 30-day signals
       Status: sent (internal only)
```

The check-in email is a draft because it's going to a new hire and the language matters; HR reviews. The internal brief goes through to manager + HR only.

Then print:

```
[hire_first_name]'s 30-day artifacts are in [path].

The agent surfaced [N] indicators and [M] pattern flags. None of these are recommendations.
The decisions stay with you.
```
