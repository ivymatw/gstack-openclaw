# SPEC.md — GStack → OpenClaw: Design Philosophy

> "The engineering barrier is gone. What remains is taste."
> — Garry Tan

---

## What This Is

A port of Garry Tan's GStack skill pack into OpenClaw — but more importantly, a translation of its **decision-making frameworks** from a coding environment into a conversational one. The code changes. The thinking doesn't.

This document is the philosophical foundation. Anyone reading this should understand the entire design intent well enough to reimplement every skill from scratch.

---

## Part I: Why GStack Works

### The Core Insight: Process, Not Tools

GStack is not a collection of useful prompts. It is a **sprint process** encoded as slash commands:

```
Think → Plan → Build → Review → Test → Ship → Reflect
```

Each stage has a different cognitive mode. Each mode requires a different kind of thinking:
- **Think** (office-hours): Am I solving the right problem?
- **Plan** (ceo-review + eng-review): Is this plan sound?
- **Build**: Implementation
- **Review** (review): What could still break?
- **Test** (qa): Does it actually work?
- **Ship**: Release
- **Reflect** (retro): What did we learn?

The genius of GStack is that it forces context-switching between modes. Without a structured process, most people conflate all of these — they start building before the problem is understood, they skip review because they "know" the code works, they never reflect. The skills enforce discipline by creating explicit transitions.

**This process is environment-agnostic.** The "Build" stage requires code. Everything else — Think, Plan, Review logic, Reflect — requires thinking. And thinking can happen in any medium.

### Why the Thinking Layer Is the Valuable Layer

Garry Tan's productivity claims (600,000 lines in 60 days, 10,000-20,000 usable lines/day) are enabled by GStack's **thinking layer**, not its coding layer.

Here's why: AI can write code at near-zero marginal cost. The bottleneck is not implementation — it's knowing *what* to implement. The skills that provide this clarity (office-hours, ceo-review) are therefore the highest-leverage skills in the entire system.

A mediocre implementation of the right idea beats a perfect implementation of the wrong idea. The thinking layer is where that distinction gets made.

### The Completeness Principle: Boil the Lake

GStack's "Boil the Lake" principle states: when AI makes the marginal cost of completeness near-zero, always do the complete thing.

In the coding context: don't skip the last 10% of feature implementation, don't defer test coverage, don't shortcut edge cases. With AI, these cost minutes, not days.

**Adapted for OpenClaw**: when AI makes the marginal cost of deep thinking near-zero, always go deep. A surface-level office-hours session and a thorough one take the same conversation. Ask all 6 questions. Push on vague answers. Don't shortcut to 3.

The principle generalizes: **the compression ratio is equally dramatic for thinking as it is for coding.** A session that would have taken 2 days with a human advisor takes 30 minutes with AI. The "2 days" version was always worth it — now there's no excuse not to do it.

---

## Part II: The Mental Model Shift — Coding Loop vs. Decision Loop

### GStack's Mental Model: The Coding Loop

GStack is optimized for engineers **actively in a coding sprint**. The context is:
- A codebase is open
- Files can be read, edited, committed
- Tests can be run
- The user is in execution mode

Every GStack skill is designed to improve what gets **built**. Even office-hours and ceo-review are ultimately oriented toward the codebase — they produce design docs that feed into `plan-eng-review` which feeds into implementation.

The loop is: **Idea → Code → Ship**. GStack optimizes every stage of that loop.

```
[office-hours] → design doc
[plan-ceo-review] → design doc (revised, scoped)
[plan-eng-review] → technical plan + test matrix
[implementation] ← reads all above
[review] → bug catches → fixes
[qa] → browser testing → fixes  
[ship] → PR created
[retro] → git history analyzed
```

The skills chain through the **file system**. The design doc that office-hours writes is the same file that ceo-review reads. The test plan that eng-review writes is the same file that qa picks up. The chain is tight, automated, and operates through artifacts on disk.

### OpenClaw's Mental Model: The Decision Loop

OpenClaw operates in a different context entirely. There is no open codebase. There is a **conversation** — and behind it, a person making decisions about how to spend their time, attention, and energy.

The relevant loop is: **Problem → Decision → Action**. And the bottleneck at each stage is different:
- **Problem**: Is this the right problem? (office-hours)
- **Decision**: Is this the right decision? (ceo-review, eng-review)
- **Action**: What's the specific next action? (all skills)

In the coding loop, the artifact is code. In the decision loop, the artifact is **clarity** — about what to do and why.

This shift has structural implications:

