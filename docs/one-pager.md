# Building an Agent — One-Pager

**An agent is a loop with judgment, tools, and boundaries.** You write the boundaries. The model brings the judgment. You point it at the loop.

> If you do something more than once a day, turn it into a command. That's the trigger condition for everything else.

## The three levels

| Level | What | Where |
|---|---|---|
| **Global rules** | Apply to every project. Your voice, defaults, things you're tired of saying. | `~/.claude/CLAUDE.md` · `~/.codex/AGENTS.md` · ChatGPT custom instructions |
| **Project rules** | Apply to one codebase or workflow. Standards, vocabulary, constraints. | `CLAUDE.md` or `AGENTS.md` at project root |
| **Skills** | Procedural knowledge — *how* a specific job gets done, in what order, with what judgment. | `.claude/commands/[skill].md` (markdown files) |

## Skill anatomy

```
SKILL.md
---
name: post-intake
description: Draft post-intake email after founder call.   ← trigger
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

**Agent enforces structure. Human keeps judgment.** Comp numbers, terms, ratings, retention calls — those stay with you. Drafts, schedules, reminders, pattern-surfacing — those are the agent's.

Every skill needs at least one human checkpoint before any send.

## Where this leaves off

Most workshops stop at "you can build a skill." The part founders skip — and where production deployments break — is the **orchestration layer**. Multiple agents handing off context, state across steps, retries that don't loop. Worth knowing it exists. Real shipping fixes it; reading doesn't.

## Resources

- **The agent we built:** [github.com/whoamialt/onboarding-agent](https://github.com/whoamialt/onboarding-agent)
- **Workshop curriculum, written up:** [docs/agent-primer.md](https://github.com/whoamialt/onboarding-agent/blob/main/docs/agent-primer.md)
- **Why every choice in this repo:** [docs/why-this-shape.md](https://github.com/whoamialt/onboarding-agent/blob/main/docs/why-this-shape.md)
- **Anthropic skills library:** [github.com/anthropics/skills](https://github.com/anthropics/skills)
- **Gooseworks skills directory:** [skills.gooseworks.ai](https://skills.gooseworks.ai/)
- **Karpathy-style skills:** [github.com/forrestchang/andrej-karpathy-skills](https://github.com/forrestchang/andrej-karpathy-skills)
- **Caveman (multi-platform skill mgmt):** [github.com/juliusbrussee/caveman](https://github.com/juliusbrussee/caveman)

## Where to start (this week)

1. Pick the workflow you do most. Not the most interesting one — the most repetitive.
2. Write a 30-line `CLAUDE.md` or `AGENTS.md`. Voice, constraints, what done looks like.
3. Write one skill. Under 80 lines. Use the structure above.
4. Run it three times on three inputs. Tighten until variance is in the right places.

Stuck? Reply to my email with what broke. I learn most from where people get stuck.

— Sophie · [executive-function.substack.com](https://executive-function.substack.com)
