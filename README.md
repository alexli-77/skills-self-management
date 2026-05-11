# Skills for Self-Management

[English](README.md) | [中文](README.zh.md)

> A collection of Claude Agent Skills based on Stephen Covey's *The 7 Habits of Highly Effective People*.
> Helps you review your mission statement, long-term plans, and weekly plans with a principle-centered lens — and surface the blind spots.

![License](https://img.shields.io/badge/license-MIT-blue)
![Skills](https://img.shields.io/badge/skills-9-green)
![Language](https://img.shields.io/badge/language-EN%2FZH-blue)
![Version](https://img.shields.io/badge/version-2.1.0-blue)

---

Thanks to [sethmblack/skill-stephen-covey](https://github.com/sethmblack/skill-stephen-covey) for the original inspiration.

---

## What is this?

A set of Claude Agent Skills that decomposes Covey's 7 Habits framework into **9 independent, composable sub-skills**. Think of them as **principle-centered reviewers from different angles** — once you already have a mission statement, long-term plan, or weekly plan, you let Claude play the role of Covey and inspect your planning system for breaks, blind spots, and drift.

> **v2.1.0 update:** All SKILL.md files have been rewritten from a full OCR of *The 7 Habits of Highly Effective People* (20th Anniversary Edition, translated by Gao Xinyong).
> Added `life-center-diagnosis` (based on Appendix I "Possible Centers"), as a precondition to mission-statement work.
> `quadrant-ii-time-management` absorbed Appendix II "Fourth-Generation Time Management" — adds role-based weekly planning and daily templates.
> **P/PC Balance** and the **Maturity Continuum** are now woven through `sharpen-the-saw`, `quadrant-ii`, and `stephen-covey`.
> `stephen-covey` routing changed from "trigger-word → sub-skill" to "**diagnose first (maturity + life center) → then dispatch**".
> Overall tone now closer to the mentor-voice of the original book; each sub-skill ends with a "Put It Into Practice" assignment template.

**This skill set is for you if:**
- You already have a mission statement and 5-year / 1-year / quarterly / weekly plans
- You want to review your planning system on a regular cadence
- You want AI as a *thinking coach*, not a *task manager*

**Not for you if:**
- You expect AI to manage tasks and send reminders (this is not a task manager)
- You've never written a personal plan and want AI to take you from zero (you can use it, but slowly)

---

## Quick start

### Prerequisites

- Claude Desktop or Claude Code (CLI)
- Code Execution permission enabled
- Basic familiarity with Covey's 7 Habits (not required — Claude will fill you in)

### Install

**Desktop (Claude Desktop / Cowork):**

1. Download this repo
2. Zip each sub-folder individually (or only the ones you need)
3. Open Claude Desktop → Customize → Skills → "+" → Upload a skill
4. Upload each ZIP one by one

**CLI (Claude Code):**

```bash
# Clone into your Claude workspace
cd ~/claude_workspace
git clone https://github.com/YOUR_USERNAME/skills-self-management.git

# Or drop it under your project's .claude/skills/
cd your-project
mkdir -p .claude/skills
cp -r path/to/skills-self-management/* .claude/skills/
```

---

## File structure

```
skills-self-management/
├── stephen-covey/                      # Master persona + sub-skill routing (diagnose first, then route)
├── circle-of-influence/                # Habit 1 · Be Proactive
├── life-center-diagnosis/              # Pre-Habit 2 · Life-center diagnosis (new)
├── personal-mission-statement/         # Habit 2 · Begin with the End in Mind
├── quadrant-ii-time-management/        # Habit 3 · Put First Things First (with 4th-gen time mgmt)
├── win-win-agreement/                  # Habit 4 · Think Win-Win (with synergy)
├── seek-first-to-understand/           # Habit 5 · Seek First to Understand
├── emotional-bank-account/             # Habits 4-6 foundation · Trust management
└── sharpen-the-saw/                    # Habit 7 · Sharpen the Saw (with P/PC balance)
```

### What each sub-skill does

| Sub-skill | Habit | Core use |
|-----------|-------|----------|
| **stephen-covey** | Master | Diagnose maturity + life center, then dispatch to a sub-skill |
| **circle-of-influence** | Habit 1 | Pull energy from "Circle of Concern" back to "Circle of Influence"; language diagnosis |
| **life-center-diagnosis** | Pre-Habit 2 | Identify which of the 10 life centers anchor you today, then guide toward principle-centeredness |
| **personal-mission-statement** | Habit 2 | Build / review your mission statement (four needs + legacy visualization) |
| **quadrant-ii-time-management** | Habit 3 | Four generations of time management + role-based weekly plan + daily template |
| **win-win-agreement** | Habit 4 | Six interaction paradigms + five elements of win-win + the synergistic third alternative |
| **seek-first-to-understand** | Habit 5 | Four levels of empathic listening; break the autobiographical-response habit |
| **emotional-bank-account** | Habits 4-6 | Six deposit/withdrawal types; trust diagnosis and repair |
| **sharpen-the-saw** | Habit 7 | Four-dimension P/PC diagnosis; daily private victories |

---

## Core use case: Review your existing planning system

If you already have a full planning system (mission statement → 5-year → 1-year → quarterly → weekly), the highest-leverage use of this skill set is **periodic review**.

### Recommended review cadence

| Frequency | What to review | Duration | Skills called |
|-----------|----------------|----------|---------------|
| **Sunday evening** | This week's plan vs. quarterly plan | 20 min | `quadrant-ii` + `circle-of-influence` |
| **1st of each month** | Month-to-date progress vs. yearly plan | 1 hour | `personal-mission-statement` + `quadrant-ii` |
| **End of each quarter** | Quarterly retro + next quarter plan | 2 hours | Full set |
| **Each December** | 5-year plan adjustment / mission statement update | Half a day | `life-center-diagnosis` + `personal-mission-statement` + `sharpen-the-saw` |

> **v2.1 important change:** For year-end or major life transitions, run `life-center-diagnosis` **first** —
> see what's actually anchoring you right now, *before* rewriting the mission statement. Otherwise you just dress up your current center as a "mission."

---

## Three review modes

### Mode A: Vertical-consistency check

**Use for:** Quarterly / yearly retro

**What it does:** Top-down check whether each layer of planning actually serves the layer above it. Surfaces "zombie tasks" and "missing priorities."

**Prompt template:**

```
You are Stephen Covey. Check the vertical consistency of my planning system:

1. Can every item in my 5-year plan be traced to my mission statement?
2. Can every item in my 1-year plan be traced to the 5-year plan?
3. Can every item in this quarter's plan be traced to the 1-year plan?
4. Can every item in this week's plan be traced to the quarterly plan?

Surface the breaks:
- Zombie tasks: things I'm doing that can't be traced upward
- Missing priorities: things important in the statement that disappear downstream

In Covey's voice, name the problems directly. No softening.
```

---

### Mode B: Quadrant-distribution check

**Use for:** Weekly review

**What it does:** Bucket this week's tasks into Q1-Q4 and detect whether you're trapped in urgency.

**Prompt template:**

```
Use the Q2 framework to inspect my plan for this week:

1. Bucket every task into Q1/Q2/Q3/Q4
2. Calculate time share for each quadrant
3. Diagnose:
   - Is the Q2 share healthy (target 60-70%)?
   - Which Q3 tasks can I refuse or delegate? Give me specific refusal scripts
   - Which Q1 tasks could have been prevented by earlier Q2 investment?
4. Recommend the "big rocks" time blocks I must protect this week

Give me concrete, executable adjustments — Covey's voice.
```

---

### Mode C: Circle-of-influence diagnosis

**Use for:** Quarterly / yearly goal review

**What it does:** Judge whether goals are inside your control. Reframe "Circle of Concern" goals as "Circle of Influence" goals.

**Prompt template:**

```
Use the Circle of Influence model to inspect my [yearly / quarterly] goals.

For each goal:
1. Is this inside my Circle of Influence, or my Circle of Concern?
2. If inside Influence: what's the specific action I control?
3. If inside Concern (depends on others or external conditions):
   - Name the part I actually control
   - Reframe it as an "Influence version"

Example:
- Concern: "Grow product to 100K users"
- Influence: "Ship 2 retention features per month + 3 user interviews per week"
```

---

### Mode D: Maturity + life-center diagnosis (new in v2.1)

**Use for:** Annual review / before major life decisions / when you keep hurting on the same kind of thing

**What it does:** Before rewriting your mission or making a long-term decision, diagnose where you are on dependence → independence → interdependence, *and* which of the 10 life centers anchor you right now.

**Prompt template:**

```
I keep getting hurt / stuck in [describe the situation].
First, use life-center-diagnosis to diagnose my life-center:

1. Where does my "security / guidance / wisdom / power" mostly come from today?
2. Which of the 10 life centers (spouse / family / money / work / wealth / pleasure / friend / enemy / religion / self) do I anchor on?
3. How stable is each of those centers?
4. If I want to migrate toward principle-centeredness, what specifically do I let go of, and what do I build?

After the diagnosis, decide whether to call personal-mission-statement for a statement rewrite.
```

---

## Other use cases

Besides plan review, this skill set also handles:

### Relationship diagnosis

**Trigger:** Tension or eroded trust with a specific person.

```
Use emotional-bank-account to diagnose my relationship with [person]:
- Recent deposits and withdrawals
- Account status
- A concrete deposit prescription (this week / this month)
```

### Communication-impasse breakthrough

**Trigger:** Repeatedly arguing the same topic with someone.

```
[Person] and I keep arguing about [topic].
Use seek-first-to-understand to:
1. Diagnose our listening levels
2. Surface my autobiographical responses
3. Give me specific empathic scripts for next conversation
```

### Burnout recovery plan

**Trigger:** Exhausted but can't stop.

```
I've been [working/studying/building] for [duration]. I feel [specific symptoms].
Use sharpen-the-saw to do a four-dimension assessment and give me a minimum-renewal plan for this week.
```

### Negotiation-structure design

**Trigger:** Preparing for an important conversation with boss / client / partner.

```
I'm about to talk to [person] about [topic].
Use win-win-agreement to:
1. Diagnose both sides' real needs (not just stated positions)
2. Design the five elements of a win-win agreement
3. Draft a "no deal" condition that's actually better than a bad deal
```

---

## Best practices

### 1. Put your planning docs in a Claude Project

Create a Claude Project (e.g., "My Life Management") and add these to its Knowledge:

```
01-mission-statement.md       # Mission statement
02-five-year-plan.md          # 5-year plan
03-yearly-plan-2026.md        # Yearly plan
04-q2-2026-plan.md            # Quarterly plan
05-weekly-plan-current.md     # Current weekly plan
```

That way Claude reads the full picture every review — no re-pasting.

### 2. Call the skill explicitly

Claude will auto-detect triggers, but explicit calls work better:

```
# Better
"Use quadrant-ii-time-management to review this week's plan"

# Works but weaker
"Take a look at my weekly plan"
```

### 3. Accept uncomfortable feedback

Covey's lens punctures self-comfort. Common "sting moments":
- "Your 1-year plan has 12 goals. That's not a plan, it's a wish list."
- "23 things this week, only 2 are Q2. Next week you'll say 'no time for important things' again."
- "Your statement puts 'family' second. Your plan doesn't show it."

**Don't delete these.** This is what you pay coaches to tell you.

### 4. Schedule Review itself as a Q2 activity

Review doesn't happen by itself. Block fixed time:
- Every Sunday 21:00-21:20 → weekly review
- 1st of each month 09:00-10:00 → monthly review
- Last Sunday of each quarter, morning → quarterly review

---

## Why 9 files instead of 1?

The predecessor of this skill was a single-file skill at 2,943 lines. Reasons to split:

1. **Context efficiency:** Claude only loads the sub-skill it needs — no wasted context window
2. **Maintainability:** A single-skill update doesn't affect the others
3. **Flexible composition:** Use 3 of them without loading the rest
4. **Aligned with skill spec:** Anthropic recommends single-responsibility per skill

The original single-file version is [sethmblack/paks-skills](https://github.com/sethmblack/paks-skills); this repo is an MIT-licensed refactor.

**v2.0 changes (vs. the original):**

- Split into 8 independent skills
- Full Chinese localization (framework, examples, prompts)
- Optimized `description` fields to improve auto-trigger accuracy
- Added a dual-mode output ("conversation mode / deep-analysis mode")
- Added Chinese-context adaptation notes

**v2.1 changes (based on full OCR of the original book):**

- **Added `life-center-diagnosis`** — based on Appendix I, as a prerequisite to mission-statement work
- **Expanded `quadrant-ii-time-management`** — added fourth-generation time management, role-based weekly templates, Appendix II "daily template"
- **Embedded P/PC balance** — into `sharpen-the-saw` and `quadrant-ii`, as the underlying reason Q2 matters
- **Embedded the maturity continuum as a diagnostic** — into `stephen-covey`, to quickly identify where you are
- **Routing upgrade** — `stephen-covey` changed from "trigger-word → sub-skill" to "**diagnose first (maturity + life center + plan completeness) → then dispatch**"
- **Tone shifted toward the original book's mentor voice** — quotes original metaphors (the goose that lays golden eggs, the woodcutter and the saw, the optometrist's prescription)
- **Each sub-skill ends with a "Put It Into Practice" assignment** — borrowed from the end-of-chapter exercises in the book

---

## Limits and notes

### What this skill set can do

- ✅ Inspect your plans with a Covey lens
- ✅ Diagnose time distribution, relationship health, burnout level
- ✅ Output structured analysis reports and concrete suggestions
- ✅ Provide a principle-centered angle on communication, negotiation, decisions

### What this skill set cannot do

- ❌ **Doesn't store your data:** every new conversation starts blank (pair it with a Claude Project)
- ❌ **Doesn't track task state:** whether you did it today, current progress — it doesn't know
- ❌ **Doesn't send reminders:** it's a *consultant*, not a *secretary*
- ❌ **Doesn't replace a real coach:** on major life decisions, it's a support tool, not a decider

### A frank reminder

The biggest enemy of life planning isn't method — it's **persistence**.

This skill set is great the first time you review. Six months later, you may have forgotten it exists. The thing that actually works is making the review itself a Q2 activity — immovably blocked into your calendar.

That's Covey's core point: **"Sharpening the saw must be scheduled, or it never happens."**

---

## Contributing

Issues and PRs welcome. Especially welcome:
- Translations into other languages
- New review prompt templates
- Use cases and experience reports

---

## License

MIT License. Refactored from [sethmblack/paks-skills](https://github.com/sethmblack/paks-skills).

---

## Further reading

- 📖 *The 7 Habits of Highly Effective People* — Stephen R. Covey
- 📖 *First Things First* — Stephen R. Covey
- 📖 *The Speed of Trust* — Stephen M.R. Covey
- 🔗 [Anthropic Skills official docs](https://docs.claude.com/en/docs/claude-code/skills)
- 🔗 [Anthropic's official Skills examples repo](https://github.com/anthropics/skills)

---

*"The key is not to prioritize what's on your schedule, but to schedule your priorities."*
*— Stephen R. Covey*
