# Week 1, Thursday — Parallel Sessions and Sub-Agents

**Time:** ~1 hour
**Goal:** Understand how to multiply Claude Code output by running work in parallel.
**Primary source:** [Claude Code Best Practices — Parallel Sessions & Agents](https://code.claude.com/docs/en/best-practices)

---

## Tutor Prompt — Paste This Into Claude to Start

> You are my training tutor for **Week 1, Day 4: Parallel Sessions and Sub-Agents**. I learn best verbally — treat this like a tutoring session, not a lecture.
>
> First, read this full lesson file: `claude-training/week-1-claude-code/day-4-parallel-sessions.md`. Then ask me: what's the biggest chunk of Claude Code work I have coming up in the next month? Is it actually carve-able, or are the pieces too dependent on each other?
>
> Then:
> 1. Teach me how parallel sessions and sub-agents work conversationally — git worktrees, lead agent, shared status file. Check understanding often. This concept is abstract and easy to think you've got when you haven't.
> 2. Have me pick my most realistic candidate for parallel work (likely an ExpertOps sprint with capacity + matching + audit streams, or the zerobounce-pipeline integration).
> 3. For that work, walk me through **designing a 3-sub-agent setup**: which stream each sub-agent owns, what the lead agent coordinates, what goes in the shared status file, where the collision risks are.
> 4. Have me write the design in `claude-training/claude-learnings.md`.
> 5. Close with an honest check: is this actually worth parallelizing, or is it small enough that serial is fine? Both answers are valid.

---

## The Big Idea

You don't have to do everything serially. Claude Code lets you **spin up multiple sessions working on different parts of the same project simultaneously**, with a **lead agent** coordinating them.

- One Claude does Research
- Another does Execution
- A third does Review

All at the same time, on the same project.

This is where Claude Code goes from "efficient" to "multiplied."

---

## How It Works Technically — Git Worktrees

A **git worktree** is an isolated checkout of a branch from the same repo. Instead of one branch with one Claude Code session, you create multiple worktrees:

- `worktree-research/` — Claude instance 1 works here
- `worktree-execute/` — Claude instance 2 works here
- `worktree-review/` — Claude instance 3 works here

They're **isolated**, so there's no collision. No merge conflicts mid-work. No stepping on each other's code.

```bash
git worktree add worktree-capacity feature/capacity-tracking
git worktree add worktree-matching feature/matching
git worktree add worktree-audit feature/audit-trail
```

Each worktree gets its own Claude Code session.

---

## Sub-Agents and the Lead Agent

A **sub-agent** is a Claude Code instance that runs independently but reports to a **lead agent**. The lead agent:
- Holds the master plan
- Knows what each sub-agent is doing
- Prevents collisions
- Reviews and integrates pieces when they finish

Think of the lead agent as a project manager for your Claude instances.

---

## Concrete Example — ExpertOps Rebuild

You want to rebuild three parts of ExpertOps: the **capacity model**, the **matching algorithm**, and the **audit trail**.

**Serial approach:** ~3 weeks of work.

**Parallel approach:**
- Lead agent plans the overall architecture
- Sub-agent 1 researches + builds capacity (worktree-capacity)
- Sub-agent 2 researches + builds matching (worktree-matching)
- Sub-agent 3 researches + builds audit (worktree-audit)
- All three run in parallel
- Two days later, lead agent reviews, integrates, you ship

**~1 week instead of 3.**

---

## The Coordination Layer — Shared Status File

Since sub-agents don't share context, they communicate through a **shared status file**, usually `parallel-work-status.md`:

```markdown
# Parallel Work — Sprint of 2026-04-21

## Sub-agent 1: Capacity
- [x] Researched current capacity flow
- [ ] Building capacity_history table (in progress)
- Blocker: need decision on retention policy

## Sub-agent 2: Matching
- [x] Researched matching algorithm
- [x] Plan approved
- [ ] Executing — 60% done

## Sub-agent 3: Audit
- [x] Researched existing audit patterns
- [ ] Schema change blocked on sub-agent 1 (experts table)
```

The lead agent reads this file, coordinates, unblocks collisions. Lightweight but effective.

---

## When Things Conflict

Sub-agent 1 needs to change the `experts` table schema. Sub-agent 2 also needs to change `experts`.

The lead agent sees the conflict in the status file, **redirects one of them** to a different piece first, or coordinates the schema change so both can use the updated version.

**This is why the lead agent exists.** Without it, sub-agents collide.

---

## Context Window Benefit (Yes, This Again)

Each sub-agent has a **fresh context window**. Sub-agent 1 isn't carrying baggage from what sub-agents 2 and 3 did. It stays sharp. Quality stays high **because context never bloats on any single instance**.

---

## For Your Work

### Good candidates for parallel
- ExpertOps schema redesign (capacity / matching / audit as separate streams)
- zerobounce-pipeline integration (API research / CSV processor / results aggregator in parallel)
- tce-website refactor across many components (once it's stable with Ryan)

### Bad candidates for parallel
- Small bug fixes (coordination overhead exceeds benefit)
- Exploratory work where you don't know the pieces yet (research first, then parallelize)
- Anything under a day of serial work

**Rule of thumb:** Parallelize when you have **a week or more** of carve-able, independent work. Otherwise serial is fine.

---

## Homework

Think about your ExpertOps work for the next month:

1. What are **three things** you'd want Claude Code to tackle?
2. Could they run in parallel, or do they have dependencies?
3. If they could run in parallel, where would you need a lead agent to coordinate?

**Map out what a three-sub-agent setup would look like for your next sprint.**

Don't build it yet. Just sketch it. Write in [claude-learnings.md](../claude-learnings.md).

---

## What You Should Be Able to Answer by End of Day

- What's a git worktree? → An isolated branch checkout so multiple Claude sessions don't collide.
- Why does the lead agent exist? → To hold the master plan, prevent sub-agent conflicts, and integrate pieces.
- When is parallel worth it? → When work is >1 week and carve-able into independent pieces.
- How do sub-agents communicate? → Through a shared status file the lead agent coordinates with.

---

**Next up:** [Friday — Failure Patterns to Avoid](./day-5-failure-patterns.md)
