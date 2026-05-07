Learn a company's onboarding context and synthesize a tailored plan for a specific new hire.

**Usage:** `/learn-company [company] [hire]`
Example: `/learn-company lattice-loom marcus-chen`

If either argument is missing, ask: "Which company and which hire?" before continuing.

---

**Step 1 — Read the three layers, in this order.**

1. `reference/onboarding-principles.md` — the doctrine. Read this every time.
2. Company layer:
   - `companies/[company]/profile.md`
   - `companies/[company]/handbook.md`
   - `companies/[company]/onboarding-template.md`
3. Hire layer:
   - `companies/[company]/hires/[hire]/intake.md`

Do not draft anything before reading all five files.

---

**Step 2 — Synthesize what's specific to this hire.**

Pull from the company files what applies to *this role at this company*. Examples of the kind of specificity required:

- If the hire is on a team that carries on-call: pull the on-call timeline and stipend from `handbook.md` and the squad-specific cadence from `profile.md`.
- If the company has a hybrid policy and the hire is local vs remote: pull the in-office days and any relocation clause.
- If the company has compliance requirements and the hire is in a role that touches the relevant data: pull the training list and the deadline.
- If the intake flagged personal context (new parent, partner job change, accessibility need, visa): pull it forward into Week 1 / Week 2 sequencing.
- If the comp policy has role-specific exceptions (e.g., signing bonus only for senior eng), check the intake matches.

If three things from the company files don't show up specifically tailored in your output, you have not done the job.

---

**Step 3 — Write a tailored 30-60-90 plan.**

Write to `companies/[company]/hires/[hire]/plan.md`. Structure:

```
# Onboarding Plan — [Hire Name]

## Snapshot
[5-line summary: role, team, manager, start date, anything load-bearing from the intake]

## What this hire's onboarding has to cover (specific to this company + role)
- [3-6 bullets, each grounded in a specific company-file or intake detail]

## Day -7 → Day 0 (preboarding)
[Tasks with owners: HR / IT / Manager / Agent. Each task names the artifact it produces.]

## Day 0 (first day)
[Morning, lunch, afternoon, end-of-day. Each item has an owner.]

## Week 1
[1:1s, all-hands, comp/benefits walkthrough, tool training. Owners + dates.]

## Day 30 milestone
[What "good" looks like at Day 30. Specific to this role.]

## Day 60 milestone
[Same.]

## Day 90 milestone
[Same.]

## Open questions for the human
[What the agent could not decide and why. e.g., "comp band walkthrough timing — Day 7 or Day 14?"]
```

---

**Step 4 — After writing.**

Print, in this order:

1. The path to the file you just wrote.
2. A 3-bullet summary of what's specifically tailored ("Picked up X from profile, Y from handbook, Z from intake").
3. A line that flags any human-judgment items: "Open questions for you to resolve: [count]. See bottom of plan.md."

Do not run any other skill. Do not mock-send anything. This skill only produces the plan.
