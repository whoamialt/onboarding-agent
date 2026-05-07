# Why This Shape

A walkthrough of every design decision in this repo, with the reasoning. If `agent-primer.md` is the theory, this is the worked example.

Read this if you want to build your own agent and you're trying to figure out why I made the choices I did. Where I made a choice, I'll say why. Where you should make a different choice, I'll say so.

---

## Why this is markdown only, no code

You'll notice this whole agent has zero Python, zero JavaScript, zero database. Just markdown files.

This is a deliberate choice for a teaching artifact. The agent works because the model reads instructions written in plain English. If the agent were 200 lines of Python wrapping an LLM, you'd be learning my Python — not how agents work.

For your own agents:

- **Start with markdown only.** Force yourself to write the whole procedure as prose first.
- **Add code only when you hit a real wall.** Calculations the model gets wrong. Side effects the model can't trigger by writing text.
- **The wall is much further out than you think.** I've shipped client work with agents that are 100% markdown.

---

## Why three context layers (company, hire, doctrine)

The agent reads three folders' worth of files on every skill: company info, hire intake, and the doctrine in `reference/onboarding-principles.md`.

The reasoning: each layer changes at a different cadence.

- **Doctrine** changes almost never. It's the immutable rules.
- **Company** changes every few months. New policies, new tools, new comp bands.
- **Hire** changes every onboarding.

By splitting them, I can update one without touching the others. When Lattice Loom changes its hybrid policy, I edit `handbook.md` and every future hire's onboarding inherits the change. I don't go editing skills.

For your own agents: **separate things that change at different speeds.** Don't put policy in skills. Don't put procedure in policy.

---

## Why the doctrine is its own file

`reference/onboarding-principles.md` could have lived inside `CLAUDE.md`. I split it out because:

1. Every skill instructs the agent to read the doctrine first. Having it as its own file makes the instruction unambiguous.
2. If I want to teach the doctrine in a workshop without the rest of the repo, I can hand someone that one file.
3. Future me will probably want to write a `recruiting-principles.md`, `performance-principles.md` — same shape, different content.

For your own agents: **if the same idea is referenced more than twice, give it its own file.**

---

## Why CLAUDE.md AND AGENTS.md (and not just one)

Different runtimes look for different filenames. Claude Code reads `CLAUDE.md`. Codex and Antigravity read `AGENTS.md`. I keep both, with the same content, so the agent works regardless of which platform you open it in.

There's an argument for symlinking them. I don't, because some platforms struggle with symlinks in cloud environments. Two real files is cheap and bulletproof.

For your own agents: **commit both, keep them in sync.** When you edit one, edit the other. Yes it's redundant. Yes it's worth it.

---

## Why five skills, not three or ten

Each skill maps to a phase of onboarding that has a clear input, a clear output, and a clear handoff to the next phase.

- `/learn-company` → `plan.md`
- `/send-contract` → `contract.md` + mock-send
- `/preboard` → `preboarding.md`
- `/first-day` → `first-day.md`
- `/thirty-day` → `thirty-day.md`

I considered combining `/preboard` and `/first-day` into one skill. I split them because they fire on different triggers (acceptance vs start date) and have different audiences (HR/IT vs Manager + new hire). Combining them would have made the body of the skill 200 lines and harder to reason about.

For your own agents: **split skills along trigger and audience boundaries, not along "this feels like a thing" boundaries.**

---

## Why every skill follows Step 1 / Step 2 / Step 3 / Step 4

The repetitive structure isn't laziness — it's calibration.

When every skill has the same shape (read context → do work → write output → mock-send or pause for human), the model gets faster at executing them. It's the same reason cooking recipes have a structure and not just prose.

For your own agents: **pick a shape and use it everywhere.** It doesn't have to be mine. But pick one.

---

## Why the human-judgment checkpoints are mandatory

Two checkpoints are non-negotiable:

1. `/send-contract` stops for explicit y/n before mock-sending.
2. `/first-day` and `/preboard` flag employee-facing drafts (Slack post, calendar invites) as drafts the manager must approve before they go out.

Could the agent decide on its own? Yes. Should it? No. Two reasons:

