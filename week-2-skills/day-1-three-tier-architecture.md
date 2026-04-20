# Week 2, Monday — The Three-Tier Skill Architecture

**Time:** ~1 hour
**Goal:** Understand the structure Anthropic recommends for Skills, and why your existing ones probably don't follow it.
**Primary source:** [Complete Guide to Building Skills for Claude (PDF)](https://resources.anthropic.com/hubfs/The-Complete-Guide-to-Building-Skill-for-Claude.pdf)

---

## Tutor Prompt — Paste This Into Claude to Start

> You are my training tutor for **Week 2, Day 1: The Three-Tier Skill Architecture**. I learn best verbally — treat this like a tutoring session, not a lecture.
>
> First, read this full lesson file: `claude-training/week-2-skills/day-1-three-tier-architecture.md`. Then ask me: did I finish Week 1? Anything I'm still chewing on? Have I looked at any of my existing TCE skills' SKILL.md files recently?
>
> Then:
> 1. Teach me the three-tier architecture conversationally — SKILL.md (Tier 1), references/ (Tier 2), validation (Tier 3). Pause to check understanding. Use my four existing skills as running examples: tce-brief-decoder, instantly-csv-processor, zerobounce-pipeline, personalized-outreach.
> 2. Have me pick **one of my four skills** and open its SKILL.md. Walk through it together, section by section, identifying what's in each tier (or misplaced).
> 3. Don't restructure anything yet — today is diagnosis only. Tomorrow I do the full audit of all four skills.
> 4. Write the observations from today's walkthrough in `claude-training/claude-learnings.md` with today's date.

---

## The Setup

You've already built at least four skills:
- `tce-brief-decoder`
- `instantly-csv-processor`
- `zerobounce-pipeline`
- `personalized-outreach`

You built them **before** reading the official playbook. This week you're going to audit them against the architecture Anthropic actually recommends. You'll almost certainly find tightening opportunities.

Today is just the **structure.** Tuesday you start the audit.

---

## Why Structure Matters

Skills get loaded into Claude's context every time they trigger. **A bloated skill burns context every time it fires.** That means:

- Slower responses
- Less room for the actual data the skill is supposed to operate on
- Quality degradation over a long session

The three-tier architecture is Anthropic's answer: **keep the core prompt focused, offload detail to references, enforce quality at the end.**

---

## The Three Tiers

### Tier 1 — `SKILL.md` (The Core)

This is the frontmatter file + the core instructions Claude reads every time the skill triggers.

**It should contain:**
- Clear trigger description (when should this fire?)
- The minimal instructions needed to run the skill
- Pointers to reference docs (not the docs themselves)
- The expected output shape

**It should NOT contain:**
- Lots of examples (those live in `references/`)
- Domain knowledge dumps (same)
- Edge-case documentation (same)

**Target length:** short. Focused. A page or so, not a novel.

---

### Tier 2 — `references/` (Detail On Demand)

A folder of supporting documentation Claude reads **only when it needs to**, not on every invocation.

**This is where the heavy material lives:**
- Detailed examples
- Templates
- Domain knowledge (TCE-specific sector expertise, client archives)
- API response schemas
- Edge-case handling
- Quality rubrics

For `tce-brief-decoder`, your references folder might hold:
- `references/tce-project-archive-index.md` — past clients by sector
- `references/boolean-string-patterns.md` — LinkedIn search templates
- `references/brief-anatomy.md` — what a typical Inex One brief looks like

SKILL.md points to these: *"When the brief mentions aerospace, see references/tce-project-archive-index.md#aerospace for overlap."*

Claude only loads what it needs, when it needs it. **Context stays lean.**

---

### Tier 3 — Validation (Quality Gates)

Before Claude returns output, the skill has **explicit validation steps** Claude runs against the result:

- Did it actually find relevant past projects, or is it claiming it did?
- Is every email in the output unique and properly formatted?
- Does the outreach email have a real subject line, or is it placeholder?
- Does the score distribution look reasonable, or is every score suspiciously identical?

These aren't tests you run separately — they're **instructions in SKILL.md** like:
> "Before returning output, verify that every row has a non-empty `GeneratedEmail` field and that no two rows share the same email address. If either check fails, regenerate the missing rows."

Most people skip this tier. It's why mediocre skills look fine until they don't.

---

## The Common Anti-Pattern

Most homemade skills (yours included, probably) put **everything in one big prompt file:**
- Trigger conditions
- Instructions
- Five examples
- Three templates
- Domain knowledge
- Quality rubric

That **fills context instantly.** Every time the skill triggers, all of that loads — even parts Claude doesn't need for this particular invocation.

The three-tier model **separates concerns:**
- Tier 1: what Claude always needs (minimal)
- Tier 2: what Claude sometimes needs (on-demand)
- Tier 3: how Claude checks its own work (gating)

---

## Example — How This Applies to `tce-brief-decoder`

Your current version likely does:
- Project brief parsing
- OneDrive cross-reference logic
- Past TCE project overlap detection
- Boolean string generation
- Expertise category identification

All in one prompt.

Restructured three-tier:

**Tier 1 (SKILL.md):**
- Trigger: "user uploads or references an Inex One project brief"
- Instructions: "(1) Parse the brief into structured fields. (2) Cross-reference against TCE project archive — see `references/project-archive-method.md`. (3) Generate expertise categories and boolean strings. (4) Validate output per `references/quality-checklist.md`."
- Output shape: defined JSON/markdown schema

**Tier 2 (references/):**
- `references/brief-anatomy.md` — what fields to expect
- `references/tce-project-archive-index.md` — past projects by sector/client
- `references/boolean-string-patterns.md` — LinkedIn templates
- `references/expertise-taxonomy.md` — TCE's internal categorization

**Tier 3 (validation, baked into SKILL.md):**
- Confirm at least one project overlap was checked (even if none found)
- Confirm every boolean string is syntactically valid
- Confirm output schema matches spec before returning

Same skill. Cleaner. Faster. Context-lean.

---

## Homework

Don't audit anything yet. Just **read one SKILL.md** from your existing skills. Pick any of the four.

Ask yourself:
- How long is it?
- Is there anything in here that would be better off in a `references/` file?
- Is there any validation at the end, or does the skill just return whatever it generated?

Write your observations in [claude-learnings.md](../claude-learnings.md). Tomorrow you'll formally audit.

---

## What You Should Be Able to Answer by End of Day

- What goes in Tier 1 vs. Tier 2? → Tier 1 = always needed, minimal. Tier 2 = sometimes needed, on-demand.
- Why does skill bloat matter? → Every trigger loads the whole SKILL.md into context; bloat taxes every invocation.
- What does validation look like? → Explicit "check X before returning" steps baked into the skill instructions.

---

**Next up:** [Tuesday — Audit Your Existing TCE Skills](./day-2-audit-existing-skills.md)
