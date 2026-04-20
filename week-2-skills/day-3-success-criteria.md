# Week 2, Wednesday — Skill Success Criteria

**Time:** ~1 hour
**Goal:** Define what "success" actually looks like for each of your skills, and embed domain knowledge in references.
**Primary source:** [Complete Guide to Building Skills for Claude (PDF)](https://resources.anthropic.com/hubfs/The-Complete-Guide-to-Building-Skill-for-Claude.pdf)

---

## Tutor Prompt — Paste This Into Claude to Start

> You are my training tutor for **Week 2, Day 3: Skill Success Criteria**. I learn best verbally — treat this like a tutoring session, not a lecture.
>
> First, read this full lesson file: `claude-training/week-2-skills/day-3-success-criteria.md`. Then ask me: did the audit land yesterday? Which skill did I pick to restructure first?
>
> Then:
> 1. Teach me why vague criteria ("feels useful") don't hold up. Use the format from the lesson: what it produces, how fast, what failure looks like.
> 2. Have me write **measurable success criteria for each of my four skills** — tce-brief-decoder, instantly-csv-processor, zerobounce-pipeline, personalized-outreach. Work through them one at a time, pushing back on any vague language.
> 3. For the skill I picked yesterday to restructure first, go deeper: which domain knowledge should move to `references/`? What should come out of SKILL.md?
> 4. Write all four skills' success criteria in `claude-training/claude-learnings.md` with today's date. This is the baseline I'll measure against on Friday.
> 5. Close by previewing tomorrow — we design the validation gate for the restructured skill.

---

## The Big Idea

A skill that feels useful and a skill that **measurably improves output** are different things. If you can't define success, you can't tell when the skill is failing, drifting, or being outgrown.

Today: **for each skill, you define measurable success criteria and start moving domain knowledge into references.**

---

## How to Write Success Criteria

Bad: "Produces a good brief decode."
Good: "Correctly identifies (1) client industry, (2) budget range, (3) timeline, (4) minimum 3 expertise categories, and (5) flags any prior TCE project overlap — in under 2 minutes."

Format:
1. **What specifically** the skill should produce (checklist, not adjectives)
2. **How fast** it should produce it
3. **What failure looks like** — so you can recognize it

---

## Success Criteria for Each Skill

### `tce-brief-decoder`

> "Given an Inex One project brief, correctly identifies:
> - Client industry and sub-sector
> - Project budget range (or flags 'not disclosed')
> - Timeline and urgency
> - At least 3 distinct expertise categories needed
> - Any overlap with past TCE projects (or explicit 'no overlap found')
> - At least 2 LinkedIn boolean search strings
> All within 2 minutes. Failure mode: generic expertise categories ('supply chain expert' instead of 'semiconductor fab capacity planner')."

### `instantly-csv-processor`

> "Given a lead-list CSV with multi-column emails, produces an Instantly-ready CSV where:
> - Every row has exactly one email
> - Every email is unique within the output
> - Every email passes syntactic format validation
> - No data loss from source columns (company, title, etc. preserved on exploded rows)
> In under 30 seconds per 1,000 rows. Failure mode: duplicate rows, malformed emails, or dropped metadata."

### `zerobounce-pipeline`

> "Given a list of email addresses, produces a verified-contacts CSV where:
> - Every email has a ZeroBounce result attached
> - Score distribution is documented
> - Deliverable emails are clearly separated from risky/invalid
> - Rate-limit and cost tracking logged
> Failure mode: skipped emails, silent failures, or score distribution outside expected norms (e.g., 100% valid is suspicious)."

### `personalized-outreach`

> "Given verified contacts + decoded brief, produces an Instantly-ready CSV where:
> - Every row has `GeneratedEmail` and `SubjectLine` fields
> - No two emails are identical
> - Voice matches TCE's executive-recruiting tone (not 'content marketer')
> - Each email references something specific about the recipient (role, company, background)
> - Max 25 contacts per batch to preserve quality
> Failure mode: generic openers, template-feeling copy, or duplicate bodies."

---

## Building Domain Knowledge Into `references/`

This is where your TCE-specific intelligence goes **without** bloating the core skill.

### For `tce-brief-decoder`
- `references/tce-project-archive-index.md` — past clients by sector
- `references/expertise-taxonomy.md` — how TCE categorizes expertise
- `references/sector-knowledge.md` — notes on aerospace, defense, supply chain, semiconductors

### For `instantly-csv-processor`
- `references/email-validation-rules.md` — exact format rules
- `references/deduplication-logic.md` — how duplicates are detected and collapsed
- `references/instantly-format-spec.md` — what the Instantly API expects

### For `zerobounce-pipeline`
- `references/zerobounce-api.md` — API response schema
- `references/score-thresholds.md` — TCE's definition of "safe to send"
- `references/cost-tracking.md` — per-email cost and batch limits

### For `personalized-outreach`
- `references/tce-voice.md` — tone guide
- `references/outreach-templates.md` — structural examples
- `references/sector-angles.md` — what hooks work for which kinds of experts

---

## Homework

For each of your four skills, **write down the success criteria in [claude-learnings.md](../claude-learnings.md)** using the format above.

Then pick **one skill** and:
1. List what needs to move into `references/`
2. List what needs to come out of SKILL.md
3. Note what validation step you'll add

Don't implement yet. Tomorrow you'll lock down the validation approach.

---

## What You Should Be Able to Answer by End of Day

- For each skill, what does "working" look like in measurable terms?
- What domain knowledge is currently bloating my SKILL.md that should live in `references/`?
- Which skill am I starting with first?

---

**Next up:** [Thursday — Quality Checklists and Validation Gates](./day-4-validation-gates.md)
