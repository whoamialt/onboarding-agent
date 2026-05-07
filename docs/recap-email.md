# Workshop Recap Email — Draft

**Subject:** Workshop recap — agent we built, resources, what to try next

**To:** [workshop attendees]

---

Hi everyone,

Thank you for spending an hour with me today. As promised, here's the agent we built in the room, the curriculum written up, and a short list of what to try next.

## Watch the recording

If you want to see the build itself — or send it to a teammate who couldn't make it:

**[Recording → Building AI agents with Claude](TODO_REPLACE_WITH_VIDEO_LINK)**

*(See note at bottom of email — the file is 236MB, too large for email; I'm uploading it to YouTube as unlisted / Drive — paste the link in once it's up.)*

## The agent we built

A built-from-scratch onboarding agent — it learns from a (fictional) Series A B2B SaaS company's information what onboarding requires for a specific hire, then runs the lifecycle from contract draft through 30-day check-in. Five skills, two human-judgment checkpoints, zero code (just markdown).

**Repo:** [github.com/whoamialt/onboarding-agent](https://github.com/whoamialt/onboarding-agent)

It works on Claude Code, OpenAI Codex, Google Antigravity, and basically any LLM you can paste markdown into. Setup instructions for each platform are in the README.

The fictional company is **Lattice Loom**. The hire is **Marcus Chen**. Both are entirely made up — this is what a teaching artifact looks like when you don't want to expose any real client information.

**To run it:** clone the repo, open it in your agent runtime, run `/learn-company lattice-loom marcus-chen`. The README walks through the 7-beat demo flow.

## The curriculum, written up

I covered a lot of ground in 60 minutes. The full version is here:

**[docs/agent-primer.md](https://github.com/whoamialt/onboarding-agent/blob/main/docs/agent-primer.md)** — the workshop curriculum, written up. Levels (global / project / skill), the agent loop, MCP vs RAG vs skills vs fine-tuning, multi-platform notes, what to do next.

If you remember one line: **if you do something more than once a day, turn it into a command.** That's the trigger condition for everything else.

## How the agent works (the visual)

I made a FigJam diagram showing the agent's loop, the five skills, and the two human-judgment checkpoints. Useful if you want to internalize the structure-vs-judgment doctrine before building your own:

**[FigJam diagram](https://www.figma.com/board/Z4LKLR2oGhDpWVzbmceYKY)**

## Why this shape

The thing I wanted to spend more time on in the room: the *reasoning* behind the shape of the agent. I wrote it up here:

**[docs/why-this-shape.md](https://github.com/whoamialt/onboarding-agent/blob/main/docs/why-this-shape.md)** — every design decision in this repo, with the why. Use it when you build your own and you're stuck on a structural choice.

## What to try next

In this order:

1. **Pick a workflow you do more than once a day.** Not the most interesting one. The most repetitive one.
2. **Open your agent runtime.** Claude Code, Codex, Antigravity, ChatGPT — whatever you have access to.
3. **Write a 30-line `CLAUDE.md` or `AGENTS.md`** describing the work, the voice, and the constraints. That's your project rules.
4. **Write one skill.** The single most repetitive sub-task inside that workflow. Keep it under 80 lines. Use the skills in this repo as a shape guide.
5. **Run it three times** on three different inputs. Tighten the body until the variance is in the right places (creativity) and not the wrong ones (procedure).

Don't try to build a whole system upfront. The system emerges from skills you actually use.

## Where this leaves off

The honest version of what we covered today: we got you to the point where you can build an agent and a skill that work *in isolation*. That's the foundation, and it's the part most workshops never even get to.

The part most founders skip — and the part I want to flag before you start building — is the **orchestration layer**. People build agents that work beautifully on their own but can't hand off context cleanly to the next agent or the next step. State management across agent steps is where production deployments fall apart. No workshop fixes that without real shipping behind it.

If your goal is "automate one thing I do every day," this repo gets you there. If your goal is "agents running my workflow end-to-end across multiple tools," that's a different set of muscles, and we should talk about it separately.

## Resources

- **[Anthropic skills library](https://github.com/anthropics/skills)** — official examples
- **[gooseworks skills directory](https://skills.gooseworks.ai/)** — searchable catalog of community skills, good for browsing patterns
- **[Andrej Karpathy skills (community pack)](https://github.com/forrestchang/andrej-karpathy-skills)** — skills modeled on Karpathy's teaching style; useful as a shape reference
- **[Caveman](https://github.com/juliusbrussee/caveman)** — third-party tool for managing skills across multiple agent runtimes
- **[My Substack](https://executive-function.substack.com)** — practitioner notes on building this stuff
- **The repo we built in the workshop:** [github.com/whoamialt/onboarding-agent](https://github.com/whoamialt/onboarding-agent)

## Stuck? Send me what you tried.

Truly — I learn from where people get stuck more than from anything else. If you sit down to build a skill this week and it doesn't work the way you expected, reply to this email with what you tried and where it broke. I'll write back.

Thanks again for spending the hour with me.

Sophie

---

*P.S. — If you want a deeper version of this in your org, I run AI enablement sessions tailored to People Ops teams. [Reply for details.]*
