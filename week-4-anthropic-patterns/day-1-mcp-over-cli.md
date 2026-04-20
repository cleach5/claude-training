# Week 4, Monday — MCP Servers Over CLI for Sensitive Data

**Time:** ~1 hour
**Goal:** Understand why Anthropic teams never put sensitive data in the CLI, and how MCP replaces it.
**Primary source:** [How Anthropic Teams Use Claude Code (PDF — search "anthropic teams claude code" to find the current link)](https://www.anthropic.com/customers)

---

## Tutor Prompt — Paste This Into Claude to Start

> You are my training tutor for **Week 4, Day 1: MCP Servers Over CLI for Sensitive Data**. I learn best verbally — treat this like a tutoring session, not a lecture.
>
> First, read this full lesson file: `claude-training/week-4-anthropic-patterns/day-1-mcp-over-cli.md`. Then ask me: have I ever pasted a credential, API key, or raw database query into Claude Code?
>
> Then:
> 1. Teach me what an MCP server is in one paragraph, then the 3 reasons MCP beats CLI (permissions, audit, context hygiene). Check understanding.
> 2. Teach me the propose-vs-execute distinction — why destructive operations should propose only, not apply.
> 3. **Inventory every sensitive system Claude Code currently touches** at TCE: Supabase/ExpertOps, Instantly, ZeroBounce, OneDrive/SharePoint, email infrastructure, the CMS. For each: is it CLI-based today, or already MCP?
> 4. Pick **one system to convert first** (likely ExpertOps/Supabase). Draft a short migration plan: what the MCP server needs to expose, what permissions it gates, what "propose only" operations are.
> 5. Log the full inventory + migration plan in `claude-training/claude-learnings.md` with today's date.

---

## The Lesson Anthropic Teams Learned the Hard Way

Don't pipe your Supabase credentials, API keys, or raw database queries through the command line into Claude Code.

**Why it fails:**
- Credentials land in your context window (logged, visible, sticky)
- No permission boundary — Claude can do anything the credentials allow
- Audit trail is poor or nonexistent

**What Anthropic's teams switched to:** **MCP servers.**

---

## What an MCP Server Is (One-Paragraph Version)

**MCP (Model Context Protocol) servers** sit between Claude and your sensitive systems. Claude talks to the MCP server through a defined interface — "query this table," "update this record," "list these files." The server does the sensitive thing and returns only what Claude actually asked for. Credentials never touch Claude's context.

Think of it as a **permission-gated API** Claude can call, instead of raw shell access.

---

## Three Reasons MCP Wins

### 1. Granular permission control
The MCP server defines exactly what Claude is allowed to do. Claude cannot arbitrarily `DROP TABLE` or expose credentials, because the server doesn't expose those operations.

### 2. Logging and audit trails
Every MCP call is logged. When something goes wrong, you have the forensic trail.

### 3. Context hygiene
Claude's context window stays clean. No connection strings, no API keys, no raw rows.

---

## Directly Relevant: Your ExpertOps Setup

You've got Supabase with expert profiles, bookings, payments, audit tables. Build an MCP server that exposes:

- `list_experts(filters)` — returns expert records, redacted as appropriate
- `update_expert_availability(id, availability)` — with audit logging baked in
- `query_active_projects()` — via the `active_projects` view only
- `propose_migration(name, sql)` — writes to a migration file, does NOT apply

Claude never sees your Supabase connection string.

---

## The Propose vs. Execute Distinction

- Reading data? Claude can do it directly via MCP.
- Non-destructive updates? Usually fine via MCP with audit logging.
- Schema changes, destructive updates, migrations? **Claude writes the proposal — a human applies it.**

---

## Applying This Across Your Stack

- **ExpertOps (Supabase):** MCP with read/update, migration proposals only, full audit
- **Instantly:** MCP for reading campaign stats; sending stays a human gate
- **ZeroBounce:** MCP for submitting jobs and retrieving results
- **OneDrive/SharePoint:** MCP for reading archives; writes human-reviewed
- **tce-website:** Claude works through repo, proposes via PRs, never deploys directly

**Pattern:** reads flow freely, writes go through review.

---

## What Not to Do

- `DATABASE_URL="postgres://..." claude-code` — credential now in session history
- `psql -c "SELECT * FROM experts;" | claude-code` — full result set in context
- `curl -H "Authorization: Bearer $API_KEY" ...` — token in every retry attempt

---

## Homework

1. List every sensitive system Claude Code currently touches.
2. For each, note: CLI or MCP? If CLI — that's a migration candidate.
3. Pick one to convert first. Write the migration plan in [claude-learnings.md](../claude-learnings.md).

---

## What You Should Be Able to Answer by End of Day

- What's the core failure mode of CLI for sensitive data? → Credentials and raw data bleed into context, no permission boundary, no audit.
- What does MCP solve? → Granular permissions, audit trails, clean context.
- When should Claude execute vs. propose? → Reads: execute. Destructive ops: propose only.

---

**Next up:** [Tuesday — CLAUDE.md as Your Data Catalog](./day-2-claude-md-as-catalog.md)
