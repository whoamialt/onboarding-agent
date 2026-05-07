Draft an offer letter for a hire and pause for human approval before mock-sending.

**Usage:** `/send-contract [hire]`
Example: `/send-contract marcus-chen`

If the hire argument is missing, ask: "Which hire?" before continuing.
If the hire's `plan.md` does not exist, say so and suggest running `/learn-company` first.

---

**Step 1 — Read.**

1. `reference/onboarding-principles.md`
2. `companies/[company]/profile.md` — for compensation philosophy and signer
3. `companies/[company]/handbook.md` — for benefits summary, work model, compliance training list
4. `companies/[company]/hires/[hire]/intake.md` — for comp terms, start date, role
5. `templates/contract-template.md`

The company is inferred from the intake file path. If multiple companies have a hire with this name, ask which one.

---

**Step 2 — Fill the template.**

Substitute every `{{variable}}` in the template with the right value, sourced from the files above. Notes:

- Comp numbers must come from the intake, not invented.
- Benefits summary should be 4-6 bullets distilled from `handbook.md`, not the full handbook.
- The work model clause must reflect the company's actual hybrid/remote policy and any individual accommodation flagged in intake.
- Role-specific terms should include any commitments specific to this role: on-call timeline for engineering, sales target ramps for AE roles, etc.
- Compliance list should pull only the trainings required for this role, not all of them.
- Offer expiry: 7 days from today's date.

If you cannot find a value for a variable, leave it as `{{variable}} ← FILL` and flag it explicitly. Do not invent.

---

**Step 3 — Write the draft.**

Write to `companies/[company]/hires/[hire]/contract.md`.

---

**Step 4 — Show the draft and ask for approval. This is the load-bearing checkpoint.**

After writing the file, print:

```
Draft contract written to: [path]

Read it. Three things to check:
1. Comp numbers match the intake.
2. Role-specific terms reflect what was actually agreed.
3. The work model clause matches the hire's geography and any flagged accommodation.

Proceed to mock-send? (y/n)
```

**Wait for the human's response.** Do not proceed without an explicit "y" or "yes". Do not infer approval.

---

**Step 5 — On "y": mock-send.**

Print, in this exact format:

```
[mock] DocuSign envelope created
       Recipient: [candidate_email]
       Subject: Your offer from [company_name]
       Cc: [manager_email_if_known]
       Status: sent
       Expiry: [offer_expiry_date]
```

Then print: "Contract is in the candidate's inbox (mocked). Next: when accepted, run `/preboard [hire]`."

---

**Step 5b — On "n" or any other response: stop.**

Print: "Stopping. Edit the draft at [path], then re-run `/send-contract [hire]` when ready."

Do not retry. Do not ask follow-up questions. Stop.
