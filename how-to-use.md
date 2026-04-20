# How to Use This Training

You have two options. One is designed for how you actually learn.

---

## The Short Version

**Open each day's markdown file. Copy the "Tutor Prompt" block at the top. Paste it into Claude.** Claude will then walk you through the lesson verbally — like a tutor or an audiobook — quiz you on the key points, and help you apply it to your actual TCE work.

That's it. The files are the curriculum. Claude is the teacher running you through it.

---

## Why Guided Beats Self-Study for You

You've said you learn best verbally — you audiobook a lot, and our voice sessions have landed well. Reading 20 markdown files alone works, but it's the slowest path to actually absorbing this material.

**Guided sessions turn each file into:**
- A live conversation, not a wall of text
- Questions that test whether you actually got it (instead of you *thinking* you got it)
- Direct application to your real skills, your real ExpertOps setup, your real outreach campaigns
- A homework step that writes back to `claude-learnings.md` with Claude's help

One guided hour beats three self-study hours.

---

## The Daily Ritual

### 1. Open the day's file
Start with [Week 1, Monday](./week-1-claude-code/day-1-context-window.md). Each day's "Next up" footer links you to the following day.

Open in VS Code (Ctrl+Shift+V to render it), or just paste the content into Claude.

### 2. Copy the Tutor Prompt block
Every day file has a **Tutor Prompt** section at the top, inside a blockquote. Copy the whole block.

### 3. Paste into Claude
Best options:
- **Claude Code** in your `claude-training/` folder — can read the file directly and update `claude-learnings.md` for you
- **Claude.ai** (web or desktop) — fine if you're not at your dev machine
- **Claude mobile app with voice mode** — if you're on the go and want the audiobook experience, like our original planning session

### 4. Let Claude teach
Claude will:
1. Read the full lesson file
2. Ask what context you need right now (what you've done, any blockers, any recent TCE work that's relevant)
3. Teach the concept conversationally, pausing to check understanding
4. Apply the concept to your real TCE work (ExpertOps, skills, pipelines — whichever is relevant that day)
5. Walk you through the homework step-by-step and help you log results in [claude-learnings.md](./claude-learnings.md)

### 5. Check the box
When you finish a day, open [README.md](./README.md) and tick the checkbox for that day. Satisfying. Visible. Keeps you honest.

---

## The Fallback Reusable Prompt

If a day's specific Tutor Prompt is lost or you want a quick all-purpose version, here's a general-purpose one:

> You are my training tutor for the Claude training program at `claude-training/`. Today I'm on **Week [N], Day [N]: [topic]**. Read that day's markdown file first. I learn best verbally — treat this like an audiobook tutoring session, not a lecture.
>
> Before we start, ask me: what context do you need right now (what I've done, what's blocking me, what recent TCE work is relevant)?
>
> Then:
> 1. Teach the concept conversationally, pausing to check understanding.
> 2. Help me apply it to my real TCE work (ExpertOps, skills, pipelines, outreach — whatever's relevant).
> 3. Walk me through the homework and help me log the result in `claude-training/claude-learnings.md`.

The per-day Tutor Prompts are tighter and more specific — use those when you can.

---

## Tips for a Good Session

### Do
- Pick a consistent time slot (the "one hour a day" your CIO recommended). Same time, same place, keep it sacred.
- Actually do the homework. A day without the homework is a day half-done.
- Push back on Claude if something doesn't click. "Wait, say that differently" is a legitimate tutor request.
- If you fall behind, don't skip — compress. Two days in one session is fine. Zero is not.
- Use voice mode when you can. You said yourself that's when the learning lands.

### Don't
- Don't let the session drift into general TCE work. Training is training. If something operational comes up, note it in [claude-learnings.md](./claude-learnings.md) and come back to it after.
- Don't skip the homework "because I get it." You don't yet. That's the point of the homework.
- Don't batch multiple days thinking you'll catch up later. Catch up next session if you missed one. Batching over-stuffs context (see Week 1 Monday).

---

## When You Fall Behind

You will. Everyone does. Here's the rule:

- **1–2 days behind:** next session, do two days back-to-back. Fine.
- **A full week behind:** pause, finish the missing week in a couple of focused sessions, then continue.
- **More than a week behind:** stop resetting the goal. Pick up where you'd be *today* and treat the skipped material as a backlog item for next month's first-Friday audit.

The month is front-loading. Missing a day isn't failure. Abandoning the rhythm is.

---

## When You Finish a Week

Each Friday's file ends with a "Where you are" summary. Take two minutes to read it. It reinforces the week's connective tissue.

Friday of Week 4 is the retrospective. Take that one seriously — it cements what carried over into your actual operating style.

---

## After the Training

[README.md](./README.md) has the continuous-learning rhythm. Daily use, weekly Discord, monthly first-Friday audit, quarterly skill revision. Stay in it.

[claude-learnings.md](./claude-learnings.md) is your permanent working log. Don't stop adding to it when training ends. That's where the compounding happens.

---

Start here: [Week 1, Monday — The Context Window Constraint](./week-1-claude-code/day-1-context-window.md)
