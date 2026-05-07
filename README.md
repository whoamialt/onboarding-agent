# Onboarding Agent — Workshop Companion

> *A live-build artifact from the First Agent Workshop. Cloning this repo is the closest thing to attending the session.*

This is the agent we built together in the room. It's also the artifact I want you to read alongside the recording — every file in this repo was either written live, referenced in the curriculum, or added afterward to capture something I should have had time to say.

If you came here from the workshop email: hi, you're in the right place. Start with [Where to start](#where-to-start) at the bottom.

If you didn't attend and you're trying to learn agent-building from scratch: also right place. The repo is designed to be self-contained.

---

## About the session

**The session was 60 minutes.** No slides, no pre-work, no installs. Conversational definition curriculum + a live build on screen. Audience was non-technical People Ops practitioners — talent partners, HRBPs, recruiters, founders' first HR hires.

**The premise we worked from:**

> If you do something more than once a day, turn it into a command.

Not "is this AI-shaped?" Not "does this need automation?" Just: am I doing this repeatedly, and is the thinking consistent enough that I could write it down?

If yes, write it down. The "writing it down" part is the agent.

---

## What we covered in the live build

Loosely in the order it happened:

1. **What an agent actually is** — a loop with judgment, tools, and boundaries. We anchored every later concept against this.

2. **The three levels** — global rules → project rules → skills. Different runtimes call them different things, but the mental model is the same across Claude Code, Codex, Antigravity, ChatGPT.

3. **The agent loop in one paragraph** — context → decide → act → observe → repeat. Everything else (RAG, MCP, multi-agent, plan mode) is plumbing for that loop.

4. **Skill anatomy** — what makes a skill different from a prompt or a doc. The description as the trigger condition. The body as procedure. Optional `scripts/`, `references/`, `assets/` folders. Progressive disclosure — why skills don't burn your context window even when you have fifty of them.

5. **Skill vs MCP vs RAG vs fine-tuning** — the four-way comparison nobody draws clearly. Skills give procedure. MCP gives tools. RAG gives facts. Fine-tuning bakes things into model weights. They compose, they're not interchangeable.

6. **The live build** — we took the onboarding workflow (a thing every founder I work with does, often badly) and built the agent in this repo, end-to-end. Five skills, two human-judgment checkpoints, zero code. Pure markdown.

7. **The doctrine** — *agent enforces structure, human keeps judgment.* The single most important sentence in the room. It's the principle that decides where to put checkpoints and where to let the agent run.

8. **Skill folder strategy** — at scale, you don't want fifty singular skills. You want one skill folder with sub-skills as references. Free-tier Claude caps you around 50 skills; cognitive load caps you sooner. Folder strategy gets around both.

9. **Plan mode** — and why I make people use it for the first month. Calibration, not safety.

10. **Definition of done for an agent** — brief done definition · custom pipelines · visible reasoning · consistency across runs.

The full curriculum is written up in **[docs/agent-primer.md](docs/agent-primer.md)**. If something I said in the room conflicts with what's there, the page version is the one I stand behind — I sometimes phrase things tighter on the page than in the moment.

---

## What we didn't cover (and why)

**The orchestration layer.** We got you to the point where you can build an agent and a skill that work *in isolation*. That's the foundation, and it's the part most workshops never even get to.

The part most founders skip — and the part where production deployments fall apart — is orchestration: multiple agents handing off context cleanly, state management across steps, retries that don't loop. No workshop fixes that without real shipping behind it. Worth knowing it exists. We'll cover it separately if there's interest.

---

## What's in this repo

