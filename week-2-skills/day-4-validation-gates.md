# Week 2, Thursday — Quality Checklists and Validation Gates

**Time:** ~1 hour
**Goal:** Build explicit validation into each skill so it verifies its own work before returning output.
**Primary source:** [Complete Guide to Building Skills for Claude (PDF)](https://resources.anthropic.com/hubfs/The-Complete-Guide-to-Building-Skill-for-Claude.pdf)

---

## Tutor Prompt — Paste This Into Claude to Start

> You are my training tutor for **Week 2, Day 4: Quality Checklists and Validation Gates**. I learn best verbally — treat this like a tutoring session, not a lecture.
>
> First, read this full lesson file: `claude-training/week-2-skills/day-4-validation-gates.md`. Then ask me: which skill did I pick to restructure, and are the success criteria locked in from yesterday?
>
> Then:
> 1. Teach me what a validation gate looks like — three parts: what to check, what failure means, what to do when it fails. Check understanding.
> 2. For the skill I'm restructuring, **help me write the full validation gate** — copy-pasteable into SKILL.md. Use the examples in the lesson as starting points, but tailor to my actual skill.
> 3. Stress-test what I wrote. Ask "what failure mode would this gate miss?" Iterate until we can't find new holes.
> 4. Also sketch validation gates for my other three skills, even if I'm not restructuring them yet. Quick drafts, not full designs.
> 5. Save everything in `claude-training/claude-learnings.md` under today's date, including the full copy-paste-ready gate for the skill I'm restructuring.

---

## The Big Idea

Yesterday you defined what success looks like. Today you **make the skill check itself** against that definition before it hands output back to you.

Validation is Tier 3 of the three-tier architecture. It's the difference between "the skill produces something" and "the skill produces something **that meets the bar.**"

---

## What a Validation Gate Looks Like

A validation gate is a set of **explicit instructions** baked into SKILL.md telling Claude:
> "Before you return your output, run these checks. If any fail, fix them or flag them."

Not tests you run separately. Not code that runs externally. **Instructions Claude follows as part of the skill.**

---

## Anatomy of a Good Gate

Three parts:
1. **What to check** — the specific condition
2. **What failure means** — how to recognize it
3. **What to do when it fails** — regenerate, fix, flag, or refuse

Example from `instantly-csv-processor`:
```
## Validation — run before returning output
1. Confirm every row has exactly one email in the email column.
   - If a row is missing, reprocess that row.
2. Confirm no two rows share the same email address.
   - If duplicates exist, collapse them and preserve metadata from whichever row had more source fields.
3. Confirm every email matches `/^[^@\s]+@[^@\s]+\.[^@\s]+$/`.
   - If any email fails, drop it and add a note to the output header.
4. Confirm the row count equals the expected count from the input (minus intentional drops).
   - If not, flag the discrepancy in the output.
```

---

## Validation Gates for Each Skill

### `tce-brief-decoder`

```
## Validation
1. Confirm all five required fields (industry, budget, timeline, categories, overlap) are populated, or explicitly marked "not found."
2. Confirm at least 3 distinct expertise categories — if fewer, explain why in the output.
3. Confirm every boolean search string is syntactically valid (balanced parens, proper operators).
4. Confirm the overlap check was actually performed against the project archive (cite at least one compared project or state "no overlaps against [N] compared projects").
```

### `instantly-csv-processor`

```
## Validation
1. One email per row — no row has multiple or empty email fields.
2. No duplicate emails across the output.
3. Every email passes format regex.
4. Source metadata preserved on exploded rows.
5. Output row count reconciles with input (exploded count - intentional drops).
```

### `zerobounce-pipeline`

```
## Validation
1. Every input email has a ZeroBounce result (or an explicit failure note).
2. Score distribution is logged.
3. Distribution sanity check: if >95% of emails are "valid" in a cold list, flag for review (too good to be true).
4. Rate-limit and cost are logged for the run.
```

### `personalized-outreach`

```
## Validation
1. Every row has non-empty GeneratedEmail and SubjectLine.
2. No two GeneratedEmail fields are identical.
3. Every email references at least one specific fact about the recipient (role, company, background, or a brief-specific angle).
4. Voice check: scan for generic AI openers ("I hope this email finds you well", "I came across your profile", "I wanted to reach out"). If any appear, regenerate that row.
5. Length check: emails stay under 150 words unless the brief context requires longer.
```

---

## Where to Put the Validation

In SKILL.md, near the bottom, under a heading like `## Validation` or `## Before Returning Output`. Claude will see it every invocation and run through it.

---

## Homework

Pick your most important skill. Write its validation gate **in full** — copy-paste-ready to drop into SKILL.md.

Paste it in [claude-learnings.md](../claude-learnings.md) under today's date.

**Don't deploy it yet.** Friday you'll test against baseline to prove the validation gate actually improves output.

---

## What You Should Be Able to Answer by End of Day

- What makes a validation gate different from "good intentions"? → Explicit checks with explicit failure actions, baked into the skill.
- Where do validation gates live? → In SKILL.md (short ones) or `references/validation-checklist.md` (long ones).
- What's the most common validation failure mode? → Silent skips that assume "looks fine."

---

**Next up:** [Friday — Testing Against Baseline and Iteration](./day-5-baseline-and-iteration.md)
