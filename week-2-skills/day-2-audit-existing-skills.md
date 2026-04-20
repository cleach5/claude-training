# Week 2, Tuesday — Audit Your Existing TCE Skills

**Time:** ~1 hour
**Goal:** Run a three-tier audit on your four existing skills and find the tightening opportunities.
**Primary source:** [Complete Guide to Building Skills for Claude (PDF)](https://resources.anthropic.com/hubfs/The-Complete-Guide-to-Building-Skill-for-Claude.pdf)

---

## Tutor Prompt — Paste This Into Claude to Start

> You are my training tutor for **Week 2, Day 2: Audit Your Existing TCE Skills**. I learn best verbally — treat this like a tutoring session, not a lecture.
>
> First, read this full lesson file: `claude-training/week-2-skills/day-2-audit-existing-skills.md`. Then ask me: am I ready to go deep on all four skills today? (Set expectation — this is a working session, not a listening session.)
>
> Then:
> 1. Explain the 4-question audit framework briefly — just enough to orient me.
> 2. Run the audit on each of my four skills in sequence: **tce-brief-decoder, instantly-csv-processor, zerobounce-pipeline, personalized-outreach.**
> 3. For each skill: have me open the SKILL.md, read through it with you, answer the 4 questions (Is it focused? What should move to references? Is there validation? Is it doing too many things?). Don't rush.
> 4. Keep a running summary in `claude-training/claude-learnings.md` under today's date. One short diagnosis block per skill. Call out the single highest-priority change per skill.
> 5. Close by having me pick **one skill to restructure first** — the most bloated or highest-leverage one. That's the skill we'll work on the rest of the week.

---

## The Skills You're Auditing

1. `tce-brief-decoder`
2. `instantly-csv-processor`
3. `zerobounce-pipeline`
4. `personalized-outreach`

You built these before reading the playbook. Today is the honest look.

---

## The Audit Framework

For each skill, answer four questions:

### Q1. Is SKILL.md actually focused?

Open each skill's SKILL.md. Read it top to bottom.

- How long is it? (pages / rough word count)
- Is the trigger description clear and specific?
- Did you bury the lede with examples?
- Are there instructions that only apply in rare cases, or that belong in references?

**Red flag:** SKILL.md is over ~1,500 words. That's burn-rate territory.

### Q2. Do I have reference docs that should live separately?

Look for these patterns **inside SKILL.md**:
- Long lists of examples
- Domain knowledge (industries, client archives, templates)
- Edge-case handling that doesn't apply to most invocations
- API response shape documentation

**If it's in SKILL.md, it loads every time.** If Claude only needs it sometimes, move it to `references/` and point SKILL.md at it.

### Q3. Are there validation steps I'm skipping?

Look at the end of SKILL.md. Does it say anything like:
> "Before returning, verify that [X]. If it fails, [regenerate / fix / flag]."

If not — **you're skipping Tier 3.** Most people do.

### Q4. Is the skill doing too many things?

If the skill's description is "it parses briefs, cross-references OneDrive, and generates outreach," that's probably **three skills wearing a trench coat.** Each concern deserves its own skill, and they can chain together.

---

## The Four Audits

### `tce-brief-decoder`

Likely issues:
- Doing brief parsing **and** OneDrive cross-reference **and** boolean string generation — three concerns in one
- Project archive knowledge probably in-line (should be `references/project-archive.md`)
- No explicit validation at the end (did we actually find overlap or just claim we did?)

**Split candidates:** consider separating parse → overlap-check → boolean-generation as tiers or chained skills.

### `instantly-csv-processor`

Likely issues:
- Email validation rules probably in-line
- Deduplication logic probably in-line
- Instantly API format expectations probably in-line

**Quick wins:**
- Move format spec to `references/instantly-format.md`
- Move validation rules to `references/email-validation-rules.md`
- Keep SKILL.md focused on **flow**: "read CSV → explode emails → dedupe → validate → write Instantly-ready CSV"
- Add explicit validation: "confirm every row has exactly one email, every email is unique, every email passes format check"

### `zerobounce-pipeline`

Likely issues:
- ZeroBounce API response schema probably in-line
- Score thresholds probably in-line
- Clean-list output format probably in-line

**Quick wins:**
- Move API schema to `references/zerobounce-api.md`
- Move score thresholds to `references/verification-thresholds.md`
- Add validation: "confirm score distribution is within expected range before returning"

### `personalized-outreach`

Likely issues:
- Email templates probably in-line
- Voice/tone guidance probably in-line
- Sector-specific angles probably in-line

**Quick wins:**
- Move templates to `references/outreach-templates.md`
- Move voice guide to `references/tce-voice.md`
- Keep SKILL.md focused on **the flow**: "take verified contacts + brief context → personalize per contact → validate → output Instantly-ready CSV"
- Add validation: "confirm every row has a non-empty subject line and non-empty body; confirm no two emails are identical"

---

## What to Do Right Now

**Don't rewrite anything yet.** Today is diagnosis, not surgery.

For each of the four skills:

1. Open the SKILL.md
2. Run it through the four questions above
3. Write the answers in [claude-learnings.md](../claude-learnings.md) under a heading like:
   ```
   ### 2026-04-21 — Skills Audit
   **tce-brief-decoder**
   - Length: ~2,100 words (too long)
   - Candidates for references/: project archive, boolean patterns
   - No validation step — needs one
   - Doing 3 things, consider splitting
   ```

You're building the **backlog** of changes. You'll work through them over Wednesday–Friday with success criteria and baseline testing.

---

## What You Should Be Able to Answer by End of Day

- Which of my four skills is the most bloated? (pick one)
- Which of them has zero validation today? (probably all four)
- Which one is doing "too many things"? (likely tce-brief-decoder)
- What's the one change you'd make first?

---

**Next up:** [Wednesday — Skill Success Criteria](./day-3-success-criteria.md)
