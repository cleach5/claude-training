# Week 3, Thursday — Role Setting in System Prompts

**Time:** ~1 hour
**Goal:** One clear sentence of role framing changes Claude's entire behavior. Learn what goes in it.
**Primary source:** [Claude Prompting Best Practices](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices)

---

## Tutor Prompt — Paste This Into Claude to Start

> You are my training tutor for **Week 3, Day 4: Role Setting in System Prompts**. I learn best verbally — treat this like a tutoring session, not a lecture.
>
> First, read this full lesson file: `claude-training/week-3-prompting/day-4-role-setting.md`. Then ask me: do my skill outputs currently sound like TCE, or do they drift into generic AI voice? Which skill is the worst offender?
>
> Then:
> 1. Teach me the 4 elements of a good role framing: what Claude is, domain, job, what to value. Walk through the examples. Check understanding.
> 2. Call out the two anti-patterns: superlatives (makes Claude hedge) and "helpful assistant" (triggers AI slop voice).
> 3. Help me write **one role sentence for each of my four skills** — tce-brief-decoder, instantly-csv-processor, zerobounce-pipeline, personalized-outreach. Push back if any feel generic.
> 4. Pick the skill that was the worst offender and **drop the new role framing into SKILL.md**.
> 5. Run the skill on real input. Compare register and tone against prior output.
> 6. Log all four role sentences + the before/after comparison in `claude-training/claude-learnings.md` with today's date.

---

## The Big Idea

A **single sentence** in your system prompt or SKILL.md changes Claude's register, rigor, and priorities.

- Bad: *"Analyze this brief."*
- Good: *"You are a TCE brief analyst specializing in supply chain intelligence. Your job is to decode Inex One briefs into actionable expert-sourcing plans. Specific beats generic. Always cite source passages."*

Same skill. Different Claude.

---

## Anatomy of a Good Role

### 1. What Claude *is*
Not "an AI assistant." Instead: "a TCE brief analyst," "a data quality gatekeeper," "an executive recruiter."

### 2. What Claude's domain is
Narrow the expertise. "Supply chain intelligence." "Email verification and sender reputation."

### 3. What Claude's job is
The verb. "Decode briefs into expert-sourcing plans." "Verify emails before they touch outreach."

### 4. What Claude should value
The single most important operating principle. "Specific beats generic." "Protect the sender reputation."

---

## Role Definitions for Each TCE Skill

### `tce-brief-decoder`
> "You are a TCE brief analyst specializing in executive recruiting and expert sourcing. Your job is to decode Inex One project briefs into actionable expert-sourcing plans with specific titles, companies, and sourcing angles. Specific beats generic. Always cite source passages from the brief. Flag ambiguity instead of filling it in."

### `instantly-csv-processor`
> "You are a data quality gatekeeper for TCE's outreach pipeline. Your job is to transform raw lead-list CSVs into Instantly-ready files where each row is exactly one valid, unique email address. No silent data loss. Every exploded row preserves source metadata."

### `zerobounce-pipeline`
> "You are the email verification layer protecting TCE's sender reputation. Your job is to run contact lists through ZeroBounce verification and produce a clean, verified-contacts CSV ready for outreach. If score distribution looks suspicious, flag it. Your failure mode is letting a risky email through."

### `personalized-outreach`
> "You are a TCE executive recruiter writing outbound expert outreach for Instantly campaigns. Each email must read like it was hand-written by a professional who researched the contact — not a content marketer's sequence. Specific beats generic. Reference one researched fact per contact. Never use generic openers. If you can't ground the personalization in provided data, flag the contact for manual review."

---

## Where Role Goes in the Prompt

- At the **top of SKILL.md**, in a `<role>` tag
- In CLAUDE.md for project-level framing
- As the first sentence before any `<task>` tag in ad-hoc prompts

---

## The Stakes Anti-Pattern

Bad: "You are a brilliant, world-class, award-winning analyst who never makes mistakes..."

Claude gets cautious. Output gets vague. Everything becomes "it depends."

**Stay grounded.** Specific job, specific domain, specific value.

---

## The Generic-Job Anti-Pattern

"You are a helpful assistant."

Claude defaults to the lowest-common-denominator voice. That's the AI slop voice.

---

## Homework

For each of your four skills, **write one role sentence** in the four-element format. Drop them into [claude-learnings.md](../claude-learnings.md).

Then pick one skill, update SKILL.md with the new role framing, run it on a recent real input. Does the new version:
- Sound more like TCE?
- Make sharper, more specific choices?
- Avoid the generic AI tone?

---

## What You Should Be Able to Answer by End of Day

- What are the four elements of a good role? → What Claude is, domain, job, what to value.
- Why does "helpful assistant" hurt? → It triggers the generic AI slop voice.
- Why not use superlatives? → They make Claude cautious and vague.

---

**Next up:** [Friday — Avoiding Generic and "AI Slop" Aesthetic](./day-5-anti-slop.md)
