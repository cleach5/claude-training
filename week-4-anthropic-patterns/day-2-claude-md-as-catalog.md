# Week 4, Tuesday — CLAUDE.md as Your Data Catalog

**Time:** ~1 hour
**Goal:** Upgrade CLAUDE.md from "project notes" to the actual source of truth for how your systems fit together.
**Primary source:** How Anthropic Teams Use Claude Code (PDF)

---

## Tutor Prompt — Paste This Into Claude to Start

> You are my training tutor for **Week 4, Day 2: CLAUDE.md as Your Data Catalog**. I learn best verbally — treat this like a tutoring session, not a lecture. **Today is hands-on — we're upgrading a real file.**
>
> First, read this full lesson file: `claude-training/week-4-anthropic-patterns/day-2-claude-md-as-catalog.md`. Then ask me to open the ExpertOps CLAUDE.md I built in Week 1 Tuesday. We're going to layer on catalog-grade sections today.
>
> Then:
> 1. Teach me the difference between basic CLAUDE.md and catalog-grade CLAUDE.md — briefly. The real work is the upgrade.
> 2. Walk me through adding each of the 5 sections to my existing ExpertOps CLAUDE.md: **System Map, Schema Reference, Business Logic, Query Patterns, Workflow**. Start with System Map and Business Logic — highest leverage.
> 3. For each section, ask me the real questions about how ExpertOps works. Don't let me write generic content — this has to reflect reality.
> 4. Target length: 1,000–1,500 words total. Save and commit.
> 5. **Test it** — open a fresh Claude Code session on ExpertOps and ask something I wouldn't have expected Claude to know. Did the enriched CLAUDE.md carry it?
> 6. Log the result in `claude-training/claude-learnings.md` with today's date.

---

## The Big Idea

Week 1 Tuesday you built a basic CLAUDE.md for ExpertOps. **Anthropic's data infrastructure team takes this much further.** They use CLAUDE.md files to **replace traditional data catalogs** — the documentation layer that tells engineers which upstream sources feed which dashboards, what transformations happen where, and where dependencies live.

Instead of hunting through Notion pages or wiki docs, **Claude reads CLAUDE.md and understands the system.**

---

## What Goes In a Catalog-Grade CLAUDE.md

### 1. System map
```markdown
## System Map — ExpertOps

- Source of truth: Supabase `experts` table
- Upstream: admin form (manual), weekly availability form, Hayden's capacity backfills
- Downstream:
  - `project_matches` (internal view)
  - `bookings` (links experts to active projects)
  - Instantly campaigns (via `personalized-outreach` skill)
  - Payment records (post-booking)
- MCP boundary: all reads/writes go through `expertops-mcp`; no direct CLI
```

### 2. Schema reference (high level)
```markdown
## Core Tables

- `experts` — one row per expert profile
  - `capacity_tier` drives matching eligibility
  - `last_verified_at` — >90 days old = stale, needs refresh before outreach
  - `tenant_id` — always scope queries here
- `bookings` — many-to-one to experts
  - `active_count` joins back to determine availability
- `experts_audit` — append-only, never queried in matching but used for review
```

### 3. Business logic that isn't in the code
```markdown
## Business Logic

- An expert is "available" when `bookings.active_count < experts.max_capacity`
- Matching requires: specialty overlap + availability + rate within brief's band
- Experts with `last_verified_at` older than 90 days are not outreach-eligible
- If a brief doesn't name a budget, cap outreach at $800/hr expert rates
- Never contact experts flagged `do_not_contact=true` — this is a legal gate
```

### 4. Query patterns that work (and don't)
```markdown
## Query Patterns

Good:
- Filter experts by specialty tag array before joining bookings
- Use the `active_projects` view, not raw `projects` table
- Always `WHERE tenant_id = $1`

Bad:
- Joining `experts` x `bookings` x `payments` in one query (slow; break it up)
- Selecting `*` from `experts` (some columns are large JSON blobs)
- Direct CLI access — all DB ops go through expertops-mcp
```

### 5. Workflow rules
```markdown
## Workflow

- Schema changes: proposal → migration file → human review → apply
- Code changes: PR → review → Vercel preview → merge to main → auto-deploy
- Outreach campaigns: brief decode → contact list → ZeroBounce → personalize → manual review → send
- No automated sends without human gate
```

---

## Why This Pays Off

- **Onboarding:** When Mujtaba, Abdullah, or a new associate starts a Claude Code session on ExpertOps, they don't need hand-holding. Claude reads CLAUDE.md and explains the system.
- **Quality of suggestions:** Claude's proposals actually reflect your system.
- **Durability:** A living CLAUDE.md is the institutional memory. Update it monthly.

---

## Homework

1. Open your ExpertOps CLAUDE.md from Week 1 Tuesday.
2. Add the five catalog-grade sections. Start with **System map** and **Business logic**.
3. Save it. Commit it.
4. Test: open a fresh Claude Code session on ExpertOps and ask something you wouldn't have expected Claude to know.
5. Log the result in [claude-learnings.md](../claude-learnings.md).

---

## What You Should Be Able to Answer by End of Day

- What's the difference between basic and catalog-grade CLAUDE.md? → Basic = build/test commands + structure. Catalog = system map, business logic, query patterns.
- What's the biggest payoff? → Onboarding becomes "hours" instead of "weeks."
- How often do I refresh it? → Monthly, 15-minute pass.

---

**Next up:** [Wednesday — Session Sharing and Team Workflows](./day-3-team-sessions.md)