```
onboarding-agent/
├── CLAUDE.md                Agent identity (Claude Code reads this)
├── AGENTS.md                Mirror of CLAUDE.md (Codex / Antigravity read this)
├── README.md                You are here
├── LICENSE                  MIT
├── .claude/commands/        Five skills (slash commands)
│   ├── learn-company.md
│   ├── send-contract.md
│   ├── preboard.md
│   ├── first-day.md
│   └── thirty-day.md
├── companies/
│   └── lattice-loom/        The fictional company
│       ├── profile.md
│       ├── handbook.md
│       ├── onboarding-template.md
│       └── hires/
│           └── marcus-chen/ The fictional new hire
│               └── intake.md
├── templates/               Boilerplate offer letter, welcome email, etc.
├── reference/
│   └── onboarding-principles.md     The doctrine
└── docs/
    ├── agent-primer.md      The workshop curriculum, written up
    ├── why-this-shape.md    Every design decision, with the why
    ├── one-pager.md         The single-page summary
    └── recap-email.md       The email draft
```

Lattice Loom and everyone in it is fictional. Any resemblance to a real company is coincidental.

---

## The agent itself

A built-from-scratch onboarding agent that learns from a (fictional) Series A B2B SaaS company's information what onboarding requires for a specific hire, then runs the lifecycle from contract draft through 30-day check-in.

**The agent does:** drafts, schedules, coordinates, surfaces patterns, maintains structure across hires.

**The agent does not:** decide compensation, terms, performance ratings, or retention actions. Those stay with humans, by design.

### The five skills

| Skill | What it does | Stops for human? |
|---|---|---|
| `/learn-company [company] [hire]` | Reads the company files + hire intake, writes a tailored 30-60-90 plan | No |
| `/send-contract [hire]` | Drafts an offer letter from intake + handbook | **Yes** — explicit y/n before mock-send |
| `/preboard [hire]` | Day -7 → Day 0 task list with owners (HR / IT / Manager / Agent) | Yes — employee-facing drafts need approval |
| `/first-day [hire]` | Day 0 morning Slack post + Week 1 calendar + manager handoff brief | Yes — same |
| `/thirty-day [hire]` | 30-day check-in email + internal retention indicators | No, but two-section file with hard separator |

Two human-judgment checkpoints are mandatory:
1. Before any contract mock-send (`/send-contract`)
2. Before any employee-facing draft goes out

This is the *agent enforces structure, human keeps judgment* doctrine made concrete.

### The fictional company

**Lattice Loom** — Boston-based B2B SaaS, Series A, 35 people, building workforce planning software for healthcare staffing agencies. Hybrid (T/W/Th in office). Platform engineering team carries on-call. HIPAA training required for most roles. Existing onboarding is a thin 12-bullet Notion doc — realistic for a company that just crossed 30 employees.

### The fictional new hire

**Marcus Chen** — Senior Backend Engineer, Platform team, reports to Diane Park (VP Eng). Local to Cambridge. New parent. HIPAA-naïve. Joined from Recurly via acqui-hire into Stripe.

The detail is on purpose. I added the new-parent flag and the HIPAA-naïve flag specifically to test whether the agent surfaces personal context into the plan and whether it tailors training pacing to the role. Generic intakes produce generic plans. The friction in the data is what makes the demo land.

---

## Run it on the platform you have

This agent is a folder of markdown files. Platform-specific glue is small. Pick yours:

### Claude Code

```bash
git clone https://github.com/whoamialt/onboarding-agent.git
cd onboarding-agent
# Open in Claude Code. Slash commands auto-load from .claude/commands/.
```

Run: `/learn-company lattice-loom marcus-chen`

### OpenAI Codex (or any agent that reads `AGENTS.md`)

```bash
git clone https://github.com/whoamialt/onboarding-agent.git
cd onboarding-agent
# Open in Codex. Codex reads AGENTS.md automatically.
```

Invoke a skill by name: *"run learn-company on lattice-loom marcus-chen."* Codex follows the procedure in `.claude/commands/learn-company.md`.

### Google Antigravity

Same as Codex. Antigravity reads `AGENTS.md` and the markdown files. Invocation pattern is the same.

### Anywhere else (ChatGPT projects, Cursor, Cline, generic LLMs)

The skills are plain markdown procedures. Paste any skill file's content into a chat and ask the model to follow it. The agent works without any tooling — it's just structured prose. Tooling makes it ergonomic, not possible.

---

## Demo it in 6–14 minutes

The 7-beat demo flow (full version is 14 min; 6-min cut drops beats 4 and 5):

