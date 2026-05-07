# Building an Agent — One-Pager

**An agent is a loop with judgment, tools, and boundaries.** You write the boundaries. The model brings the judgment. You point it at the loop.

> If you do something more than once a day, turn it into a command. That's the trigger condition for everything else.

## Chat vs workflow vs agent — when do I use which?

|  | **Chat** | **Workflow** | **Agent** |
|---|---|---|---|
| You give it | A question + context | A goal + every step in order | A goal + constraints |
| It gives you back | An answer | A repeatable execution | A judgment-aware execution |
| You feel like | A user | A micromanager | A manager of a skilled employee |
| Adapts to context? | Per conversation | No — runs steps as written | Yes — reads, adjusts, asks |
| Best for | One-off drafts, research | Same procedure, every time | Work that needs procedure *and* judgment |

**Decision rule:** chat first. Workflow if you need consistency. Agent only if the work needs to adapt to context. Don't reach for an agent when a workflow will do.

## The three levels — where rules live

| Level | What | Where |
|---|---|---|
| **Global** | Apply to every project. Voice, defaults, things you're tired of saying. | `~/.claude/CLAUDE.md` · `~/.codex/AGENTS.md` · ChatGPT custom instructions |
| **Project** | Apply to one workflow. Standards, vocabulary, constraints. | `CLAUDE.md` or `AGENTS.md` at project root |
| **Skill** | *How* one specific job gets done — order + judgment. | One markdown file per skill |

## Skill anatomy

```
---
name: post-intake
description: Draft post-intake email after founder call.   ← this is the trigger
---
Step 1 — Read: intake-notes.md, template.md
Step 2 — Draft (300-400 words, first-person, no consultant-speak)
Step 3 — Show me, ask "tone right? anything to cut?"
Step 4 — Update tracker.md
```

Description = trigger. Body = procedure. Add `scripts/`, `references/`, `assets/` only when needed.

## Skill vs MCP vs RAG vs fine-tuning

- **Skill** = how (procedure)
- **MCP** = what tools the agent can reach
- **RAG** = factual knowledge it can look up
- **Fine-tuning** = baked into the model weights

They compose. They're not interchangeable.

## The doctrine

**Agent enforces structure. Human keeps judgment.** Comp numbers, terms, ratings, retention calls — those stay with you. Drafts, schedules, reminders, pattern-surfacing — those are the agent's. Like managing a skilled employee, not micromanaging a workflow.

Every skill needs at least one human checkpoint before any send.

## How to actually run it

**Three modes** (Claude Code, Codex, Antigravity all have versions):
- **Ask permissions** — agent asks before each action. Start here.
- **Plan mode** — agent writes a plan, you approve, then it executes. Use for ambiguous tasks.
- **Auto mode** — runs autonomously. Use only when you trust the procedure.

**My usual flow:** plan mode for the build, then ask permissions for the day-to-day execution.

**Brief definition of done.** Before the agent starts, tell it what "good enough" looks like. *"My definition of done is X."* This forces both of you to agree on success up front. Skips most of the rework.

## Where this leaves off

Most workshops stop at "I built one skill that works." The part that gets skipped — and where production deployments break — is the **orchestration layer**: multiple agents handing off context, state across steps, retries that don't loop. Worth knowing it exists. Real shipping fixes it; reading doesn't.

## Resources

**Watch / listen:**
- 🎧 [How I AI podcast](https://www.youtube.com/@howiaipodcast) — practitioners on how they actually use AI; start with [this episode](https://www.youtube.com/watch?v=LJ1YZ3Uek3g)

**Build:**
- [The agent we built](https://github.com/whoamialt/onboarding-agent) — clone, run, fork
- [Anthropic skills library](https://github.com/anthropics/skills) — official examples
- [Gooseworks skills directory](https://skills.gooseworks.ai/) — community catalog
- [Karpathy-style skills](https://github.com/forrestchang/andrej-karpathy-skills) — pedagogical shape reference
- [Caveman](https://github.com/juliusbrussee/caveman) — multi-platform skill management; also useful when context windows balloon

**Go deeper:**
- 🎓 [HuggingFace Agents Course](https://huggingface.co/learn/agents-course/en/unit0/introduction) — free, self-paced; the course I took and recommend
- [Workshop curriculum, written up](https://github.com/whoamialt/onboarding-agent/blob/main/docs/agent-primer.md)
- [Why every choice in the repo](https://github.com/whoamialt/onboarding-agent/blob/main/docs/why-this-shape.md)

## Where to start (this week)

1. Pick the workflow you do most. Not the most interesting one — the most repetitive.
2. Decide: is it chat, workflow, or agent? (Default: workflow. Step up only if it needs to adapt.)
3. Write a 30-line `CLAUDE.md` or `AGENTS.md`. Voice, constraints, definition of done.
4. Write one skill. Under 80 lines. Use the structure above.
5. Run it three times on three inputs. Tighten until variance is in the right places.

Stuck? Reply to my email with what broke. I learn most from where people get stuck.

— Sophie · *[Unsupervised](https://sophielemieux.substack.com)*
