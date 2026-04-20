# Week 1, Friday — Failure Patterns to Avoid

**Time:** ~1 hour
**Goal:** Recognize the traps before you fall in them.
**Primary source:** [Claude Code Best Practices — Common Failures](https://code.claude.com/docs/en/best-practices)

---

## Tutor Prompt — Paste This Into Claude to Start

> You are my training tutor for **Week 1, Day 5: Failure Patterns to Avoid**. I learn best verbally — treat this like a tutoring session, not a lecture.
>
> First, read this full lesson file: `claude-training/week-1-claude-code/day-5-failure-patterns.md`. Then ask me: describe the last long Claude Code session I ran. What was I doing? How did it go? Was there a moment where output quality dropped or Claude started repeating itself?
>
> Then:
> 1. Walk me through all 8 failure patterns conversationally. After each one, ask if I've hit that pattern recently — and if yes, what I did about it.
> 2. From the session I described at the start, help me **diagnose which failure patterns I actually hit**. Be honest with me; don't let me off the hook.
> 3. Pick **the one pattern with the biggest impact** if I stopped doing it. Make me commit to a specific change — what I'll do differently next session.
> 4. Write the commitment in `claude-training/claude-learnings.md` with today's date and an action I can check off later.
> 5. Close by zooming out: we've finished Week 1. What are the two or three things from this week that already changed how I think about working with Claude?

---

## The Big Idea

By now you understand:
- The context window constraint (Monday)
- CLAUDE.md for persistent memory (Tuesday)
- The five-stage workflow (Wednesday)
- Parallel sessions (Thursday)

Today is about **what breaks Claude Code workflows.** Knowing the traps is how you avoid them.

---

## The Eight Failure Patterns

### 1. Context Bloat Without Checkpoints

**The trap:** Running a session for 8 hours straight.

**What happens:** Claude's performance degrades gradually. By hour 8 you're getting mistakes you wouldn't see in hour 2.

**The fix:** Every 2–3 hours, **save what you've learned, end the session, start fresh.** Write the summary into CLAUDE.md or a notes file so the next session picks up where you left off.

---

### 2. Asking Claude to Remember Instructions From Hours Ago

**The trap:** "At the beginning of this session I told you we never modify the X table directly — why are you modifying it?"

**What happens:** After enough files read and commands run, Claude genuinely forgets. It's not defiance; it's context buried at the top of a full window.

**The fix:** If an instruction matters, put it in **CLAUDE.md** (permanent) or **repeat it in the current session** near the relevant ask. Don't assume persistence over time.

---

### 3. Mixing Debug and Build in One Session

**The trap:** You're building a feature, hit a bug, try to debug and keep building in the same conversation.

**What happens:** Context explodes. You miss things. Claude starts confusing the broken state with the intended state.

**The fix:** Finish the build, end the session. **Start a fresh session just for debugging.** Fresh eyes, clean context.

---

### 4. Using CLI for Sensitive Data

**The trap:** Piping Supabase credentials, API keys, or raw database queries through the terminal into Claude Code.

**What happens:** Credentials land in your context window. Logs. Session history. Security surface expands.

**The fix:** **MCP servers.** They gate what Claude can access, log what it does, protect sensitive data. Your ExpertOps Supabase setup needs this. Claude never sees raw credentials — it uses a defined interface.

More on this in [Week 4 Monday](../week-4-anthropic-patterns/day-1-mcp-over-cli.md).

---

### 5. Vague Prompts With Huge Codebases

**The trap:** "Optimize this project" → into a 10,000-file codebase.

**What happens:** Claude doesn't know where to start. Context gets wasted on exploration. Quality drops.

**The fix:** **Be specific.** "Optimize the expert matching algorithm in `/lib/matching.ts`." Now Claude has a clear target and the whole context window is available for real work.

---

### 6. Assuming Fresh Instances Share Memory

**The trap:** Sub-agent 1 learns something important. You assume sub-agent 2 knows it too. It doesn't.

**What happens:** Sub-agent 2 duplicates work, makes conflicting decisions, or ignores the learning entirely.

**The fix:** **Shared documentation** — CLAUDE.md, status files, decision logs. If a fact matters across instances, write it down where all of them read.

---

### 7. Review in the Same Session as Execution

**The trap:** "Claude, you just built this — now review it for bugs."

**What happens:** The Claude that wrote the code has **context bias**. It's attached to what it wrote. It'll defend or miss its own bugs.

**The fix:** Review happens in a **fresh instance.** New conversation, clean context, load the code fresh. Bugs jump out that the builder missed.

---

### 8. Letting CLAUDE.md Get Stale

**The trap:** Build CLAUDE.md once, never touch it again.

**What happens:** Six months later, project has evolved, CLAUDE.md says the old thing. Claude gets confidently wrong answers.

**The fix:** **Monthly 15-minute refresh.** Stale documentation is worse than missing documentation because Claude trusts it.

---

## One More Pattern: Ignoring Degrading Output

If Claude starts:
- Repeating itself
- Giving generic answers
- Missing details you already gave it

**That's context fullness signaling.** Don't push through. Save state, start fresh. Your output quality matters more than session continuity.

---

## Homework

Review one Claude Code session you've done recently — or imagine one you're about to do.

1. **Which of these patterns would you likely hit?** (Honest answer. All of us hit at least one.)
2. **Which one would have the biggest impact if you stopped doing it?**
3. **What's one concrete change you'll make?** Write it in [claude-learnings.md](../claude-learnings.md) with a date.

You're not implementing anything today. You're **training yourself to recognize the traps before you fall in them.**

---

## End of Week 1 — Where You Are

You've got the foundation:

- ✓ Context constraint understood
- ✓ CLAUDE.md built for ExpertOps (if you did Tuesday's homework)
- ✓ Five-stage workflow locked
- ✓ Parallel sessions understood
- ✓ Failure patterns recognized

You're not an expert yet — but you understand **the *why* behind every best practice.** Everything in week 2 (skills), week 3 (prompting), and week 4 (enterprise patterns) builds on this foundation.

---

## What You Should Be Able to Answer by End of Day

- Why does Claude "forget" things I said at the start? → Context bloat pushes early instructions out of active attention.
- Why should review happen in a fresh session? → Context bias — the builder won't catch its own bugs.
- What's the single highest-impact hygiene habit? → Don't let sessions run 8+ hours. End them, summarize, restart.
- When do I know context is too full? → Repetition, generic answers, missed details. Stop and restart.

---

**Next up:** [Week 2, Monday — The Three-Tier Skill Architecture](../week-2-skills/day-1-three-tier-architecture.md)
