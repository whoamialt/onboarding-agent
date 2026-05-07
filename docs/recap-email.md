# Workshop Recap Email — Draft (one-page version)

**Subject:** Workshop recap — agent + everything you need to start

---

Hi everyone,

Thanks for spending the hour with me today. Most of you came in not knowing what an agent actually was, and you all left having watched one get built end-to-end. That's a real shift, and I appreciated how you stayed with the harder parts.

Here's everything in one place so you don't have to dig.

## The agent we built (works without any code)

**[github.com/whoamialt/onboarding-agent](https://github.com/whoamialt/onboarding-agent)**

It's the onboarding agent we built live — runs the lifecycle from contract draft through the 30-day check-in for a (fake) Series A B2B SaaS company called Lattice Loom. Five skills. Two human checkpoints. Pure markdown, no code.

You don't need to be technical to use it. The README walks you through how to clone it and run it on Claude Code, ChatGPT, Codex, or Antigravity. If you've never opened a terminal before, you can also paste the skill files directly into a Claude or ChatGPT chat and ask the model to follow them — that works too.

**The recording (unlisted):** [TODO_REPLACE_WITH_VIDEO_LINK]

## The one thing I want you to leave with

> If you do something more than once a day, turn it into a command.

Not "is this AI-shaped?" Not "should I automate this?" Just: am I doing it repeatedly, and is the thinking consistent enough that I could write it down? If yes, that's the trigger. The "writing it down" part is the agent.

## The structure, in three lines

- **Global rules** = the things you're tired of saying. Voice, defaults. (Top-level user setting.)
- **Project rules** = how this one workflow works. Standards, vocabulary, constraints. (`CLAUDE.md` or `AGENTS.md` at the project root.)
- **Skills** = the procedure for one specific job. *How* it gets done, in what order, with what judgment. (One markdown file per skill.)

The doctrine that ties it together: **the agent enforces structure, the human keeps judgment.** Comp numbers, ratings, retention calls — those stay with you. Drafts, reminders, scheduling, surfacing patterns — the agent's job.

## Where to start this week

1. Pick the most repetitive thing you do — not the most interesting, the most repetitive. Sourcing emails. Intake notes. Onboarding setup. Whatever you do over and over.
2. Write 30 lines of project rules describing the work, the voice, and what "done" looks like.
3. Write one skill — under 80 lines — for the most repetitive sub-task.
4. Run it three times on three different inputs. Tighten until the variance is in the right places (creativity) and not the wrong ones (procedure).

That's it. Don't try to build a system upfront. The system emerges from the skills you actually use.

## What we didn't cover

The orchestration layer — multiple agents handing off context cleanly, state across steps, retries that don't loop. Most workshops never even get to "build a working skill," so I'm glad we did. But the part where production deployments break is orchestration, and no workshop fixes that without real shipping behind it. Worth knowing it exists. Happy to go deeper with anyone who wants to.

## Resources, by what they're for

**Watch / listen:**
- 🎧 **[How I AI podcast](https://www.youtube.com/@howiaipodcast)** — my favorite podcast on this. Practitioners showing how they actually work with AI. Start with [this episode](https://www.youtube.com/watch?v=LJ1YZ3Uek3g).
- 📹 **The workshop recording (above)**

**Build:**
- **[The agent we built](https://github.com/whoamialt/onboarding-agent)** — clone, run, fork
- **[Anthropic skills library](https://github.com/anthropics/skills)** — official examples; read three or four and the pattern clicks
- **[Gooseworks skills directory](https://skills.gooseworks.ai/)** — community catalog, browse it like a cookbook
- **[Karpathy-style skills](https://github.com/forrestchang/andrej-karpathy-skills)** — pedagogical shape reference

**Go deeper:**
- 🎓 **[HuggingFace Agents Course](https://huggingface.co/learn/agents-course/en/unit0/introduction)** — the course I took and recommend. Free, self-paced, much more depth than 60 minutes allows.
- **[Workshop curriculum, written up](https://github.com/whoamialt/onboarding-agent/blob/main/docs/agent-primer.md)** — the full version of what we covered
- **[Why every choice in the repo](https://github.com/whoamialt/onboarding-agent/blob/main/docs/why-this-shape.md)** — design decisions explained

## Stuck? Send me what you tried.

Truly — I learn most from where people get stuck. If you sit down to build a skill this week and it doesn't work the way you expected, reply to this email with what you tried and where it broke. I'll write back.

Thanks again for the hour.

Sophie

📩 *Reply directly* — *[sophielemieux.substack.com](https://sophielemieux.substack.com) (Unsupervised)*

*P.S. — If you want a tailored version of this for your team — recruiting, HR, ops — I run AI enablement sessions for People Ops teams. Reply if you'd like to talk.*