1. **Setup** (1m) — show `profile.md`, `handbook.md`, `intake.md`. *"Here's what the agent knows."*
2. **`/learn-company lattice-loom marcus-chen`** (3m) — agent generates `plan.md`. Narrate three things it specifically picked up (hybrid Boston, on-call by Day 60, HIPAA-naïve ramp).
3. **`/send-contract marcus-chen`** (2m) — agent drafts, **stops**, asks y/n. *"Agent enforces structure. I keep judgment."*
4. **`/preboard marcus-chen`** (3m) — agent generates owner-tagged task list. *"Half of these aren't the agent."*
5. **`/first-day marcus-chen`** (2m) — agent generates Slack post + Week 1 calendar + manager brief. *"The manager brief is the load-bearing one."*
6. **`/thirty-day marcus-chen`** (2m) — two-section file, one for the hire, one internal. *"Patterns surface. Decisions stay with humans."*
7. **Close** (1m) — *"An agent is a loop with judgment, tools, and boundaries."*

A FigJam visualization of the flow lives [here](https://www.figma.com/board/Z4LKLR2oGhDpWVzbmceYKY).

### Reset between demos

```bash
cd companies/lattice-loom/hires/marcus-chen
ls | grep -v '^intake.md$' | xargs rm
```

The intake stays. Everything else regenerates.

---

## How to extend it

### Add a new hire to Lattice Loom

```bash
mkdir -p companies/lattice-loom/hires/[new-hire-slug]
cp companies/lattice-loom/hires/marcus-chen/intake.md \
   companies/lattice-loom/hires/[new-hire-slug]/intake.md
# Edit the intake. Then run the five skills.
```

### Add a new company

```bash
mkdir -p companies/[new-company]/hires
# Author profile.md, handbook.md, onboarding-template.md
# following the lattice-loom shape.
```

The skills are company-agnostic. They derive the company from the hire's path.

### Add a new skill

Drop a markdown file into `.claude/commands/`. Use the existing skills as a shape guide: trigger description on line 1, then **Step 1 — Read**, **Step 2 — [Verb]**, **Step 3 — Write**, **Step 4 — [Mock-send / human checkpoint]**.

---

## Where to start

If you came from the workshop:

1. **Read [docs/one-pager.md](docs/one-pager.md)** — five-minute refresh.
2. **Run the agent** — clone, open in your runtime, run `/learn-company lattice-loom marcus-chen`. See the structure work.
3. **Read [docs/why-this-shape.md](docs/why-this-shape.md)** — every design decision in this repo, with the why. Use it when you build your own.
4. **Pick the workflow you do most** — not the most interesting one, the most repetitive — and write a 30-line `CLAUDE.md` or `AGENTS.md` for it.
5. **Write one skill.** Under 80 lines. Use the existing skills as shape reference.
6. **Run it three times** on three different inputs. Tighten until the variance is in the right places (creativity) and not the wrong ones (procedure).

If you're stuck, send me what you tried and where it broke. I learn most from where people get stuck.

---

## Teaching artifacts

- **[docs/agent-primer.md](docs/agent-primer.md)** — the full workshop curriculum, written up
- **[docs/why-this-shape.md](docs/why-this-shape.md)** — every design choice in this repo, with reasoning
- **[docs/one-pager.md](docs/one-pager.md)** — single-page summary
- **[docs/recap-email.md](docs/recap-email.md)** — the email that brought you here

## Resources

- [Anthropic skills library](https://github.com/anthropics/skills) — official examples
- [Gooseworks skills directory](https://skills.gooseworks.ai/) — community catalog
- [Karpathy-style skills](https://github.com/forrestchang/andrej-karpathy-skills) — pedagogical shape reference
- [Caveman](https://github.com/juliusbrussee/caveman) — multi-platform skill management

---

## License

MIT. Use it, fork it, rebuild it for your own context. Attribution appreciated.

## Built by

Sophie Lemieux — [sophielemieux.substack.com](https://sophielemieux.substack.com) — *Unsupervised*
