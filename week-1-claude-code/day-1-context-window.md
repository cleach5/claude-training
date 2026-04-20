# Week 1, Monday — The Context Window Constraint

**Time:** ~1 hour
**Goal:** Understand the single constraint that explains every other best practice this month.
**Primary source:** [Claude Code Best Practices — Context Window Management](https://code.claude.com/docs/en/best-practices)

---

## Tutor Prompt — Paste This Into Claude to Start

> You are my training tutor for **Week 1, Day 1: The Context Window Constraint**. I learn best verbally — treat this like an audiobook/tutoring session, not a lecture.
>
> First, read this full lesson file: `claude-training/week-1-claude-code/day-1-context-window.md`. Then ask me what context you need right now — any TCE work I'm in the middle of, any prior familiarity with context windows, any blockers — before diving in.
>
> Then:
> 1. Teach me the concept of the context window conversationally. Pause often to check understanding with questions like "does that land?" or "can you explain that back to me?" Don't rush.
> 2. Help me apply it by having me pick **one project I'm actively working on** (ExpertOps, zerobounce-pipeline, instantly-csv-processor, or tce-website) and asking: where am I currently asking Claude to do too much in one conversation? Where would the natural splits be?
> 3. Walk me through the homework and help me log my answer in `claude-training/claude-learnings.md` with today's date.
>
> By the end, I should be able to answer: "If I'm refactoring, debugging, and optimizing — should that be one session or three? Why?"

---

## The Big Idea

Claude Code reads your files, runs commands, and makes changes while holding everything in memory at once. That memory has a hard ceiling — the **context window**. Think of it as a whiteboard: you can write a lot, but once it's full, you can't add more without erasing something. And here's the catch — as it fills up, Claude gets worse at remembering what's at the top. It's not a cliff; it's a slope.

Every best practice you'll learn this month exists because engineers figured out how to **work within this constraint instead of fighting it.**

---

## What Lives in Your Context Window

Everything:

- Every message you've sent Claude
- Every file Claude has read
- Every command output
- Every response Claude gave you

All of it stays in memory for the whole conversation. So if you ask Claude to read your entire tce-website codebase, then debug a bug, then refactor a component, then review the refactor — by the end, your context is packed.

---

## The Degradation Curve

This is important. Context doesn't just stop working at the limit — it degrades **gradually**:

- **~50% full:** Claude is still sharp.
- **~75% full:** small mistakes creep in — missed details, repeated suggestions.
- **~90% full:** attention is scattered; Claude forgets a key instruction from 30 messages ago.

Claude Opus 4.7 has a 200,000-token context window. Sounds like a lot until you're actually using Claude Code. A single debugging session can easily burn 30,000–50,000 tokens.

---

## The Three Characteristics That Matter

1. **Finite** — there is a hard ceiling.
2. **Degrades** — more information actively hurts performance as it builds up; it's not neutral.
3. **Shared** — your instructions, the files Claude reads, and its responses all compete for the same tokens.

---

## Real Consequence for TCE

Your brief decoder needs to read past project files, understand client context, cross-reference OneDrive — that's context-heavy work. If you tried to do all of that **plus** generate outreach copy **plus** validate expert matches in one session, by the time you're generating copy Claude has lost half the context about what makes a good match for this specific client.

That's why splitting into separate focused sessions — research, then matching, then outreach — actually produces **better output, faster.**

---

## What "Refactoring" Means (in case the word trips you up)

Refactoring = cleaning up code without changing what it does. Rearranging furniture, not redecorating the room. Same output, better organized, easier to change later. Refactoring is context-heavy because Claude has to understand current code, plan a new structure, and rewrite it — so you never combine refactoring with debugging or new-feature work in the same session.

---

## The Workflow Shift

Most people use Claude Code like a chatbot — one long conversation, asking questions, building incrementally. That works for simple stuff. For complex projects (your website refactor, pipeline work, ExpertOps features) it fills context fast and produces mediocre output by the end.

**Operators who get the most out of Claude Code** structure work so each session has:
- a clear purpose
- a limited scope
- a defined endpoint

Then they start fresh.

**Instead of:** "Help me understand my codebase, then build this feature, then debug it."
**Do:** Session 1 — understand and document. Session 2 — build. Session 3 — debug with fresh eyes.

---

## Homework

Pick one project you're actively working on — `zerobounce-pipeline`, `ExpertOps`, or `instantly-csv-processor`. Ask yourself:

> "Where am I currently asking Claude to do too much in one conversation? If I split this into separate focused sessions, where would the breaks naturally happen?"

Write the answer in [claude-learnings.md](../claude-learnings.md). Don't implement anything yet — this is awareness, not action.

---

## What You Should Be Able to Answer by End of Day

- What's in my context window? → Everything. Messages, files, outputs, responses.
- Why does it matter? → It fills up and Claude gets worse as it does.
- What's the solution? → Structure work so each session has clear boundaries. Save state between sessions.
- If I need to refactor a component, debug an issue, and optimize performance — should that be one session or three? Why?
  - Three. Research/planning in one. Execution in another. Review in a third. Each stays focused. Each stays sharp.

---

**Next up:** [Tuesday — CLAUDE.md Files and Persistent Memory](./day-2-claude-md.md)
