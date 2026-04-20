# Week 2, Friday — Testing Against Baseline and Iteration

**Time:** ~1 hour
**Goal:** Prove that your restructured skill actually improves output vs. the old version, and set up the versioning rhythm.
**Primary source:** [Complete Guide to Building Skills for Claude (PDF)](https://resources.anthropic.com/hubfs/The-Complete-Guide-to-Building-Skill-for-Claude.pdf)

---

## Tutor Prompt — Paste This Into Claude to Start

> You are my training tutor for **Week 2, Day 5: Testing Against Baseline and Iteration**. I learn best verbally — treat this like a tutoring session, not a lecture. **Today is a working session — we're running actual tests on real data.**
>
> First, read this full lesson file: `claude-training/week-2-skills/day-5-baseline-and-iteration.md`. Then ask me: do I have the restructured skill ready to test? Do I have a real input (a real brief, a real contact list, a real CSV) that represents typical use?
>
> Then:
> 1. Briefly teach me the 3-run baseline test and the 4 scoring dimensions (quality, consistency, speed, token cost). Don't over-explain — I need to run the test.
> 2. Walk me through **actually running the three runs** on the same input: bare Claude with no skill, old skill, restructured new skill. Capture output for each.
> 3. Score all three against the success criteria I wrote on Wednesday. Fill in the comparison table in `claude-training/claude-learnings.md`.
> 4. Help me decide: is the new skill actually better? If yes, help me version it (v1 → v2) and commit. If no, help me spot the regression and iterate.
> 5. Close by zooming out: Week 2 is done. What's my backlog for the other three skills? When will I do each?

---

## The Big Idea

Anthropic's explicit guidance: **"prove the skill improves results versus baseline."**

Building a skill feels productive. Proving a skill is **better than the baseline** is what separates operational leverage from busy work. Today you run the comparison.

---

## The Three-Run Baseline Test

1. **Run 1 — No skill.** Bare Claude, no skill invoked, no reference docs. Just the prompt.
2. **Run 2 — Old skill.** Your current production version, as-is.
3. **Run 3 — New skill.** The restructured three-tier version with validation gates.

Same input. Three different output sets.

---

## What You're Measuring

- **Output quality** — does it meet the success criteria?
- **Consistency** — run 2–3 times, does output vary wildly or stay stable?
- **Speed** — how long from prompt to usable output?
- **Token cost** — rough order of magnitude per invocation

---

## Comparison Table Template

```
| Dimension     | No skill | Old skill | New skill |
| ------------- | -------- | --------- | --------- |
| Quality       | ...      | ...       | ...       |
| Consistency   | ...      | ...       | ...       |
| Speed         | ...      | ...       | ...       |
| Token cost    | ...      | ...       | ...       |
```

If the new skill isn't clearly better — it isn't better yet. Iterate.

---

## Versioning

When you promote a restructured skill into production:

- Save the old version as `tce-brief-decoder-v1/` (or tag it in version control)
- Call the restructured version `tce-brief-decoder-v2/`
- Keep your baseline comparison data somewhere retrievable

This sounds like overhead. It's actually what lets you evolve skills without breaking them.

---

## The Iteration Rhythm

1. **Build** — initial version
2. **Measure** — baseline test
3. **Use in production** for 2–4 weeks
4. **Revisit** — what's drifting? What edge case broke?
5. **Update** — usually minor, occasionally a v-bump
6. **Re-measure** against the last baseline

Once a month you'll review one skill. Over a year, each skill gets the deep revision treatment three or four times.

---

## End of Week 2 — Where You Are

- ✓ Three-tier architecture understood
- ✓ All four existing skills audited
- ✓ Success criteria defined per skill
- ✓ Validation gates designed
- ✓ One skill restructured and tested against baseline

---

## What You Should Be Able to Answer by End of Day

- How do I know a skill is actually working? → Three-run baseline test, scored on quality, consistency, speed, cost.
- What do I do when the restructured version isn't better? → Find the regression, iterate, don't ship.
- How often do I revisit skills? → Monthly review, deeper revision 3–4x per year per skill.

---

**Next up:** [Week 3, Monday — XML Tags and Structural Clarity](../week-3-prompting/day-1-xml-tags.md)