| Dimension | GStack (Coding Loop) | OpenClaw (Decision Loop) |
|---|---|---|
| Context | Codebase, files, git | Conversation, memory, Obsidian |
| User state | In execution mode | In exploration or decision mode |
| Primary output | Design doc → code → PR | Design note → clarity → action |
| Chain mechanism | File system artifacts | Obsidian notes + conversational context |
| Feedback loop | Tests pass or fail | Decision leads to outcome |
| "Done" criteria | Code merged | Action taken, decision made |
| Time horizon | Next sprint (days) | Next chapter (weeks to months) |

Neither loop is better. They're optimized for different contexts. GStack users are building. OpenClaw users are **deciding what to build, whether to build, and how to think about what they've built**.

### The Target User Difference

GStack's target: founders and engineers actively shipping code. Technical enough to run Claude Code. In a sprint.

This port's target: **Steve Ma** — a retired executive with deep technical expertise who is now in a **life design sprint**, not a code sprint. He is:
- Exploring ideas (should I build X? should I pursue Y?)
- Making strategic decisions (where should I focus my attention?)
- Designing systems (how should I set this up?)
- Reflecting on progress (what did I learn this week?)
- Not necessarily implementing anything immediately

The skills must therefore be calibrated for **pre-implementation thinking** — not "how do we build this" but "should we build this, and is our thinking about it clear enough to act on?"

---

## Part III: What Gets Ported and Why

### The Port Taxonomy

**Category 1: Pure Thinking Frameworks — Port Directly**

These skills work because of the intellectual frameworks they encode, not because of their code integration. The frameworks are fully portable.

| GStack Skill | Framework | Why It Ports |
|---|---|---|
| `/office-hours` | YC's 6 diagnostic questions | The questions work on any idea, not just software |
| `/plan-ceo-review` | Brian Chesky's 10-star thinking + 18 CEO patterns | Strategic thinking is environment-agnostic |
| `/investigate` | Iron Law debugging + pattern matching | Root cause thinking applies to any problem |
| `/plan-eng-review` | Architecture diagrams + failure mode mapping | System design thinking works on any system |
| `/retro` | Weekly retrospective + trend analysis | Personal + project reflection needs no codebase |

**Category 2: Heavily Adapted (Future Work)**

These skills have valuable thinking frameworks, but the coding integration is load-bearing:
- `/review` — the staff engineer's bug-hunting mindset could become an "idea review," but loses fidelity without a diff to examine
- `/ship` — the release discipline is valuable but the mechanics are code-only

**Category 3: Skip (Code Infrastructure)**

These skills are pure code tooling with no thinking layer to port:
- `/browse`, `/qa`, `/qa-only` — browser automation
- `/careful`, `/freeze`, `/guard` — code safety hooks
- `/codex` — multi-AI code review
- `/setup-browser-cookies`, `/gstack-upgrade` — utility tools

### The Five Ported Skills

1. **office-hours** — YC product thinking
2. **ceo-review** — Strategic/founder thinking
3. **investigate** — Systematic debugging (any domain)
4. **eng-review** — Technical architecture review
5. **retro** — Weekly reflection

These five cover the three highest-leverage thinking modes:
- **Clarity of problem** (office-hours)
- **Clarity of strategy** (ceo-review)
- **Clarity of system** (eng-review)
- **Clarity of root cause** (investigate)
- **Clarity of progress** (retro)

---

## Part IV: The Adaptation Principles

### Principle 1: Preserve the Framework, Adapt the Mechanics

Every GStack skill has two layers:
1. **The intellectual framework** — the questions asked, the cognitive patterns applied, the structure of the analysis
2. **The mechanics** — bash commands, file reading, telemetry, AskUserQuestion calls

In porting: preserve layer 1 completely. Adapt layer 2 for conversational use.

Example — office-hours:
- **Preserve**: The 6 YC questions, their sequence, the push-back posture, the premise challenge, the alternatives generation
- **Adapt**: Replace `AskUserQuestion` with conversational follow-up; replace file system output with Obsidian save; remove bash preamble, telemetry, and YC application pitch

### Principle 2: One Question at a Time — Always

GStack enforces this in office-hours: "Questions ONE AT A TIME." This rule exists because batching questions lets users answer shallowly. When only one question is live, the person must engage with it directly.

This principle is **more important in conversational mode**, not less. In a coding session, the user is focused. In a conversation, they can drift. One question keeps the thread.

### Principle 3: Push Until Specific

GStack's startup mode has this principle: "comfort means the founder hasn't gone deep enough." When someone gives a vague answer, the skill should push again — not accept it and move on.

