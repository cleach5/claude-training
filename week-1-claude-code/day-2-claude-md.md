# Week 1, Tuesday — CLAUDE.md Files and Persistent Memory

**Time:** ~1 hour (30 min reading, 30 min hands-on)
**Goal:** Build your first CLAUDE.md for ExpertOps.
**Primary source:** [Claude Code Best Practices — CLAUDE.md](https://code.claude.com/docs/en/best-practices)

---

## Tutor Prompt — Paste This Into Claude to Start

> You are my training tutor for **Week 1, Day 2: CLAUDE.md Files and Persistent Memory**. I learn best verbally — treat this like a tutoring session, not a lecture.
>
> First, read this full lesson file: `claude-training/week-1-claude-code/day-2-claude-md.md`. Then ask me: did I do yesterday's homework? What project did I pick? Am I ready to build a CLAUDE.md today?
>
> Then:
> 1. Teach me what CLAUDE.md is and why it matters, using ExpertOps as the running example. Pause to check understanding.
> 2. Today is **hands-on** — we're actually building a CLAUDE.md for ExpertOps by end of session. Have me open a terminal in the ExpertOps project directory and run `/init` in Claude Code. Let it generate a starter.
> 3. Spend the bulk of the session refining the draft together: schema, MCP setup, business logic, query patterns, data quality standards. Ask me questions about my actual Supabase setup so the file reflects reality, not a template.
> 4. Help me save and commit the final CLAUDE.md.
> 5. Log the result in `claude-training/claude-learnings.md` with today's date — what I built, what surprised me, what I'll still refine.
>
> Note: the training originally had me target tce-website here, but that's being troubleshot with Ryan. **ExpertOps is the correct target** — reference the Week 1 Tuesday lesson.

---

## The Big Idea

Yesterday you learned that context is finite and degrades. **Today's move is the answer:** give Claude persistent memory across sessions without burning your context window.

A **CLAUDE.md** file lives in your project root. Claude reads it automatically at the start of every conversation. It's a standing brief that persists across sessions — your chance to tell Claude everything about your project *without re-explaining it every time.*

---

## What Goes in CLAUDE.md

- **Project structure** — where frontend lives, where backend is, where the schema is.
- **Build and test commands** — how do you run this? What's the test command?
- **Coding style** — functional vs. class components, naming conventions, linting rules.
- **Workflow rules** — deployment process, review requirements, pre-ship checklist.
- **Key dependencies** and their versions.
- **Gotchas and patterns** specific to your project.

---

## What *Not* to Put in CLAUDE.md

- Your entire codebase. Don't copy-paste files.
- Long reference manuals. Claude reads CLAUDE.md every session — bloat hurts everyone.
- Target: **500–1,000 words.** Readable. Scannable.

CLAUDE.md is a **guide**, not a reference manual. It says "here's how to navigate this project," not "here's every line of code."

---

## Why It Matters

- **Faster orientation.** Instead of Claude reading 5 files to understand structure, it reads CLAUDE.md in 30 seconds.
- **Consistent behavior across sessions.** You don't re-explain "we use Next.js with Tailwind and Supabase" every time.
- **Clean context.** Tokens you saved on discovery are available for actual work.
- **Team leverage.** When Mujtaba, Abdullah, or Masood start a Claude Code session on the same project, they all start from the same baseline.

---

## How You Build One

Anthropic ships a command: `/init`. You run it in your project directory and it auto-generates a starter CLAUDE.md by analyzing your codebase (package.json, file structure, config files). Then you refine it — add your actual deployment process, coding standards, and gotchas.

---

## Concrete Example — What ExpertOps' CLAUDE.md Might Contain

```markdown
# ExpertOps

TCE's expert database and project-matching system, running on Supabase.

## Access
All queries go through the Supabase MCP server, never direct CLI.
Credentials are never pasted into prompts.

## Schema
- `experts` — expert profiles, capacity, specialties
- `projects` — active TCE project records
- `bookings` — expert-to-project assignments
- `payments` — payment status per booking
(See references/schema.md for field-level detail.)

## Business Logic
- An expert is "available" when bookings.active_count < experts.max_capacity
- Project matching is bounded by specialty overlap + availability + rate band
- Audit: every expert update logs to experts_audit

## Query Patterns That Work
- Filter experts by specialty tag array before joining bookings
- Use the `active_projects` view, not raw projects table
- Always scope by tenant_id

## Data Quality Standards
- Email addresses pass ZeroBounce verification before they touch outreach
- Expert capacity is refreshed weekly from the `expert_availability` form

## Deployment
- Schema changes go through migration files in /supabase/migrations
- Test migrations in staging before production
- Claude Code should propose migrations, not apply them directly
```

That's roughly 250 words. Claude now starts every ExpertOps session knowing all of that **without asking**.

---

## Why ExpertOps First (not tce-website)

Originally Tuesday was going to be `tce-website`, but Ryan is still troubleshooting that project and the skill access isn't stable. **ExpertOps is cleaner:**

- Defined Supabase schema
- Not tangled in active troubleshooting
- Directly runs the business
- MCP server setup is well-defined

`tce-website` will wait until it's in a stable state. `zerobounce-pipeline` is next after ExpertOps — also clean and self-contained.

---

## The Iteration Pattern

CLAUDE.md isn't static:
- New dependency → add it.
- Changed deployment process → update it.
- New coding standard → document it.

**Once a month, 15 minutes: refresh CLAUDE.md.** Stale documentation is worse than none.

---

## Homework

1. Open a terminal in your ExpertOps project directory.
2. Run `/init` inside Claude Code. Let it generate a starter CLAUDE.md.
3. Spend 30 minutes refining it:
   - Document the Supabase schema (high level — field detail goes in a references/ file if you need it)
   - Document the MCP server setup and what Claude is allowed to access
   - Document business logic (capacity flow, matching rules, audit requirements)
   - Document your data quality standards
4. Save it. Commit it.

**Deliverable:** one ExpertOps CLAUDE.md, fully baked.

---

## What You Should Be Able to Answer by End of Day

- What's the difference between what goes *in* CLAUDE.md and what goes in your codebase? → CLAUDE.md = how to navigate; codebase = the actual thing.
- Why doesn't Claude just read all my files every session? → Context is finite (yesterday's lesson). CLAUDE.md is pre-loaded knowledge that doesn't bloat the window.
- How do I keep it accurate over time? → Monthly 15-min refresh. Stale > missing.

---

**Next up:** [Wednesday — Research → Plan → Execute → Review → Ship](./day-3-workflow-pattern.md)