1. **Stakes.** A contract that goes out wrong is recoverable but expensive. A Slack post in #general that misnames the team is mildly humiliating and has to be deleted. The cost of the y/n is 30 seconds. The cost of getting it wrong is much higher.
2. **Pedagogical clarity.** When demoing this agent, the y/n is the moment everyone in the room *gets* what "structure vs judgment" means. Removing it would remove the lesson.

For your own agents: **think about your worst-case wrong action and where the agent would have to decide.** Add a checkpoint there.

---

## Why mock-sends are printed strings, not real API calls

The skills print `[mock] DocuSign envelope sent` instead of actually calling DocuSign. For this demo:

- **Reliability.** Live API calls fail in front of audiences. Auth tokens expire. Networks blip. None of that is the lesson, all of it derails the lesson.
- **Resettability.** I can re-run the demo back-to-back without sending five real DocuSign envelopes to my own email.
- **Transparency.** The audience can read exactly what *would* be sent, in plain text, on the screen. That's more pedagogical than a black-box API call returning success.

For real production use, you'd swap the printed string for a real tool call (probably via MCP). The skill body stays the same; only the side effect at the end changes. That's the value of the structure.

For your own agents: **build with mocks first. Swap to real tools when the structure is solid.** Not the other way around.

---

## Why the fake company has so much detail

`profile.md` has 65 lines. `handbook.md` has 80 lines. Neither is strictly necessary — the agent could probably produce something passable from a 10-line "Lattice Loom is a B2B SaaS in Boston" description.

But it would produce *generic* output. Generic onboarding artifacts are worse than no onboarding artifacts; they look right and aren't.

The detail in the company files is what lets the agent produce visibly tailored output during the demo. When the agent says "Marcus needs HIPAA training because Lattice Loom serves healthcare staffing," it's not making that up — it pulled it from `profile.md`. That specificity is what makes the demo land.

For your own agents: **the quality of the agent's output is bounded by the quality of the context.** If the output is generic, the input was generic.

---

## Why Marcus has a partner with a new job and a 6-month-old

Look at `intake.md` for Marcus. There's a paragraph:

> Marcus mentioned his partner is starting a new job same week and they have a 6-month-old at home. Flagged he may need flexibility in first two weeks.

I added that on purpose. It tests whether the agent surfaces personal context into the plan (it should — the start of week 2 daycare drop-off shouldn't collide with the 9am all-hands). It's the kind of detail that real intakes contain and that real onboarding fails to handle.

For your own agents: **build your test cases with friction.** Make the data hard. The agent that handles a perfect intake well is not the agent you actually need.

---

## Why the 30-day skill has two sections, separated visibly

`thirty-day.md` produces a file with two clearly labeled sections: one *for* the new hire (the check-in email), one *for* HR + manager only (retention indicators and patterns).

The separator is non-negotiable in the skill prose. The reason: it would be very easy for an unsuspecting reader to copy the whole file into an email and accidentally send the internal section to the new hire. The visible separator + label prevents that.

For your own agents: **when one artifact contains content for different audiences, make the boundary impossible to miss.** Visual, textual, structural. Don't rely on the reader paying attention.

---

## Why the agent surfaces patterns but never recommends actions

The doctrine says: "Marcus mentioned on-call training was thin — second hire to flag this in 30 days" is a valid agent output. "We should restructure the on-call rotation" is not.

The reason isn't ideological — it's about decision rights. The agent doesn't have the org context to decide that on-call should be restructured. It might cost $20K in eng time. There might be a planned restructure already. The manager might disagree about the diagnosis. None of that is in the agent's context window.

But the *pattern* — two hires said the same thing — is a clean signal the agent absolutely can produce. Surfacing the signal lets the human make the decision with the data the agent assembled.

For your own agents: **let the agent do the part it's actually better at than humans.** Pattern-matching across many inputs is one of those parts. Org-level decision-making is not.

---

## Where I'd cut

If I were building this for a single client and not a teaching artifact, I'd:

- Drop the templates folder. Inline the templates into the skills. Less indirection.
- Drop the second judgment checkpoint and let `/first-day` send drafts as previews. The first checkpoint is the load-bearing one.
- Add real Gmail and Calendar MCP integration. Replace the mocks with actual sends.

I kept all of those because they make the *teaching* clearer. For real production use, simplify.

For your own agents: **the version you teach with and the version you ship are usually different.** Ship the simpler one.

---

If you build something using this shape, send it to me. I want to see how you bent it.