This is the difference between a useful office-hours session and a useless one. A useful session produces:
- A named specific human (not "SMBs")
- Specific evidence of demand (not "people seem interested")
- A specific narrowest wedge (not "we'd need to build the platform")

Push once. Then push again. The real answer usually comes on the third try.

### Principle 4: Questions Are Evidence, Not Courtesy

Every question in every skill exists because the answer reveals something specific about the quality of the thinking. It's not a conversation scaffold — it's diagnostic.

The purpose of Q1 (Demand Reality) is not to "understand the idea better" — it's to test whether real demand has been validated. If the answer is vague, that's not just a communication failure — it's evidence that demand validation hasn't happened.

Skill designers must know what each question is testing and what answer pattern indicates a problem.

### Principle 5: Obsidian as the File System

GStack uses `~/.gstack/projects/` as its artifact store. Design docs written by office-hours are read by ceo-review. Test plans written by eng-review are picked up by qa. The file system is the integration layer.

OpenClaw's equivalent is **Obsidian**. Every skill saves its output to `obsidian/GStack/YYYY-MM-DD-[skill]-[slug].md`. When a downstream skill needs context from an upstream one, it reads the Obsidian note.

This creates the same chain:
```
office-hours note → ceo-review reads it → eng-review reads both → retro references all
```

The chain must be maintained deliberately in conversation: "Should I look at your last office-hours note?" But the artifact discipline is the same.

### Principle 6: Opinionated Output

GStack skills end with recommendations, not menus. "RECOMMENDATION: Approach A because [reason]." Not "here are some things to consider."

This principle is critical for the target user. Steve doesn't want a menu of options — he wants a recommendation he can evaluate, push back on, and decide about. The skill should have a position.

### Principle 7: Status Reporting

Every GStack skill ends with: DONE / DONE_WITH_CONCERNS / BLOCKED / NEEDS_CONTEXT.

This is more than ceremony — it forces the skill to account for its own completeness. "DONE" requires evidence. "DONE_WITH_CONCERNS" requires listing the concerns. "BLOCKED" requires explaining what's blocking.

Preserve this protocol exactly.

---

## Part V: What Gets Dropped and Why

### Dropped: Bash Preamble and Telemetry

GStack's preamble runs bash commands to check for updates, track sessions, initialize telemetry, and detect the git branch. None of this is relevant in OpenClaw. Drop entirely.

### Dropped: AskUserQuestion as a Tool Call

GStack uses `AskUserQuestion` as a literal tool call that pauses execution and waits for user input. In OpenClaw, questions are natural conversational turns. Same discipline (one at a time, never batch), different mechanics.

### Dropped: YC Application Pitch

GStack's office-hours ends with a pitch for Y Combinator, calibrated by "founder signal strength." Steve is 56, a retired exec, and a former VP who led an industry consortium. He is not applying to YC.

The spirit of this — "you're showing real founder thinking" — is worth preserving as an observation, but the pitch itself is dropped entirely.

### Dropped: Completeness Scores for Code

GStack's AskUserQuestion format includes `Completeness: X/10` scores that calibrate against code implementation completeness. In OpenClaw, completeness is assessed against thinking quality: has the framework been applied fully? Have questions been pushed until specific? Has the premise challenge been run?

The scoring concept is useful, but the calibration is different.

### Dropped: Git Integration

All git commands — `git log`, `git diff`, `git branch` — are dropped. Context comes from Obsidian memory files and conversation.

---

## Part VI: Success Criteria

An implementation of these skills is successful if:

1. **Every skill is trigger-able** by natural phrases Steve would actually use — not formal slash commands
2. **Core frameworks are preserved intact** — all 6 YC questions, all 4 CEO modes, all phases of the Iron Law, all 8 eng-review questions
3. **Every session produces an Obsidian note** at `obsidian/GStack/YYYY-MM-DD-[skill]-[slug].md`
4. **Questions are pushed** — vague answers don't get accepted; the skill pushes for specificity
5. **Skills chain** — downstream skills can reference upstream Obsidian notes
6. **Outputs are opinionated** — every session ends with a recommendation, not a list of considerations
7. **Status is reported** — every session ends with DONE / DONE_WITH_CONCERNS / BLOCKED / NEEDS_CONTEXT
8. **Anyone reading DESIGN.md** can understand the complete intellectual framework well enough to reimplement any skill

---

## Version

- Version: 1.0.0
- Date: 2026-03-20
- Author: Ivy (OpenClaw AI assistant)
- Based on: GStack v2.x by Garry Tan (https://github.com/garrytan/gstack), MIT License
