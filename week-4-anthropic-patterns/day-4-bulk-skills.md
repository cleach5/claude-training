# Week 4, Thursday — Skills for Bulk Operations

**Time:** ~1 hour
**Goal:** Scale Claude Code from one-at-a-time to many-at-once for the parts of your work that are inherently volume-heavy.
**Primary source:** How Anthropic Teams Use Claude Code (PDF)

---

## Tutor Prompt — Paste This Into Claude to Start

> You are my training tutor for **Week 4, Day 4: Skills for Bulk Operations**. I learn best verbally — treat this like a tutoring session, not a lecture.
>
> First, read this full lesson file: `claude-training/week-4-anthropic-patterns/day-4-bulk-skills.md`. Then ask me: what do I currently process **one at a time** that is inherently a batch operation?
>
> Then:
> 1. Teach me the two flavors of bulk (data bulk and code bulk) and the 3 failure modes (silent per-record failures, resource exhaustion mid-batch, drift across parallel branches). Check understanding.
> 2. Have me pick **one workflow** that should be bulk but currently isn't (or isn't fully).
> 3. **Design the bulk version together**: batch size, parallel-vs-serial within the batch, checkpointing strategy, whole-batch validation rules, what "processed N" summary looks like.
> 4. If the pick is already bulk, audit it for the 3 failure modes instead.
> 5. Log the bulk design or audit findings in `claude-training/claude-learnings.md` with today's date.
> 6. Close: is this something I build next week, or a backlog item for next month's first-Friday audit?

---

## The Big Idea

Claude Code has first-class support for **bulk operations** — refactoring at scale, running the same pattern across many files, processing hundreds of records in one pass.

Right now, your TCE work has inherently bulk operations you're probably handling serially:
- ZeroBounce verification across hundreds of emails
- Outreach personalization across 25-contact batches
- Schema refactors that touch many ExpertOps views
- Page-by-page updates across tce-website

---

## Two Flavors of Bulk

### 1. Data bulk — many records, same operation
Examples: 500 emails through ZeroBounce. 25 personalized outreach emails.

**Pattern:** SKILL.md defines the operation, input is a batch, skill processes in parallel where safe, validation checks the batch as a whole.

### 2. Code bulk — many files, same pattern
Examples: renaming a function across all `tce-website` components.

**Pattern:** Claude Code runs across files, a slash command defines the operation, git worktrees isolate the work, review catches drift.

---

## Upgrade Opportunities for Your Skills

### `zerobounce-pipeline`
- Explicit batch size with rate-limit awareness
- Parallel calls within the API's limit
- Mid-batch checkpoint file (so if it fails at 400/500, restart from 400)
- Run-level summary: "500 submitted, 487 valid, 13 risky, average score 0.92"

### `personalized-outreach`
- Per-contact grounding: each email must cite one fact from provided background
- Cross-batch uniqueness check: no two emails share sentences/structure
- Whole-batch voice review

### `instantly-csv-processor`
- Parallel processing of independent rows
- Whole-file validation (row count reconciles, no dupes, no dropped metadata)

---

## When Bulk Goes Wrong

### 1. Silent per-record failures
In a 500-row batch, if 13 rows fail and the skill returns "processed 500," you've shipped garbage. **Validation must reconcile row counts explicitly.**

### 2. Resource exhaustion mid-batch
API rate limits. Token limits. Timeout. **Build checkpointing for any batch over ~100 records.**

### 3. Drift across parallel branches
Three sub-agents refactoring concurrently with no shared convention source = three different interpretations. **Lead agent must own the convention doc.**

---

## When NOT to Bulk

- One-off tasks
- Small batches (<10) of heterogeneous work
- High-stakes destructive writes at scale — stay serial with human review per record

---

## The Mental Shift

One-at-a-time: "I'll process this, then the next one, then the next one."

Bulk: "I'll define the operation once and apply it across the batch, with validation on the whole batch at the end."

**Engineering scales. Doing doesn't.**

---

## Homework

Pick one thing in your TCE workflow that you do serially and should probably be bulk. Write it up in [claude-learnings.md](../claude-learnings.md): what's the operation, current serial pattern, what the bulk version would look like, checkpointing strategy, batch validation.

---

## What You Should Be Able to Answer by End of Day

- When does bulk beat serial? → Batch size >10, uniform operation, low-to-medium stakes per record.
- What's the biggest failure mode of bulk? → Silent per-record failures hidden in "processed 500" summaries.
- Why does bulk need checkpointing? → Rate limits and timeouts will bite on any batch over ~100.

---

**Next up:** [Friday — The Full Picture and Building Intuition](./day-5-intuition-over-rules.md)
