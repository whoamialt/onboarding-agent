# Build your first agent. Step by step.

*Follow this once and you'll have a working agent in about ten minutes. If your screen looks different from what I describe, that's fine. The tools change weekly. The shape stays the same.*

> The designed (HTML/PDF) version of this lives at `docs/one-pager.html`. Open it in a browser, then ⌘P → Save as PDF if you want to attach it.

---

## What you're building

An agent is a loop with judgment, tools, and boundaries. You give it a goal and the constraints. It reads the situation, picks an approach, asks when it's stuck.

That's different from chat, which forgets you between conversations. And different from a workflow, which runs the same steps no matter what. If your task is "do these exact steps every time," build a workflow. If the work has to read the case before it acts, that's where an agent earns its keep. Onboarding a senior IC is different from onboarding an intern. Sourcing for a fractional exec is different from sourcing for an associate. That's agent territory.

---

## Step 01. Install your tool

Pick one. They do roughly the same thing.

- **[Claude Code](https://www.claude.com/product/claude-code)** (Anthropic). What I use most. Download from claude.com or run `npm install -g @anthropic-ai/claude-code` in your terminal.
- **[Codex](https://chatgpt.com/codex)** (OpenAI). The OpenAI version.
- **[Antigravity](https://antigravity.google/)** (Google). $10 a month. Best for tasks involving video or visual content.

Open it from your dock or your browser, depending on what you installed. You'll see a window with a prompt box at the bottom. That's where you type.

---

## Step 02. Set three switches before you type

At the top (or in settings, depending on the tool):

1. **Permissions.** Start with Ask Permissions. The agent checks with you before each action.
2. **Mode.** For "build me an agent" or anything ambiguous, use Plan Mode. The agent writes a plan, you approve, then it builds. For simpler tasks, Ask is enough.
3. **Model + effort.** Default to Opus + high. Stay there until you have a reason to step down.

Sonnet is fine for mechanical tasks. Max effort is for when stakes are high. Opus + high is where I'd start.

---

## Step 03. Type your goal

Open with this phrasing. Works for me every time.

```
> I would like to build an agent. My goal is to build an onboarding agent
  that learns from company information what onboarding requires, and
  manages every part from the initial contract through the 30-day check-in.
```

Specific is better. The more your goal sentence sounds like one you'd say to a new hire, the more useful the agent will be.

---

## Step 04. Add your definition of done

Same prompt, right after your goal. Say what "good enough" looks like. The thing that has saved me the most rework.

```
> My definition of done is an MVP that runs the full onboarding lifecycle
  end-to-end, with the live steps and human checkpoints visible.
```

---

## Step 05. Submit. Then answer the agent's questions.

Hit enter. The agent will think for a minute (longer on max effort). Then it usually asks back: *"who's the audience? how real should the actions be? any preference on industry?"*

Answer them. This is where the agent gets specific to your context. Don't skip this. The questions it asks are doing real work.

---

## Step 06. Review the plan

The agent shows you a plan before building anything. Read it. Two checks:

- Does it match what you asked for?
- Is anything missing or overscoped?

If yes, accept. If no, redirect:

```
> I'd like you to start with X instead.   (or whatever the change is)
```

Then accept once it's right.

---

## Step 07. Allow as it works

The agent now builds. It'll ask permission for each meaningful action: *"can I write this file? can I create this folder?"* Click allow.

If it's a task you trust, click "always allow this in this project" to save clicks. Don't do this on your first agent. Watch a few permission requests so you understand what it's doing.

---

## Step 08. Use it. Then iterate.

When the build finishes, your agent lives in a folder on your machine. To use it, type `/skill-name` in the same window.

To improve it: rerun the agent on three different inputs, watch where it gets confused, tighten the skill files. Three runs is enough to see what's working.

---

## Step 09. (optional) Save and share

To back it up or share with someone:

```
> Please initialize a git repo in this folder and push to GitHub.
```

The agent will do it. You'll get a URL you can send to anyone.

---

## Once you've built one

A few things worth knowing once you're past the first build.

If you're on Claude Code, install the mobile app. They call it Dispatch. When the agent pauses for a permission check, it surfaces on your phone, so you can approve from anywhere. It's the tool change that has affected my workflow the most.

After the first build, my flow is plan mode for designing something new, ask permissions for day-to-day, auto only for procedures I've run dozens of times.

If your tokens are running out, install [Caveman](https://github.com/juliusbrussee/caveman). It's a skill (and a discipline) for compressing prompts. The biggest token saver I've used.

The agent we built together is at [github.com/whoamialt/onboarding-agent](https://github.com/whoamialt/onboarding-agent). Clone it, open in your tool, type `/learn-company lattice-loom marcus-chen`. Five skills, two human checkpoints, no real client info. A teaching artifact you can fork.

---

## To go deeper

- **[Andrej Karpathy](https://x.com/karpathy)**. Co-founder of OpenAI, ex-Tesla AI, taught Stanford CS231n. The most-recommended AI educator on the internet. Watch his "Intro to LLMs" lecture (1 hr on YouTube). It will change how you think about everything else.
- **[HuggingFace Agents Course](https://huggingface.co/learn/agents-course/en/unit0/introduction)**. The course I took. Free, self-paced.
- **[How I AI](https://www.youtube.com/@howiaipodcast)**. My favorite podcast. Start with [this episode](https://www.youtube.com/watch?v=LJ1YZ3Uek3g).
- **[Anthropic skills library](https://github.com/anthropics/skills)** and **[Gooseworks directory](https://skills.gooseworks.ai/)**. Worth a browse when you want to see what other people have built.

---

## What's going on?

If something's not working, reply to my email. Tell me what you tried and where it broke. I learn most from where people get stuck.

Sophie. [Unsupervised on Substack](https://sophielemieux.substack.com).
