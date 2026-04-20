# Week 3, Wednesday — Ground Responses in Quotes

**Time:** ~1 hour
**Goal:** Force Claude to point at evidence before drawing conclusions. Kills hallucination and creates traceable output.
**Primary source:** [Claude Prompting Best Practices](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices)

---

## Tutor Prompt — Paste This Into Claude to Start

> You are my training tutor for **Week 3, Day 3: Ground Responses in Quotes**. I learn best verbally — treat this like a tutoring session, not a lecture.
>
> First, read this full lesson file: `claude-training/week-3-prompting/day-3-grounding-in-quotes.md`. Then ask me: where in my work have I caught Claude saying something that sounded right but turned out to be made up?
>
> Then:
> 1. Teach me the quote-then-conclude pattern and the "say so if you can't" clause. Walk through how each kills hallucination. Check understanding.
> 2. Help me pick **one skill or workflow** where Claude draws conclusions from documents — likely `tce-brief-decoder`, market research, or Guggenheim-style analysis work.
> 3. Add the grounding pattern to that skill's prompt. Be explicit: every conclusion must quote a source passage; if evidence doesn't exist, say so instead of inventing.
> 4. **Test it on a real document.** Does Claude now catch itself on any unsupported claims?
> 5. Log the before/after and the catch-rate observation in `claude-training/claude-learnings.md` with today's date.

---

## The Big Idea

When Claude is working through a long document and needs to draw a conclusion, ask it to **quote the relevant passages first, then explain.**

This does three things:
1. **Kills hallucination.** Claude can't cite a quote that isn't there.
2. **Creates traceable sourcing.** Your output has built-in citations you can verify.
3. **Improves the reasoning itself.** Claude's conclusions, when grounded in specific quotes, get sharper.

---

## The Pattern

### Without grounding
> "What are the three biggest supply chain risks in this document?"

### With grounding
```xml
<task>
Find the three biggest supply chain risks in the document above.

For each risk:
1. Quote the specific passage(s) that demonstrate it.
2. Explain why it's a risk.
3. Rate severity (low/medium/high) with reasoning.

If you can't find three supported risks in the document, say so
and list only the ones you can support.
</task>
```

---

## The "Say So If You Can't" Clause

> "If you can't find three supported risks in the document, say so and list only the ones you can support."

Without this, Claude may invent to fill the quota. With it, Claude is explicitly allowed to say "only two actually appear in the document." That's the anti-hallucination move.

Use this clause **anytime** you're asking for a specific count of things.

---

## Applying This to Your Work

### `tce-brief-decoder` — past project overlap
**After:**
> "Compare the brief against the project archive. For each potential overlap, quote the brief passage and the archive entry that match. Rate the overlap as direct, adjacent, or weak. If no overlap exists, state 'no overlaps found against [N] compared projects.'"

### `personalized-outreach` — recipient-specific angles
**After:**
> "For each contact, the email must reference one fact cited from the provided background. Quote the source fact in a comment at the top of each email draft. If no usable fact exists, flag the contact for manual review — do not fabricate."

---

## When to Use This Pattern

- Any time output must be traceable
- Any time Claude is drawing conclusions from long documents
- Research work (always)
- When generating counts of things ("find N examples of Y")

---

## Homework

Pick one existing skill or workflow where Claude draws conclusions from input documents. Add the grounding-in-quotes pattern.

Test on real data. Questions for [claude-learnings.md](../claude-learnings.md):
- Did Claude catch itself on any claims it couldn't quote?
- Does the output feel more defensible to a client?

---

## What You Should Be Able to Answer by End of Day

- Why does quoting reduce hallucination? → Claude can't quote what isn't there; forced to admit gaps instead of invent.
- What's the "say so if you can't" clause? → Explicit permission to report fewer findings, removing pressure to fabricate.
- Where does this matter most? → Research, client analysis, anywhere a wrong claim has a real cost.

---

**Next up:** [Thursday — Role Setting in System Prompts](./day-4-role-setting.md)
