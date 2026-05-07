# Build your first agent — step by step

*Follow this once and you'll have a working agent in about ten minutes. If your screen looks different from what's described — that's fine. The tools change weekly. The shape stays the same.*

> The designed (HTML/PDF) version of this lives at `docs/one-pager.html`. Open it in a browser, then ⌘P → Save as PDF if you want to attach it.

---

## What you're building

An agent is a loop with judgment, tools, and boundaries. You give it a goal and the constraints. It reads the situation, picks the right approach, asks when stuck.

Different from chat (forgets each time). Different from a workflow (can't adapt). If your task is "do these exact steps every time," you want a workflow. If it has to adjust based on the case — different role, different person, different situation — you want an agent.

---

## STEP 01 — Install your tool

Pick one. They do roughly the same thing.

- **[Claude Code](https://www.claude.com/product/claude-code)** (Anthropic) — what I use most. Download from claude.com or run `npm install -g @anthropic-ai/claude-code` in your terminal.
- **[Codex](https://chatgpt.com/codex)** (OpenAI) — same idea on the OpenAI side.
- **[Antigravity](https://antigravity.google/)** (Google) — Google's version. $10/month. Best for tasks involving video or visual content.

Open it from your dock or your browser, depending on what you installed. You'll see a window with a prompt box at the bottom. That's where you type.

---

## STEP 02 — Set three switches before you type

At the top (or in settings, depending on the tool):

1. **Permissions** — start with **Ask Permissions**. The agent checks with you before each action.
2. **Mode** — for "build me an agent" or anything ambiguous, use **Plan Mode**. The agent writes a plan, you approve, then it builds. For simpler tasks, Ask is enough.
3. **Model + effort** — default to **Opus + high**. Stay there until you have a reason to step down.

*Sonnet is fine for very mechanical tasks. Max effort is for when stakes are high. Opus + high is the right starting point for almost everyone.*

---

## STEP 03 — Type your goal

Open with this exact phrasing — it works:

```
> I would like to build an agent. My goal is to build an onboarding agent
  that learns from company information what onboarding requires, and
  manages every part from the initial contract through the 30-day check-in.
```

Specific is better. The more your goal sentence sounds like a sentence you'd say to a new hire, the more useful the agent will be.

---

## STEP 04 — Add your definition of done

Same prompt, right after your goal. Say what "good enough" looks like. This is the single biggest thing that has saved me rework.

```
> My definition of done is an MVP that runs the full onboarding lifecycle
  end-to-end, with the live steps and human checkpoints visible.
```

---

## STEP 05 — Submit. Then answer the agent's questions.

Hit enter. The agent will think for a minute (longer on max effort). Then it usually asks back — *"who's the audience? how real should the actions be? any preference on industry?"*

Answer them. This is where the agent gets specific to your context. Don't skip this — the questions it asks are doing real work.

---

## STEP 06 — Review the plan

The agent shows you a plan before it builds anything. Read it. Two checks:

- Does this match what I asked for?
- Is anything missing or overscoped?

If yes, accept. If no, redirect:

```
> I'd like you to start with X instead.   (or whatever the change is)
```

Then accept once it's right.

---

## STEP 07 — Allow as it works

The agent now builds. It'll ask permission for each meaningful action — *"can I write this file? can I create this folder?"* Click allow.

If it's a task you trust, click **"always allow this in this project"**. Saves a lot of clicks. Don't do this on your first agent — watch a few permission requests so you understand what it's doing.

---

## STEP 08 — Use it. Then iterate.

When the build finishes, your agent lives in a folder on your machine. To use it, run a skill by typing `/skill-name` in the same window.

To improve it: rerun the agent on three different inputs, watch where it gets confused, tighten the skill files. Three runs are enough to see what's working.

---

## STEP 09 (optional) — Save and share

To back it up or share with someone:

```
> Please initialize a git repo in this folder and push to GitHub.
```

The agent will do it. You'll get a URL you can send to anyone.

---

## Once you've built one — the next things worth knowing

**Dispatch — Claude Code on your phone.** If you're on Claude Code, install the mobile app. They call it Dispatch. When the agent stops for a permission check, it surfaces on your phone. Approve, redirect, or pause from anywhere. The thing that has changed how I work the most.

**The flow I run after the first build.** Plan mode while I'm designing something new → Ask Permissions for day-to-day → Auto only for procedures I've run dozens of times.

**If your tokens are running out.** Install **[Caveman](https://github.com/juliusbrussee/caveman)**. A skill (and a discipline) for compressing prompts. The biggest single thing for keeping cost sane on a Pro plan.

**The agent we built today.** [github.com/whoamialt/onboarding-agent](https://github.com/whoamialt/onboarding-agent) — clone it, open in your tool, run `/learn-company lattice-loom marcus-chen`. Five skills, two human checkpoints, no real client info. A teaching artifact you can fork.

---

## To go deeper

- **[Andrej Karpathy](https://x.com/karpathy)** — co-founder of OpenAI, ex-Tesla AI, taught Stanford CS231n. The most-recommended AI educator on the internet. Watch his "Intro to LLMs" lecture (1 hr on YouTube). It will change how you think about everything else.
- **[HuggingFace Agents Course](https://huggingface.co/learn/agents-course/en/unit0/introduction)** — the course I took. Free, self-paced.
- **[How I AI](https://www.youtube.com/@howiaipodcast)** — my favorite podcast. Start with [this episode](https://www.youtube.com/watch?v=LJ1YZ3Uek3g).
- **[Anthropic skills library](https://github.com/anthropics/skills)** · **[Gooseworks directory](https://skills.gooseworks.ai/)** — when you're ready to study what other people have built.

---

## Stuck?

Reply to my email with what you tried and where it broke. I learn most from where people get stuck.

— Sophie · *[Unsupervised on Substack](https://sophielemieux.substack.com)*
