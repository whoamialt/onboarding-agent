# Building agents, live — session recap

*A recap of the live-build session: what I covered, what we built together, and the resources to keep going.*

> The designed (HTML/PDF) version of this lives at `docs/one-pager.html`. This markdown version is the same content, version-controlled and easy to copy.

---

## What we did today

Two weeks ago we did the theory session — what an agent is, when to build one, how teams should work alongside them. The feedback from the survey was clear: thanks for the theory, now show us how to actually build one. So today was the live build.

We picked onboarding because almost everyone in the room has a version of it on their plate. I built the agent from scratch in Claude Code while you watched — fictional company, fictional new hire, five skills, two human checkpoints, no real client info anywhere on screen.

The thing I most want you to leave with is the mental model, not the agent. The agent is a teaching artifact. The mental model is what you'll use on Tuesday morning.

---

## The mental model — chat, workflow, agent

The most-asked question in the survey was the difference between these three. Here's how I think about it.

**Chat** is a conversation. You ask, it answers, you have to provide the context every single time. Good for one-offs and brainstorming. Not good for anything you do over and over because you're re-loading context every time. *You feel like a user.*

**A workflow** is a procedure. You write down every step in order, and the workflow runs the same procedure the same way every time. Onboarding checklists. Weekly reports. Sourcing-to-screen handoffs. The win is consistency. The cost is that you have to write every step. *A workflow makes you a micromanager.*

**An agent** is the thing you reach for when the work has to adapt. Not just "do these steps in order" but "here's the goal and the constraints, figure out the right approach for this case." Onboarding a senior IC is different from onboarding an intern. Sourcing for a fractional exec is different from sourcing for an entry-level associate. An agent reads the situation, picks the right approach, asks when stuck. *You're not micromanaging anymore — you're managing a competent employee.*

> Chat first. Workflow if you need the same thing every time. Agent only if it has to adapt. Don't reach for an agent when a workflow will do.

For me, "agent territory" usually means more than one workflow, more than one skill, and the work has to read the situation before it acts. Every step up the ladder costs more — more setup time, more tokens, more debugging surface. Don't pay that cost unless the work needs it.

---

## What we built

