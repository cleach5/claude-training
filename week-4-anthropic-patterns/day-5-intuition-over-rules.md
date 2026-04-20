# Week 4, Friday — The Full Picture and Building Intuition Over Rules

**Time:** ~1 hour
**Goal:** Connect everything. Transition from following the checklist to developing the intuition.
**Primary source:** How Anthropic Teams Use Claude Code (PDF) + four weeks of your own notes

---

## Tutor Prompt — Paste This Into Claude to Start

> You are my training tutor for **Week 4, Day 5: The Full Picture and Building Intuition — the capstone**. I learn best verbally — treat this like a closing conversation, not a lecture. This is the last day of the program.
>
> First, read this full lesson file: `claude-training/week-4-anthropic-patterns/day-5-intuition-over-rules.md`. Also read the full `claude-training/claude-learnings.md` so you have context on what I actually did across the four weeks.
>
> Then:
> 1. Walk me through "the full picture" diagram from the lesson — the one connecting context, persistence, structure, scale, protection, and team sharing. Pause to check if it clicks.
> 2. Teach me the difference between following rules and developing intuition. What are the signs I'm starting to have it? Quiz me.
> 3. Help me write the **retrospective** in `claude-training/claude-learnings.md`:
>    - The 3 practices that had the biggest impact on my actual work
>    - The single highest-priority backlog item — something I commit to implementing next week
>    - What I'd still like to get better at
> 4. Confirm my **post-training rhythm**: daily use, weekly Discord scroll, monthly first-Friday audit, quarterly skill revision.
> 5. Help me draft a short message to my CIO — the recommendation was right, here's what it unlocked, thank you.
> 6. Close by naming the shift: I didn't just learn about Claude Code. I shifted from dabbling to operating.

---

## Where You Are

Four weeks in. You understand:

**Week 1 — Claude Code Fundamentals**
- Context is the constraint. Everything else flows from it.
- CLAUDE.md gives Claude persistent memory without burning context.
- Research → Plan → Execute → Review → Ship keeps sessions focused.
- Parallel sessions + git worktrees multiply throughput.
- Eight failure patterns, all of which you can now recognize.

**Week 2 — Skills**
- Three-tier architecture: SKILL.md focused, references on demand, validation gates.
- Audited your four skills and found the tightening opportunities.
- Defined measurable success criteria.
- Built validation gates.
- Proved improvement against baseline with the three-run test.

**Week 3 — Prompting**
- XML tags for structural clarity.
- Data at the top for long inputs.
- Grounding in quotes to kill hallucination.
- Role framing to change Claude's register.
- Explicit voice with anti-patterns to kill AI slop.

**Week 4 — Enterprise Patterns**
- MCP over CLI for sensitive data.
- CLAUDE.md as live data catalog.
- Team session sharing to propagate patterns.
- Bulk skills and slash commands as institutional leverage.

---

## The Full Picture

These aren't five separate things. They're **one system:**

```
                           CONTEXT IS FINITE
                                  │
        ┌─────────────────────────┼─────────────────────────┐
        │                         │                         │
     PERSIST                   STRUCTURE                  SCALE
        │                         │                         │
  ┌─────┴─────┐             ┌─────┴─────┐             ┌─────┴─────┐
  │           │             │           │             │           │
 CLAUDE.md  Refs/       Research→Ship  Skills     Parallel      Bulk
 (project)  (skills)      workflow     (3-tier)  (worktrees)  (operations)
                             │            │
                             │            └── role, voice, grounding, tags
                             │
                             └── review gate catches drift

Shared across the team via: demo sessions, slash commands, hooks, playbook
Protected from leakage via: MCP servers for anything sensitive
```

Every practice exists because **context is finite and degrades**. Every practice either:
- Saves context (CLAUDE.md, references, MCP)
- Structures it (workflow, XML tags, data-first)
- Multiplies it (parallel sessions, bulk skills)
- Protects it (validation, review, voice guides)
- Scales it (team sessions, slash commands, playbook)

---

## Intuition Over Rules

Over time you'll develop feel:
- You'll know when to be specific with Claude and when to leave room for exploration
- You'll sense when context is getting full and split the session before quality drops
- You'll know when a skill needs refactoring vs. when it just needs a prompt tweak
- You'll know when an operation is worth bulk and when it's not

Your gut will tell you "this context window is full, time to save state and start fresh." You won't need the checklist.

**That intuition comes from running Claude Code deliberately, measuring what works, and iterating.**

---

## The "Deliberate Practice" Loop

1. **Do the work.** Use Claude Code every day. Real work, not toy exercises.
2. **Notice friction.** Every time something feels wrong, pay attention.
3. **Name the pattern.** "I'm hitting failure pattern #3."
4. **Try the fix.** Apply the relevant practice.
5. **Log the result.** In [claude-learnings.md](../claude-learnings.md). Dated. Specific.
6. **Revisit monthly.** First Friday of the month, read through. Pick one backlog item. Implement.

---

## Post-Training Rhythm (Starting Next Week)

### Daily
- Use Claude Code on real TCE work. Notice what works and what breaks.
- Drop observations in [claude-learnings.md](../claude-learnings.md) as they come up.

### Weekly
- 30 minutes in the Anthropic Discord. Scroll for patterns others are hitting.
- One team session (Wednesday 4-MON pattern) — demo or watch.

### Monthly (first Friday)
- One hour reading new Anthropic material.
- One hour auditing your own workflows.
- Pick **one** backlog item from [claude-learnings.md](../claude-learnings.md). Implement it.

### Quarterly
- Deep revision pass on one skill. Full three-run baseline test. Update voice guide.
- Review the playbook. Add/remove entries.

---

## What Separates "Dabbles" From "Operates"

Someone who dabbles with Claude:
- Uses it as a chatbot
- Has one long conversation per task
- Doesn't structure prompts
- Has no repeatable workflows

Someone who operates Claude like a system:
- Treats context as the primary resource
- Structures every non-trivial task into stages
- Has persistent project memory via CLAUDE.md
- Protects sensitive data via MCP
- Multiplies throughput via parallel sessions and bulk skills
- Validates output before shipping it
- Shares patterns across the team
- Iterates on skills with measurable baselines

**You're operating now.** That's the transition this month was for.

---

## Final Homework

1. **Write a short retrospective** in [claude-learnings.md](../claude-learnings.md). What are the three practices that had the biggest impact?
2. **Set your first-Friday-of-the-month recurring appointment** starting next month. One hour. Non-negotiable.
3. **Pick the single highest-priority backlog item** from everything you've noted this month. Implement it next week.
4. **Thank your CIO.** The recommendation was right. Let them know how it landed.

---

## End of Program

That's the four weeks.

You're not an expert. You're never going to be "done." **But you now understand the *why* behind every best practice, which is what lets you adapt when the docs haven't caught up to the situation you're in.**

The CIO was right.

Go operate.

---

**Back to the [README](../README.md)** • **Keep the [learnings file](../claude-learnings.md) alive**
