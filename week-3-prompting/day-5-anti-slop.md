# Week 3, Friday — Avoiding Generic and "AI Slop" Aesthetic

**Time:** ~1 hour
**Goal:** Keep your content distinctive. Embed voice explicitly so Claude doesn't default to the middle of the road.
**Primary source:** [Claude Prompting Best Practices](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices)

---

## Tutor Prompt — Paste This Into Claude to Start

> You are my training tutor for **Week 3, Day 5: Avoiding Generic and "AI Slop" Aesthetic**. I learn best verbally — treat this like a tutoring session, not a lecture. **This is a working session — we're actually building the TCE voice guide today.**
>
> First, read this full lesson file: `claude-training/week-3-prompting/day-5-anti-slop.md`. Then ask me: when I read AI-generated emails or drafts, what phrases make me cringe? What do I always edit out?
>
> Then:
> 1. Teach me briefly why Claude defaults to slop and why anti-patterns beat positive rules.
> 2. **Draft `references/tce-voice.md` together** — the full voice guide with: voice description, positive rules, anti-pattern list (banned openers, banned phrases, banned words), good example, bad example.
> 3. **Update `personalized-outreach`** SKILL.md to reference tce-voice.md. Add length constraints (max words) and the "specific grounded fact required" rule.
> 4. **Generate 5 real outreach emails** on a real batch. Read them out loud. Are they TCE voice, or AI slop? Iterate.
> 5. Commit the voice guide and the updated skill. Log the banned-phrase list in `claude-training/claude-learnings.md`.
> 6. Close by zooming out: Week 3 done. What's the one prompting move that changed my output the most?

---

## The Big Idea

Without specific guidance, Claude defaults to generic patterns — **safe, middle-of-the-road, forgettable.** This is what people mean by "AI slop":

- "I hope this email finds you well"
- "I wanted to reach out to discuss an exciting opportunity"
- "In today's rapidly evolving landscape..."
- "It's worth noting that..."
- Em-dash overuse
- Polished, safe, hollow

Anthropic **explicitly warns** about this. If you don't specify voice, Claude picks the safest possible one.

---

## The Fix — Explicit Voice Embedding

```xml
<voice_guide>
Voice: [who you sound like]
Rules:
- [positive rule 1]
- [positive rule 2]

Anti-patterns — never use:
- [banned opener 1]
- [banned phrase 2]

Example (good): "[short example that demonstrates the voice]"
Example (bad): "[short example of the AI slop version]"
</voice_guide>
```

---

## TCE Voice Guide (starting draft)

```xml
<voice_guide>
Voice: a founder who's done the work — not a content marketer.

Rules:
- Specific beats generic. Name the company, the specialty, the angle.
- Direct beats hedged. No "it's worth noting" or "I wanted to reach out."
- Short beats long. Trim ruthlessly.
- Opinions beat observations. If there's a recommendation, make it.
- Industry-fluent language, not consultant-speak.

Anti-patterns — never use:
- "I hope this email finds you well"
- "I wanted to reach out"
- "I came across your profile"
- "Exciting opportunity"
- "In today's [X] landscape"
- "Leverage" as a verb
- "Unlock" as a verb
- Generic adjectives: "impressive," "dynamic," "innovative," "world-class"
- Em-dashes where a period would do
- "Looking forward to hearing from you"

Example (good):
"Saw your work on the hypersonics capacity push at Raytheon — we're
sourcing for a Guggenheim engagement looking specifically at the
supplier-qualification bottleneck. 30-minute paid call worth your time?"

Example (bad):
"I hope this email finds you well. I came across your impressive
background in the hypersonics space and wanted to reach out about
an exciting opportunity to leverage your expertise..."
</voice_guide>
```

---

## Why Anti-Patterns Matter More Than Positive Rules

Positive rules ("be specific," "be direct") are vague — Claude can technically follow them while still sounding generic.

**Anti-patterns are concrete.** "Never use 'leverage' as a verb" is unambiguous. Claude complies.

Give 10 anti-patterns and 3 positive rules. That's a better voice guide than 10 positive rules.

---

## The Length Move

AI slop is **long.** Add length constraints:
- `<constraint>max 120 words</constraint>` on outreach emails
- `<constraint>no more than 3 sentences per section</constraint>` on briefs
- `<constraint>trim: if removing a sentence doesn't lose information, remove it</constraint>`

---

## End of Week 3 — Where You Are

- ✓ XML tags for structural clarity
- ✓ Data-first ordering for long inputs
- ✓ Grounding-in-quotes for defensible output
- ✓ Role framing for register and priority
- ✓ Explicit voice with anti-patterns for TCE-grade output

Every one of your skills and every research prompt is now substantially better than it was Monday.

---

## Homework

1. **Draft the TCE voice guide** as `references/tce-voice.md`. Adjust to your actual voice.
2. **Apply it to `personalized-outreach`.** Generate 5 emails for a real batch. Read them out loud — do they sound like TCE or like AI? Adjust until they sound like TCE.
3. **Build your banned-phrase list.** Add every phrase you notice yourself editing out of Claude's drafts.

---

## What You Should Be Able to Answer by End of Day

- Why does Claude default to AI slop? → It's the safest register when voice isn't specified.
- What's more effective: positive rules or anti-patterns? → Anti-patterns. Concrete and enforceable.
- What's the one phrase I should kill first? → Pick one from your actual drafts. Ban it explicitly.

---

**Next up:** [Week 4, Monday — MCP Servers Over CLI for Sensitive Data](../week-4-anthropic-patterns/day-1-mcp-over-cli.md)