**[github.com/whoamialt/onboarding-agent](https://github.com/whoamialt/onboarding-agent)**

Five skills, two human checkpoints, zero code. Pure markdown. Works on Claude Code, Codex, Antigravity, or anywhere you can paste markdown into a chat.

- `/learn-company` — reads company files + intake, drafts a tailored 30-60-90
- `/send-contract` — drafts the offer letter, stops, asks "send? y/n"
- `/preboard` — Day -7 → Day 0 with owners (HR, IT, Manager, Agent)
- `/first-day` — Day 0 morning + Week 1 calendar + manager handoff
- `/thirty-day` — check-in email + retention indicators (internal section, not for the hire)

The fictional company is **Lattice Loom** — Series A B2B SaaS, healthcare-adjacent, hybrid Boston, 35 people. The new hire is **Marcus Chen** — Senior Backend Engineer, joining a team that carries on-call, has a partner starting a new job the same week, has a 6-month-old at home, has never touched HIPAA. I picked the friction details on purpose. Every onboarding intake I've ever seen has friction in it. I wanted the output to feel real.

**The doctrine the whole repo is built on: agent enforces structure, human keeps judgment.** The agent drafts and schedules and surfaces patterns. The human decides on the comp number, the term, the rating, the retention call.

If you only read one doc inside the repo, read [`docs/why-this-shape.md`](https://github.com/whoamialt/onboarding-agent/blob/main/docs/why-this-shape.md) — every design choice in the repo, with the reasoning. It's the part that turns the artifact into something you can build your own version of.

---

## How I actually run it

### Model + effort level

I default to **Opus + high effort** for most agent work. Opus is reliably better at reasoning, and "high" gives the model enough room to think through complex tasks. For very simple, mechanical procedures — a time tracker, a file mover, an admin script where the steps are obvious — Sonnet is fine and faster and cheaper.

I scale effort with how much reasoning the work needs: **high** for synthesis and design, **medium** for execution, **max** only when stakes are high or I'm in front of an audience.

**For someone starting out:** Opus + high is a good default. Stay there until you have a reason to step down.

### The three run modes

- **Plan mode** — agent writes a plan, you review, you approve, then it executes. Use when the task is new or ambiguous.
- **Ask permissions** — agent runs but asks before each meaningful action. Use when you trust the shape of the work and just want to stay in the loop.
- **Auto** — agent runs autonomously. Use sparingly, only for procedures you've run many times.

**The flow I usually run:** plan mode while I'm designing the agent (or anything new) → ask permissions for day-to-day execution → auto mode only for the most well-tested procedures.

Plan mode isn't about safety — it's about *calibration.* It forces the agent to articulate what it's about to do before it does it, so you catch wrong assumptions before they become wrong outputs.

### Dispatch — Claude Code on your phone

If you're on Claude Code, install the mobile app — they call it **Dispatch**. It's the thing that has changed how I work the most. Whatever's running on my laptop gets surfaced on my phone, so when an agent stops for a permission check, I see it and can approve, redirect, or pause from anywhere.

It keeps the oversight without keeping me chained to the screen. Honestly a little addictive — I've caught myself approving agent runs from the grocery store. Worth it for any work that uses long-running agents with human checkpoints, which is most of it.

> **The starter recipe:** Opus, high effort, plan mode for the build, ask permissions for the day-to-day, Dispatch on your phone so you're not stuck at the laptop. That's the whole stack for the first month.

---

## Two more questions you asked

**Are these `.md` files Claude-generated, or do I have to add params?**

Both work. You can copy a skill from a public library and use it as-is, but I almost never do that — the institutional knowledge is the whole point. What I do instead is work with Claude directly. I tell it what I want a skill to do, what templates I already use, what tone, what checkpoints I want. Then we build it together. The result is a skill that reflects how I actually work, not how someone else's job worked.

The trap I see: people download every skill they can find. Don't do that. It's like starting a new job and being given every internal doc from every team — you remember none of it and use less of it. Build the skills you'll actually use. Three good ones beat fifty downloaded ones.

**My Pro plan runs out of tokens running one daily agent — am I doing something wrong?**

Probably not, but it depends. How many MCPs is the agent connected to? How big is the context window? How heavy is the task? An agent that pings five tools, reads ten files, and runs a multi-step decision will eat through a Pro plan.

The first thing I'd try is **[Caveman](https://github.com/juliusbrussee/caveman)** — a skill (and a discipline) for compressing prompts and tightening what gets loaded into context. Install it if your context windows are running long. It's the single highest-leverage thing for keeping token usage sane.

Beyond that, Anthropic's plans are roughly Pro at $20/month, the 5x at ~$100, Max at $200, then enterprise. The Max plan isn't unreasonable in a building phase — I'm running Max while I'm actively building and expect that to drop once the heavy build is done. Investing more during the build phase is fine; you'll do less of it in steady state.

---

## Resources, with what each is

### The hero — Andrej Karpathy

**Who he is.** Co-founder of OpenAI. Former director of AI at Tesla. Taught Stanford's CS231n (the deep learning class everyone has watched). Now runs Eureka Labs — an AI-native education company. Posts on X as [@karpathy](https://x.com/karpathy). Blog at [karpathy.ai](https://karpathy.ai).

**Why everyone talks about him.** He's the single most-recommended AI educator on the internet, and the reason is simple: he explains how this stuff actually works in a way that's clear AND deep. Most teachers pick one — clear OR deep. He does both. Watching him is the closest thing to "having a real-world model installed in your head" without doing a CS degree.

**What to watch first.** His **Intro to LLMs** lecture (~1hr on YouTube — search "Karpathy Intro to LLMs"). It will change how you think about everything else in this space. No math required, no programming background needed. By the end you'll understand what a model actually is, why prompts work the way they do, and why some agents fail in ways that will start to feel obvious.

**If you want to go deeper.** His **Zero to Hero** series — eight YouTube videos that build a language model from scratch in Python. Save it for when you want to know the engineering side.

### The course I took and recommend

**[HuggingFace Agents Course](https://huggingface.co/learn/agents-course/en/unit0/introduction)** — the most thorough free course on agents. Goes from first principles up through multi-agent and tool use. I took it because I wanted to make sure my mental models matched what serious researchers in the space were teaching. They mostly did, with a few useful sharpenings. If you want to get serious about building agents, this is where I'd start.

### The podcast I listen to most

**[How I AI](https://www.youtube.com/@howiaipodcast)** — practitioners showing how they actually use AI day to day. Not "AI is changing the world" hype — just how they work. Start with [this episode](https://www.youtube.com/watch?v=LJ1YZ3Uek3g), then browse.

### Skill libraries

- **[Anthropic skills library](https://github.com/anthropics/skills)** — official examples. Read three or four. The pattern clicks fast. The canonical "here's what a well-shaped skill looks like" reference.
- **[Gooseworks skills directory](https://skills.gooseworks.ai/)** — searchable catalog of community-built skills. Browse it like a cookbook. Do that for an afternoon and you'll never need a skill template again.
- **[Karpathy-style skills](https://github.com/forrestchang/andrej-karpathy-skills)** — community-built skills modeled on his teaching style. Useful as a shape reference if you want to encode pedagogical structure into your own skills.
- **[Caveman](https://github.com/juliusbrussee/caveman)** — multi-platform skill manager AND a pattern for compressing prompt context. Install it if your context windows are long, or if you're managing skills across Claude Code, Codex, and ChatGPT.

---

## Who to follow

### On X (the tight list)

- **[@karpathy](https://x.com/karpathy)** — Andrej. Teaches in posts. The single most-followable account in this space.
- **[@simonw](https://x.com/simonw)** — Simon Willison. Builds AI tools daily, blogs every one. Practical, opinionated, prolific.
- **[@emollick](https://x.com/emollick)** — Ethan Mollick, Wharton prof. Best account for AI-in-work framing without engineering depth. His Substack (One Useful Thing) is great too.
- **[@goodside](https://x.com/goodside)** — Riley Goodside. Prompt engineering practitioner. Gets weird with models in instructive ways.
- **[@swyx](https://x.com/swyx)** — Shawn Wang. AI engineering culture. Runs the Latent Space podcast.
- **[@geoffreylitt](https://x.com/geoffreylitt)** — Geoffrey Litt. Small AI tools, end-user programming. Useful if you're thinking "how do non-engineers build with AI."

### On TikTok (honestly thin)

I don't watch much AI content on TikTok — most of the depth lives on YouTube, X, and Substack. If you're a TikTok-first person:

- **[@rowancheung](https://www.tiktok.com/@rowancheung)** — bite-sized AI news, decent for keeping up without reading.

For short bites that aren't TikTok, subscribe to **The Rundown AI** — daily email, fast, opinion-light, easy to skim. Same author as Rowan's TikTok.

### For workshop continuity

- **[Unsupervised](https://sophielemieux.substack.com)** — my Substack. Practitioner notes on building this stuff — agents, skills, where things break.

---

## What to do this week

1. **Pick the most repetitive thing on your plate.** Not the most interesting one. The most repetitive.
2. **Decide what shape it needs.** Chat? Workflow? Agent? Default to workflow. Step up to agent only if it has to adapt.
3. **If it's an agent — clone the repo we built.** Read the README. Run it once with the fake company so you see the structure work. Then start copying the shape onto your real workflow.
4. **Write one skill.** Under 80 lines. Use the existing skills as the shape guide. Tell the agent your *brief definition of done* in the prompt — this is the single coaching tip that has saved me the most rework.
5. **Run it three times on three different inputs.** Tighten until the variance is in the right places — creativity, not procedure.

Don't try to build a system upfront. The system shows up after the third or fourth skill, when patterns start to repeat.

---

## Stuck? Send me what you tried.

Truly. I learn most from where people get stuck. Reply to my email with what you tried and where it broke and I'll write back.

— Sophie · *[Unsupervised on Substack](https://sophielemieux.substack.com)*
