# Week 3, Monday — XML Tags and Structural Clarity

**Time:** ~1 hour
**Goal:** Use XML tags to make your prompts readable, parseable, and consistent.
**Primary source:** [Claude Prompting Best Practices](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices)

---

## Tutor Prompt — Paste This Into Claude to Start

> You are my training tutor for **Week 3, Day 1: XML Tags and Structural Clarity**. I learn best verbally — treat this like a tutoring session, not a lecture.
>
> First, read this full lesson file: `claude-training/week-3-prompting/day-1-xml-tags.md`. Then ask me: how did Week 2 land? Do I have any prompts I already suspect are messy and would benefit from structure?
>
> Then:
> 1. Teach me how XML tags work and why Claude reads structure better than prose. Show me before/after examples. Check understanding.
> 2. Help me pick **one existing prompt** from my skills (tce-brief-decoder, personalized-outreach, or a research workflow I use). Open it together.
> 3. Rewrite it with XML tags — `<task>`, `<brief>`, `<archive>`, `<voice_guide>`, `<output_format>`, whatever fits. Walk through each tag choice.
> 4. **Run both versions on the same real input.** Compare output. Is the new version more consistent? Easier to parse later?
> 5. Log the before/after and observations in `claude-training/claude-learnings.md` under today's date. If it's a clear win, commit the restructured prompt into the skill.

---

## The Big Idea

Claude reads **structure better than prose.** When you dump everything into one wall of text, Claude has to guess at hierarchy — what's the brief, what's the instructions, what's the constraint, what's the data. Guessing burns attention and introduces inconsistency.

XML tags fix this. They tell Claude exactly what each section is, what it's for, and how to treat it.

---

## The Basic Pattern

Instead of this:

> Here's the client brief. It's for Guggenheim and the industry is hypersonics. We need five expert profiles with backgrounds in supply chain and semiconductor fabrication. Budget is $75k. Make the profiles sound like TCE voice. Here's our past archive for reference...

Do this:

```xml
<task>
Identify 5 expert profiles that match the brief.
</task>

<brief>
Client: Guggenheim
Industry: Hypersonics
Specialties needed: supply chain, semiconductor fabrication
Budget: $75k
</brief>

<voice_guide>
TCE voice — executive recruiting tone, specific beats generic, no content-marketer fluff.
</voice_guide>

<archive>
[past project reference here]
</archive>

<output_format>
Markdown. One section per expert. Include: name placeholder, specialty match, past role, sourcing angle.
</output_format>
```

Same information. Claude now knows exactly what each piece is.

---

## Why This Works

1. **Hierarchy is explicit.** Claude doesn't have to guess what's a task, what's input, what's constraint.
2. **Sections are separable.** Claude can re-read a section when it needs to.
3. **Consistency across runs.** Structured prompts produce structured outputs. Variance drops.
4. **Debugging is easier.** When output is wrong, you can point to the tag that was ambiguous.

---

## Standard Tag Vocabulary

- `<task>` — what Claude should do
- `<instructions>` — step-by-step process
- `<context>` — background information
- `<brief>` / `<document>` / `<input>` — the primary content to work on
- `<example>` — a demonstrated input/output pair
- `<constraint>` / `<rule>` — a hard limit
- `<output_format>` — what the response should look like
- `<voice_guide>` / `<style>` — tone and register

---

## Where XML Tags Belong in Your TCE Skills

### `tce-brief-decoder`
- Wrap the incoming brief in `<brief>`
- Wrap the project archive reference in `<archive>`
- Wrap the output schema in `<output_format>`

### `personalized-outreach`
- Wrap each contact in `<contact>` with nested fields
- Wrap the brief context in `<brief_context>`
- Wrap voice guide in `<voice_guide>`

### `instantly-csv-processor`
- Wrap the raw CSV as `<input_csv>`
- Wrap validation rules in `<validation>`

### `zerobounce-pipeline`
- Wrap the email list in `<emails>`
- Wrap score thresholds in `<thresholds>`

---

## When NOT to Use XML Tags

- Short, simple prompts where structure is obvious
- Casual conversation
- When you only have one section

**Rule of thumb:** use tags when there are **2+ distinct categories of information** in the prompt.

---

## Homework

Pick one prompt you use regularly. Rewrite it with XML tags. Run both versions on the same input. Compare: is the output more consistent? Does it follow the structure better?

Write the before/after and observation in [claude-learnings.md](../claude-learnings.md).

---

## What You Should Be Able to Answer by End of Day

- Why does Claude read structure better than prose? → Tags give explicit hierarchy; prose forces Claude to infer it.
- When should I use XML tags? → Whenever there are 2+ distinct categories of info in the prompt.
- What's the downside? → A little verbosity. Negligible compared to the consistency gain.

---

**Next up:** [Tuesday — Longform Data at the Top](./day-2-longform-data.md)
