# Week 3, Tuesday — Longform Data at the Top

**Time:** ~1 hour
**Goal:** Stop burying your data under your instructions. Claude reads the top more carefully than the bottom.
**Primary source:** [Claude Prompting Best Practices](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices)

---

## Tutor Prompt — Paste This Into Claude to Start

> You are my training tutor for **Week 3, Day 2: Longform Data at the Top**. I learn best verbally — treat this like a tutoring session, not a lecture.
>
> First, read this full lesson file: `claude-training/week-3-prompting/day-2-longform-data.md`. Then ask me: what's the most data-heavy prompt I run — brief decoding, contact-list processing, market research, something else?
>
> Then:
> 1. Teach me why data-first beats instructions-first for long inputs. Walk through the attention mechanics. Check understanding — this is counterintuitive.
> 2. Help me pick **one real long-input prompt** I use. Confirm the data volume is >1,000 tokens.
> 3. Rewrite the prompt data-first, combining with the XML tags from yesterday. Data at top → context in the middle → task and output format at the bottom.
> 4. **Run both versions on the same real input.** Does the new output engage with specific details more?
> 5. Log the before/after and observations in `claude-training/claude-learnings.md` with today's date.

---

## The Counterintuitive Rule

When you're feeding Claude a large piece of content — a 15-page client brief, a 500-row expert list, a document you want analyzed — **put the data first, before your instructions.**

---

## Why

- When instructions come **first**, Claude optimizes for the instructions and tends to skim the data
- When data comes **first**, Claude reads it carefully knowing instructions are coming
- Claude's attention is slightly weighted toward the **top and bottom** of the context window

Optimal order for heavy-data prompts:
1. **Top:** the data (longform, high-volume)
2. **Middle:** context, references, examples
3. **Bottom:** instructions, task, output format

---

## Practical Examples

### Wrong (instructions first)
```
I need you to find the three biggest supply chain risks in the document below.
Here's the document:
[15,000-word document]
```

### Right (data first)
```xml
<document>
[15,000-word document]
</document>

<task>
Find the three biggest supply chain risks in the document above.
For each risk, quote the specific passage that demonstrates it.
</task>
```

---

## Applying This to Your Work

### `tce-brief-decoder`
**After:**
```xml
<brief>
[15-page brief at top]
</brief>

<task>
Decode into fields: industry, budget, timeline, expertise categories, past project overlap.
</task>
```

### `personalized-outreach`
Put the verified contacts CSV and decoded brief at the top. Put the instructions at the bottom.

---

## The Volume Threshold

- **Under ~1,000 tokens:** order barely matters
- **1,000–10,000 tokens:** data-first starts showing improvement
- **10,000+ tokens:** data-first is a large, consistent win

Your brief decoder, market maps, and bulk outreach all live in the 5,000–50,000 token range. Data-first is a win for all of them.

---

## Combined With Yesterday's XML Tags

```xml
<brief>[large document]</brief>
<archive_references>[relevant context]</archive_references>
<voice_guide>[tone and register]</voice_guide>
<task>[what you want Claude to do]</task>
<output_format>[how the result should look]</output_format>
```

---

## Homework

Take one of your longer prompts. Rewrite it data-first. Run both versions on the same input.

Observation questions for [claude-learnings.md](../claude-learnings.md):
- Did the output engage with specific details from the document more?
- Did it feel less generic?
- Did it surface insights that the old version missed?

---

## What You Should Be Able to Answer by End of Day

- Why put data at the top? → Claude reads the top more carefully; instructions at the top cause skimming of the data.
- When does this start to matter? → ~1,000+ tokens of data.
- How do I combine this with XML tags? → Tag every section, heavy-content tags at top, task tags at bottom.

---

**Next up:** [Wednesday — Ground Responses in Quotes](./day-3-grounding-in-quotes.md)
