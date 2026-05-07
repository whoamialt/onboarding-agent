# Agent Primer

The workshop curriculum, written up. Use this as your reference when you build your own agent.

If something I said in the room conflicts with something here, this version is the one I stand behind — I sometimes phrase things tighter on the page than in the moment.

---

## The one thing I want you to leave with

> If you do something more than once a day, turn it into a command.

That's the trigger condition for building an agent or a skill. Not "is this AI-shaped?" Not "does this need automation?" Just: **am I doing this repeatedly, and is the thinking behind it consistent enough that I could write it down?**

If yes, write it down. The "writing it down" part is the agent.

---

## What an agent actually is

An agent is **a loop with judgment, tools, and boundaries.**

- **Loop:** the model reads context, decides on a step, takes the step, reads the result, decides on the next step. It keeps going until done.
- **Judgment:** it makes choices the procedure can't pre-determine — what to ask, how to phrase, what to skip.
- **Tools:** it can do things outside of generating text — read files, call APIs, hit a database, send an email.
- **Boundaries:** what it's allowed to do, what it must stop and ask about, what it never does.

When you build an agent, you're writing the boundaries and pointing it at the loop. The model brings the judgment. You bring the structure.

---

## The three levels — global, project, skill

Every agent runtime I've used (Claude Code, Codex, Antigravity) has the same three layers, even if they call them different things. Get this mental model and you can move between platforms.

### Level 1 — Global agent rules (wide)

Rules that apply to every project you start. "Always use first-person voice. Always show me the diff before committing. Never push to main without my approval." These are the things you get tired of saying.

In **Claude Code**: `~/.claude/CLAUDE.md` (user-level memory).
In **Codex**: `~/.codex/AGENTS.md`.
In **Antigravity**: similar global config.
In **ChatGPT**: custom instructions in your account settings.

### Level 2 — Project rules (specific)

Rules that apply only to this codebase / this project. Coding standards. Architecture decisions. Domain vocabulary. Who does what on this team.

In **Claude Code**: `CLAUDE.md` at the project root.
In **Codex / Antigravity**: `AGENTS.md` at the project root.
In **ChatGPT**: paste them at the top of every chat or pin them in a project.

This is where most of the value lives. A 100-line `CLAUDE.md` is worth more than a 10-page Notion playbook nobody reads.

### Level 3 — Skills (deep)

Skills are how you encode a specific workflow — the procedural knowledge of *how* a job gets done, in what order, with what judgment.

If your project rules say "we always do X carefully," skills say "here's exactly how to do X."

I'll go deep on skills below.

---

## The agent loop, in one paragraph

You hand the agent a goal and a starting context. The model reads the context. It decides on the next step (call this tool, write this file, ask this question). It takes the step. The result becomes new context. The loop continues until the goal is met or it gets stuck and asks you. That's it. Everything else — RAG, MCP, skills, multi-agent — is plumbing for that loop.

---

## What a skill actually is

A skill is a markdown file that tells the agent *how to do one specific job.* Not what — how.

The reason skills exist is that LLMs are extremely flexible reasoners but extremely inconsistent procedural workers. They'll write five different versions of the same email if you ask them five times. Skills fix that. They turn a flexible reasoner into a consistent procedural worker, for the jobs you've codified.

### Anatomy of a skill

The simplest skill is one markdown file:

```
SKILL.md
---
name: post-intake
description: Draft a post-intake follow-up email after a founder call.
---

Step 1 — Read these files:
  - companies/[name]/intake-notes.md
  - templates/post-intake-email.md

Step 2 — Draft the email. Requirements:
  - 300-400 words
  - First-person, direct, no consultant-speak
  - Open with something specific from the call

Step 3 — Show me the draft and ask:
  - "Is the tone right?"
  - "Anything to add or cut?"

Step 4 — Update tracker.md to note the email is drafted.
```

Three things matter:

1. **The description** is the trigger. The agent uses it to decide *when* to invoke the skill. Make it specific. "Draft a post-intake email" is good. "Help with onboarding stuff" is not.
2. **The body** is plain markdown — instructions, step-by-step workflows, rules. Written like you're handing it to a competent colleague.
3. **It's a file**, so it's version-controlled, copyable, shareable. You can move skills between platforms by moving the file.

### Optional folders inside a skill

If a skill needs more, you can add:

- `scripts/` — bash, Python, whatever the agent should run as part of the procedure
- `references/` — docs the agent should consult while doing the job
- `assets/` — data files, templates, images the agent uses

You don't need any of these for a basic skill. Add them as the procedure gets more complex.

### Progressive disclosure

This is the design pattern I like the most about how skills work in modern agent runtimes:

1. The skill's **description** is the table of contents — always loaded, lightweight, helps the agent decide when to use the skill.
2. The skill's **body** loads only when the agent decides to use the skill.
3. The optional folders (scripts, references, assets) load only when the body says they're needed.

That means you can have 50 or 100 skills available without burning context window on any of them until they're called for.

