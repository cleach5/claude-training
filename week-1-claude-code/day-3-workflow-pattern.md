# Week 1, Wednesday — Research → Plan → Execute → Review → Ship

**Time:** ~1 hour
**Goal:** Learn the workflow pattern that keeps Claude focused and gates quality at every stage.
**Primary source:** [Claude Code Best Practices — Workflow](https://code.claude.com/docs/en/best-practices)

---

## Tutor Prompt — Paste This Into Claude to Start

> You are my training tutor for **Week 1, Day 3: The Research → Plan → Execute → Review → Ship Workflow**. I learn best verbally — treat this like a tutoring session, not a lecture.
>
> First, read this full lesson file: `claude-training/week-1-claude-code/day-3-workflow-pattern.md`. Then ask me: did I finish the ExpertOps CLAUDE.md yesterday? What's one feature or fix I'm actually planning to build on ExpertOps soon?
>
> Then:
> 1. Teach me the 5-stage workflow conversationally. Pause to check understanding at each stage. Use the ExpertOps feature I named as the running example throughout.
> 2. For that real feature, **walk me through mapping all 5 stages before I write any code**: what does Research look like? What's the Plan? What's the Execute scope? Who reviews? What's Ship? Push back if I combine stages that shouldn't be combined.
> 3. Show me the exact prompt wording for each stage (Research prompt, Plan prompt, Execute prompt, etc.) so I have a copy-pasteable template.
> 4. Walk me through writing the homework map in `claude-training/claude-learnings.md`.
>
> By end of session I should have a concrete 5-stage plan for one real ExpertOps feature, ready to execute next week.

---

## The Big Idea

Instead of asking Claude to build something and watching it dump code, you **break work into five stages**. Each stage has a clear purpose. Each stage keeps Claude's attention focused. Each stage gates quality before moving on.

This is how Anthropic's own data infrastructure team works. It's slower to set up than "just build me a thing," but it's **faster overall** because you catch problems before they're coded.

---

## The Five Stages

### 1. Research

Claude explores the codebase. Reads relevant files. Asks clarifying questions. **Nothing is built yet.**

For ExpertOps, if you're building a capacity-tracking feature, Claude starts by:
- Reading your CLAUDE.md
- Understanding the schema
- Looking at existing capacity code
- Mapping dependencies

Research answers: *"What do I actually need to understand to do this right?"*

### 2. Plan

Claude proposes an approach before touching code:
> "Here's how I'd structure the new capacity tracking feature. Here's what tables I'd touch. Here's the API changes. Here's the MCP server additions."

**You review the plan.** Ask questions. Approve or redirect. This is where bad architecture gets caught — **before** it's implemented.

### 3. Execute

Now Claude builds. But it's building a **specific plan you approved**, not exploring open-ended. Claude doesn't drift into "I could also add this other thing." It does the thing.

### 4. Review

Here's where freshness matters. **Ideally a different Claude instance** — fresh context, no bias toward code it just wrote — reviews the work:
- Does it match the plan?
- Are there bugs?
- Is code style consistent?

The Claude that just built code has context bias. A fresh instance catches what the builder missed.

### 5. Ship

Final check. Tests pass? Deployment ready? Push.

---

## Why This Works (the context view)

Each stage is focused. None requires the others' context:
- **Research** doesn't need Execute context.
- **Execute** doesn't need Research context (just the plan).
- **Review** doesn't need Execute bias.

You're not asking one Claude to do all five things in one conversation — **that's where context bloat happens.** You're breaking it across sessions. Each session stays small, focused, and sharp.

### Rough token budgets per stage
- Research: ~10,000 tokens reading + understanding
- Plan: ~2,000 tokens of discussion
- Execute: focused — build this specific thing
- Review: ~3,000 tokens of checking (fresh context)
- Ship: ~50 tokens — confirm and deploy

---

## Concrete Example — Bulk Expert Availability Updates (ExpertOps)

**Research:**
> "Explore how we currently handle expert availability updates. What's the current flow? What constraints exist?"

Claude reads the availability code, the bookings table, the audit logging.

**Plan:**
> "Propose an approach for bulk availability updates. What would you change? What new tables or columns?"

Claude proposes: a batch job, updates to `experts`, audit entries in `experts_audit`, notification triggers. You say yes, or ask for changes.

**Execute:**
> "Build the bulk update feature following this plan: [paste the plan]. Here's the code structure. Go."

**Review (new session):**
> "Review this code for bulk expert updates. Does it match the plan? Are there bugs? Is it production-ready?"

**Ship:**
> "Merge and deploy to production."

Each prompt is **explicit about what stage you're in.**

---

## When to Combine Stages

The pattern is flexible, not absolute:
- Research + Plan in one session → fine for small projects
- Execute + Review together → fine for tiny changes

**Principle:** Keep each conversation focused enough that Claude stays sharp. If context feels thick, split.

---

## Homework

Think about a real feature or fix you want to make to ExpertOps. **Don't execute anything yet.** Just map out the five stages:

- Where does Research end and Planning begin?
- Where does Execution start?
- When would you want Review?
- What's the actual Ship step?

Write it in [claude-learnings.md](../claude-learnings.md).

---

## What You Should Be Able to Answer by End of Day

- Why split a build into stages? → Context stays focused; quality gets caught at each gate.
- Why does Review need a fresh Claude instance? → The Claude that built it has context bias; fresh eyes catch more.
- What's the biggest mistake people make? → Asking Claude to build AND debug AND review in one conversation. Context explodes.

---

**Next up:** [Thursday — Parallel Sessions and Sub-Agents](./day-4-parallel-sessions.md)
