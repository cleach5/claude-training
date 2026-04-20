# Claude Training Program — 4 Weeks, 1 Hour/Day

**Started:** 2026-04-19
**Mandate:** CIO recommended spending an hour a day reading Anthropic best practices and help documentation. This curriculum turns that recommendation into a structured program.

---

## Why This Exists

You're already running Claude harder than most TCE-scale operators — skills, Cowork, multiple MCP servers, Claude Code for the website, Supabase integration. But you're self-taught. This program closes the gap between **"using Claude"** and **"running Claude like a system."**

After four weeks you should understand not just *what* the best practices are, but *why* each one exists. That means you can improvise in situations the docs don't cover.

---

## How to Use This

- **One hour a day, Monday through Friday, for four weeks.**
- **This is designed to be guided by Claude**, not self-study. See [how-to-use.md](./how-to-use.md) for the full ritual.
- Every day's file has a **Tutor Prompt** block at the top — copy it, paste it into Claude, and Claude will teach you the lesson verbally, quiz you, and help you apply it to your real TCE work.
- Every day ends with a homework task. Most are reflection, not implementation. Do them.
- Keep [claude-learnings.md](./claude-learnings.md) open. Anything you read that would change a workflow, skill, or CLAUDE.md — drop it in with a date and a concrete action.
- Mark each day complete in the tracker below when you finish.

---

## Progress Tracker

### Week 1 — Claude Code Fundamentals
- [ ] [Monday: The Context Window Constraint](./week-1-claude-code/day-1-context-window.md)
- [ ] [Tuesday: CLAUDE.md Files and Persistent Memory](./week-1-claude-code/day-2-claude-md.md)
- [ ] [Wednesday: Research → Plan → Execute → Review → Ship](./week-1-claude-code/day-3-workflow-pattern.md)
- [ ] [Thursday: Parallel Sessions and Sub-Agents](./week-1-claude-code/day-4-parallel-sessions.md)
- [ ] [Friday: Failure Patterns to Avoid](./week-1-claude-code/day-5-failure-patterns.md)

### Week 2 — Skills Deep Dive
- [ ] [Monday: The Three-Tier Skill Architecture](./week-2-skills/day-1-three-tier-architecture.md)
- [ ] [Tuesday: Audit Your Existing TCE Skills](./week-2-skills/day-2-audit-existing-skills.md)
- [ ] [Wednesday: Skill Success Criteria](./week-2-skills/day-3-success-criteria.md)
- [ ] [Thursday: Quality Checklists and Validation Gates](./week-2-skills/day-4-validation-gates.md)
- [ ] [Friday: Testing Against Baseline and Iteration](./week-2-skills/day-5-baseline-and-iteration.md)

### Week 3 — Prompting Best Practices
- [ ] [Monday: XML Tags and Structural Clarity](./week-3-prompting/day-1-xml-tags.md)
- [ ] [Tuesday: Longform Data at the Top](./week-3-prompting/day-2-longform-data.md)
- [ ] [Wednesday: Ground Responses in Quotes](./week-3-prompting/day-3-grounding-in-quotes.md)
- [ ] [Thursday: Role Setting in System Prompts](./week-3-prompting/day-4-role-setting.md)
- [ ] [Friday: Avoiding Generic and "AI Slop" Aesthetic](./week-3-prompting/day-5-anti-slop.md)

### Week 4 — How Anthropic Teams Actually Use Claude Code
- [ ] [Monday: MCP Servers Over CLI for Sensitive Data](./week-4-anthropic-patterns/day-1-mcp-over-cli.md)
- [ ] [Tuesday: CLAUDE.md as Your Data Catalog](./week-4-anthropic-patterns/day-2-claude-md-as-catalog.md)
- [ ] [Wednesday: Session Sharing and Team Workflows](./week-4-anthropic-patterns/day-3-team-sessions.md)
- [ ] [Thursday: Skills for Bulk Operations](./week-4-anthropic-patterns/day-4-bulk-skills.md)
- [ ] [Friday: The Full Picture and Building Intuition](./week-4-anthropic-patterns/day-5-intuition-over-rules.md)

---

## Primary Source Links

- [Claude Code Best Practices](https://code.claude.com/docs/en/best-practices) — week 1 foundation
- [Complete Guide to Building Skills for Claude (PDF)](https://resources.anthropic.com/hubfs/The-Complete-Guide-to-Building-Skill-for-Claude.pdf) — week 2
- [Claude Prompting Best Practices](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices) — week 3
- How Anthropic Teams Use Claude Code (PDF, linked inside week 4 Monday) — week 4

---

## After Week 4 — Continuous Learning Rhythm

One month of front-loaded learning. After that, maintenance, not catch-up:

1. **Anthropic Discord** — scroll once a week, 15 min. Ask CIO for the invite link.
2. **Official blog / platform.claude.com / code.claude.com** — subscribe, skim new announcements.
3. **First Friday of every month** — one hour auditing your own workflows. Did anything new come out? Did you hit friction the docs could solve? Apply one thing.
4. **New Claude model releases** — read the migration guide only when upgrading. Don't chase every release.
5. **Keep the learnings file alive** — [claude-learnings.md](./claude-learnings.md). Pick one backlog item per month to actually implement.

The rhythm matters more than the volume.