---

## Skill folder strategy (this matters at scale)

Free-tier Claude has a cap on how many skills you can store (around 50, in my experience). Pro is significantly higher. But beyond the platform limit, there's a *cognitive* limit — too many singular skills makes the agent worse at choosing the right one.

What I do: **one skill folder, many sub-skills as references.**

Instead of `design-color-system/`, `design-typography/`, `design-spacing/`, `design-components/` as four separate skills, I have one `design-suite/` skill with a body that says "when working on UI design, refer to references/[topic].md based on what's needed." The references contain the deep knowledge.

This gives me:
- One trigger condition for the agent to match against
- All the depth available when needed
- A natural place to grow without sprawl

---

## Skill vs MCP vs RAG vs fine-tuning

These get conflated. They're four different things doing four different jobs:

| Tool | What it gives the agent | What it doesn't |
|---|---|---|
| **Skill** | Procedural knowledge — *how* to do a job, in what order, with what judgment | Doesn't give it tools or facts |
| **MCP (Model Context Protocol)** | Tool access — APIs, files, services it can reach | Doesn't tell it *what* to do once it has access |
| **RAG (Retrieval Augmented Generation)** | Factual knowledge — pulls reference material into context | Doesn't teach it *how* to use the knowledge |
| **Fine-tuning** | Bakes knowledge into model weights — permanent, fast at runtime | Locked to a model version; if model changes, redo it |

The most common mistake I see: treating skills as if they were RAG, or treating MCP as if it were skills. They compose well, but they're not interchangeable.

When you ask "should I build a skill or hook up an MCP?" the answer is usually "both." Skills tell the agent *how*; MCP gives it the tools to do it.

---

## Multi-agent / multi-platform orchestration

A pattern I'm using more: let one model type be the orchestrator, and delegate chunks of the task to other models.

Concrete example: Claude orchestrates, Perplexity does the real-time web research, GPT does a final pass for tone variation. The orchestrator router decides which model gets which subtask based on what each is good at.

This is overkill for a solo workflow. It pays off when you're building a pipeline that runs frequently and the per-task quality differences matter.

If you want to try it, start with a `multi-platform-orchestration/` folder where each model has a sub-skill, and an orchestrator skill at the top that decides who handles what.

---

## Plan mode (and why it matters)

Most agent runtimes have a "plan first" mode that holds all writes until you've approved a plan. Use it. Especially when you're learning.

The reason isn't safety — it's calibration. Plan mode forces the agent to articulate what it's about to do before it does it. You catch wrong assumptions before they become wrong code or wrong emails. After a few weeks of using plan mode, your trust in the agent gets dramatically more accurate, in both directions.

In **Claude Code**: `/plan` or shift-tab.
In **Codex**: similar flag.
In **Antigravity**: built into the default flow.

---

## Definition of done — what a "good" agent looks like

When I'm building an agent and want to stop, I ask:

1. **Brief definition of done.** Could a colleague read the project rules and a skill and know what success looks like? If not, I haven't written it down well enough.
2. **Custom pipelines.** Can I run the same skill against different inputs and get coherent outputs? Or does it only work for the one example I built it on?
3. **Reasoning is visible.** When the agent makes a choice I didn't expect, can I see why?
4. **Consistency.** Run the skill three times on similar inputs. The outputs should rhyme. If they don't, the skill body is too vague.

If all four are yes, ship it.

---

## Resources

### Anthropic skills library

[github.com/anthropics/skills](https://github.com/anthropics/skills) — official examples. Read three or four of them. The pattern will click.

### Caveman (cross-platform skill management)

[github.com/juliusbrussee/caveman](https://github.com/juliusbrussee/caveman) — third-party tool that helps you manage skills across multiple agent runtimes. Worth a look if you're going multi-platform.

### This repo

[github.com/sophielemieux/onboarding-agent](https://github.com/sophielemieux/onboarding-agent) — the agent we built in the workshop. Clone it, run it, fork it, rebuild it for your own workflow.

### My writing

[executive-function.substack.com](https://executive-function.substack.com) — practitioner notes on building this stuff. New posts roughly monthly.

---

## What to do next

If you've never built an agent before, in this order:

1. **Pick the workflow you do most.** Not the most interesting one. The most repetitive one.
2. **Write the project rules first.** A 30-line `AGENTS.md` or `CLAUDE.md` describing the work and the voice and the constraints. That's your level 2.
3. **Write one skill.** The single most repetitive sub-task inside that workflow. Use the structure above. Keep it under 80 lines.
4. **Run it three times.** On three different inputs. See where it varies and where it's consistent. Tighten the body until the variance is in the right places (creativity) and not the wrong ones (procedure).
5. **Add a second skill.** When the first one feels like it works.

Don't try to build a whole system upfront. The system emerges from skills you actually use. The ones you don't use, delete.

---

If you're stuck, send me what you tried and where it broke. I learn from your stuck more than from anything else.
