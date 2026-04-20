# Week 4, Wednesday — Session Sharing and Team Workflows

**Time:** ~1 hour
**Goal:** Turn individual Claude Code wins into team-wide leverage.
**Primary source:** How Anthropic Teams Use Claude Code (PDF)

---

## Tutor Prompt — Paste This Into Claude to Start

> You are my training tutor for **Week 4, Day 3: Session Sharing and Team Workflows**. I learn best verbally — treat this like a tutoring session, not a lecture.
>
> First, read this full lesson file: `claude-training/week-4-anthropic-patterns/day-3-team-sessions.md`. Then ask me: who on my team (Mujtaba, Abdullah, Masood, Hayden, Mousab, Ryan) is currently using Claude Code in any serious way? Who would benefit from watching me work for 30 minutes?
>
> Then:
> 1. Teach me why shared sessions propagate patterns faster than docs. Check understanding.
> 2. Teach me the 5/15/5/5 session structure: 5 min context, 15 min live walkthrough, 5 min what broke, 5 min Q&A.
> 3. Help me pick **my first demo topic** — a recent real win or failure from the last month.
> 4. Help me decide **who to invite** (start with 2–3, not everyone).
> 5. Pick the recurring weekly slot. Put it on the calendar in-session if possible.
> 6. Help me **start the `tce-claude-playbook.md`** at the repo root — seed with the demo topic I just picked.
> 7. Log everything in `claude-training/claude-learnings.md` with today's date.

---

## The Big Idea

Anthropic teams hold **sessions where members demo their Claude Code workflows to each other.** One engineer figures out a clever pattern, shows the team, everyone levels up. Patterns spread through **shared practice**, not documentation.

Right now you're learning Claude Code solo. Mujtaba, Abdullah, Masood, Hayden, Mousab are all using it (or could be) — but none of you see each other's wins. That's a huge amount of slack.

---

## Why Shared Sessions Beat Shared Docs

- Written documentation decays. Patterns demonstrated live are remembered.
- Watching someone else work reveals moves you wouldn't think to ask about.
- Questions get asked in real-time that never would in async docs.
- The demonstrator learns too — explaining a workflow forces them to structure it.

**Rule of thumb:** 30 minutes of shared session = 5 hours of async doc reading.

---

## The Format Anthropic Uses

### Weekly 30-minute session
Once a week, one person demos. Rotate.

### Structure
- 5 min: context — what were you trying to do?
- 15 min: live walkthrough — actually run the workflow in Claude Code
- 5 min: what broke, what you'd change
- 5 min: Q&A

### Recording and notes
Record it if you can. Keep a running log: **"patterns we've seen demo'd this quarter."** This becomes your team's internal playbook.

---

## What to Demo

### Failures and pivots are more valuable than wins
"I tried X, it blew up because Y, now I do Z." The team learns the trap without paying for it.

### Specific-tool tactics
- How you set up MCP for a sensitive system
- A prompt that unexpectedly worked (or didn't)
- A CLAUDE.md section that paid off disproportionately

---

## Who at TCE Should Be In These Sessions

Not everyone needs to be in every session:
- **Anyone using Claude Code on code** — must attend
- **Anyone using skills in daily ops** — should attend
- **Hayden** — walking through his own Claude Code session forces structure on his workflow
- **Ryan** — once tce-website is stable, absolutely

Start with a core 2–3 people. Grow from there.

---

## Slash Commands and Hooks as Shared Patterns

### Slash commands
Package a workflow as a slash command anyone on the team can invoke. `/decode-brief`, `/bulk-verify`. Once it's a slash command, the pattern propagates with zero friction.

### Hooks
Settings in `.claude/settings.json` that automate behavior. "Before running a destructive command, run X." These run without anyone thinking about them.

This is the difference between "I have a good workflow" and "my team has a good workflow."

---

## The Playbook File

Maintain a `tce-claude-playbook.md` — a running doc of the patterns your team has validated. Organized by:
- **Workflows** — new client brief end-to-end, expert outreach campaign
- **Skills** — with links to their SKILL.md files and success criteria
- **Slash commands** — what each does, when to use
- **Failure patterns we've hit** — the traps we've learned

---

## Homework

1. **Schedule your first session.** Pick a day/time that can become weekly — not a one-off.
2. **Draft a demo topic.** Pick the highest-value workflow you've built or restructured this month.
3. **Start the playbook file.** Create `tce-claude-playbook.md`. Add one entry — the workflow you're about to demo.
4. **Invite the right people.** Start with 2–3.

Log the schedule and topic in [claude-learnings.md](../claude-learnings.md).

---

## What You Should Be Able to Answer by End of Day

- Why do shared sessions beat shared docs? → Live demo reveals moves you wouldn't think to ask about.
- What's the difference between personal leverage and institutional leverage? → Personal = you know it. Institutional = slash commands, hooks, playbook, new hires absorb it automatically.
- What's the simplest first step? → One recurring 30-minute weekly session with 2–3 people.

---

**Next up:** [Thursday — Skills for Bulk Operations](./day-4-bulk-skills.md)
