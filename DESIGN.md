# DESIGN.md — Intellectual Frameworks Reference

> This is the source of truth for every framework being ported. Someone reading this should understand the complete intellectual content of each skill well enough to reimplement everything from scratch.

**Relationship to PROMPTS.md**: This document is the source of truth for all intellectual frameworks. PROMPTS.md contains production-ready SKILL.md content distilled from this document. When details differ, DESIGN.md governs. When updating frameworks, update DESIGN.md first, then propagate to PROMPTS.md.

---

## How to Read This Document

Each skill section contains:
1. **The Core Framework** — the intellectual model, not the implementation
2. **The Diagnostic Purpose** — what each question/phase is testing, and what answer patterns indicate problems
3. **The Edge Cases** — what happens when the framework hits friction
4. **The Output Structure** — what a complete session produces and why
5. **The Chain** — how this skill's output feeds the next skill

### Completeness Calibration for Conversational Use

The original GStack provides a compression ratio table for coding tasks. The equivalent for decision-making:

| Thinking task | Solo thinking | AI-assisted | Compression |
|---|---|---|---|
| Problem definition & reframing | 2 days | 30 minutes | ~6x |
| Premise identification & challenge | Half day | 15 minutes | ~20x |
| Alternative generation | 1 day | 20 minutes | ~30x |
| Root cause tracing | 1 day | 30 minutes | ~15x |
| Architecture review (8 questions) | 2 days | 45 minutes | ~4x |
| Weekly retrospective with data | 3 hours | 20 minutes | ~9x |

This table makes "always go deep" a calibrated judgment, not a slogan. A 30-minute office-hours session that covers all 6 questions is the equivalent of 2 days of solo thinking. There is no reason to shortcut.

---

## Skill 1: `office-hours` — YC Product Thinking

### The Core Framework

Office-hours is designed to close the gap between **what founders think they're building** and **what they're actually building**. This gap is almost always present. The skill's job is to surface it before implementation begins.

The canonical example from GStack: a founder says "I want to build a daily briefing app for my calendar." After running through the forcing questions, it becomes clear they're actually building "a personal chief of staff AI." The reframe changes the entire product. Without the questions, they build the wrong thing excellently.

The framework has two distinct modes because the diagnostic purpose differs:
- **Startup mode**: Is there real demand? Is this a business?
- **Builder mode**: Is this the most exciting version of this idea?

Both modes end in the same place (alternatives + design note) but travel different paths.

### Why Two Modes? The Question Design Logic

The six startup questions are specifically calibrated for **demand validation failure modes** — the ways founders most commonly fool themselves:
- Confusing interest for demand
- Describing categories instead of people
- Being attached to architecture over value
- Not having watched real users struggle
- Not having a future-fit thesis

The builder questions are calibrated for **excitement maximization** — what makes this idea as interesting as possible, what's the fastest path to something shareable, what's the 10x version.

A builder asked startup questions will feel interrogated and defensive. A startup founder asked builder questions will feel unchallenged and uncritical. Mode selection is not a convenience — it's precision tooling.

### The Six Startup Forcing Questions — Full Diagnostic Logic

#### Smart Routing by Product Stage

Not every idea needs all six questions. The diagnostic purpose of each question maps to a specific product stage:

- **Pre-product** (idea stage, no users yet) → Q1, Q2, Q3 — validate demand exists before anything else
- **Has users** (people using it, not yet paying) → Q2, Q4, Q5 — understand the status quo gap and observe real behavior
- **Has paying customers** → Q4, Q5, Q6 — find the wedge, observe usage, validate future-fit

This routing is a recommendation, not a hard gate. If a question's answer is already clear from context, skip it and name it: "Your answer to Q2 already covers Q4, so let's move on." If the situation is ambiguous, default to asking all six — the Completeness Principle applies.

The routing exists because asking a pre-product founder about Future-Fit (Q6) is premature, and asking someone with paying customers about Demand Reality (Q1) is redundant.

#### Q1: Demand Reality

**The question**: "What's the strongest evidence you have that someone actually wants this — not interested, not signed up for a waitlist, but would be genuinely upset if it disappeared tomorrow?"

**What it's testing**: Whether the founder has crossed the threshold from "people are interested" to "people depend on this." These are categorically different things.

**The demand ladder** (from weakest to strongest evidence):
1. "People say it's interesting" — not demand
2. "We got waitlist signups" — not demand
3. "VCs are excited about the space" — not demand
4. "We have beta users" — possible weak demand
5. "Users use it daily" — possible demand
6. "Someone called us when it went down" — demand
7. "Someone expanded usage without being asked" — demand
8. "Someone pays us money" — strong demand
9. "Someone would scramble to replace us if we disappeared" — strong demand

**Push pattern**: Accept only levels 6-9 as evidence of demand. Push on anything weaker. "They're on the waitlist" → "Have you had a conversation with any of them about how they're solving this problem today?" "People say it's interesting" → "What's the most specific evidence you have — not vibes, but something a person actually did?"

**Red flag patterns to name directly**: "We got 500 waitlist signups." "VCs are excited." "Industry analysts say this market is growing." None of these are demand — name it.

#### Q2: Status Quo

**The question**: "What are people doing right now to solve this problem — even badly? What does that workaround cost them?"

**What it's testing**: Whether there is real pain. The status quo is the product's actual competitor — not another startup, but the existing workaround. If the status quo is "nothing," either the problem isn't painful enough (most likely) or the opportunity is genuinely novel (rare).

**The status quo ladder** (from least to most painful):
1. "Nothing — there's no solution, that's the opportunity" — suspect
2. "They use a general tool badly (Excel, email, Slack)" — mild pain
3. "They have a paid but inadequate tool" — moderate pain
4. "They have hired a person to do this manually" — significant pain
5. "They have built their own internal tool to solve this" — strong pain
6. "They are constantly failing at this despite real effort" — strong pain

**Push pattern**: Get specific. "They use spreadsheets" → "Walk me through what that looks like in practice — what does a specific person do on a specific day to manage this?" The goal is a concrete picture of the workaround, not a category description.

**The cost extraction**: Every workaround has a cost — hours per week, dollars per month, errors per quarter, hires needed. Extract the number. "It takes forever" → "What does 'forever' mean in hours?"

#### Q3: Desperate Specificity

**The question**: "Name the actual human who needs this most. What's their title? What gets them promoted? What gets them fired? What keeps them up at night?"

**What it's testing**: Whether the founder can name a real person, not a category. Categories are fiction. "Marketing teams at mid-market B2B companies" is not a customer. "Sarah, Head of Marketing at Acme Corp, who is responsible for pipeline attribution and gets blamed when the numbers don't add up" is a customer.

**The specificity ladder** (from least to most useful):
1. "Enterprises in healthcare" — fiction
2. "Marketing teams" — category
3. "Marketing managers at SaaS companies" — narrow category
4. "Marketing operations leads at 50-200 person SaaS companies" — closer
5. "The person responsible for CRM data quality at a fast-growing startup" — close
6. "Sarah at Acme Corp, ops manager, responsible for CRM hygiene" — real

**Push pattern**: "Marketing teams" → "Okay, within that, who specifically? What's their title?" → "Head of Marketing Ops" → "And what does a Head of Marketing Ops at a 100-person company get fired for?" → "Missing pipeline targets because of bad attribution data." That's a real person with real stakes.

**The four questions about the person**:
- What gets them promoted? (What is success for them?)
- What gets them fired? (What is failure for them?)
- What keeps them up at night? (What is their anxiety?)
- What would they pay to make the anxiety go away? (Where is the value?)

#### Q4: Narrowest Wedge

**The question**: "What's the smallest possible version of this that someone would pay real money for — this week, not after the platform is built?"

**What it's testing**: Whether the founder is attached to architecture or to value. The classic failure mode: "We need to build the full platform before anyone can really use it." This is almost always false. There is always a smaller version.

**The narrowest wedge heuristic**: The narrowest wedge is the intersection of (a) smallest scope that provides a complete value moment and (b) something buildable in days, not months.

**Finding the wedge — the de-featurization ladder**:
1. Full product vision → too big
2. Core feature set → probably still too big
3. One feature → getting closer
4. One workflow → possibly right
5. One workflow for one user in one context → right size

**The bonus push**: "What if the user didn't have to do anything to get value — no login, no integration, no setup? What would that look like?" This forces the absolute minimum. If the answer is "that's not possible," push on why not. Very often the setup/onboarding can be eliminated.

**Red flags**: "We need the full platform first." "Stripped down it's not differentiated." Both of these mean attachment to the architecture. The right response: "The platform is what you're building toward. What delivers value before the platform exists?"

#### Q5: Observation & Surprise

**The question**: "Have you actually sat down and watched someone use this without helping them? What did they do that surprised you?"

**What it's testing**: Whether the founder has moved beyond hypothetical users to observed behavior. Surveys reveal what people say they do. Demos reveal what people can be walked through. Observation reveals what people actually do.

**Why surprise is the key word**: If nothing surprised you, you were either filtering observations through your existing assumptions, or you haven't done the observation. Genuine observation almost always produces surprise. The surprise is data.

**The gold**: The most valuable observation is when a user does something the product wasn't designed for. That's the real product trying to emerge. "Users kept exporting our data to Excel and building their own dashboards" → the real product is the dashboard.

**The hierarchy of research quality**:
1. Survey — weakest; measures what people say
2. Demo call — weak; measures what people do when guided
3. Watching without helping — strong; measures what people actually do
4. Longitudinal usage data — strongest; measures patterns over time

**Push pattern**: "We did user interviews" → "Did you watch them use it, or did you ask them questions about it?" → "We asked them questions" → "Have you sat behind someone and watched them try to use it without helping?" That's the question. If no, that's assignment #1.

#### Q6: Future-Fit

**The question**: "If the world looks meaningfully different in 3 years — and it will — does this become more essential or less? Why?"

**What it's testing**: Whether the founder has a product thesis that improves with time, not just a business that exists in a growing market.

**The distinction**: "The market is growing 20% per year" is not a thesis. That rising tide raises everyone. The question is whether this specific product becomes more valuable as the world changes — and specifically, why.

**Good future-fit answers**:
- "As AI handles more routine tasks, the intelligence layer we provide becomes more valuable, not less"
- "As remote work becomes the default, the problem we solve gets more acute"
- "As data volumes grow, the manual process we replace becomes more painful"

**Bad answers**:
- "AI will make everything better" (rising tide, not specific)
- "The market is growing" (market ≠ your product)
- "We'll have more features by then" (that's not a thesis, that's a roadmap)

**Push pattern**: "AI will help us" → "How specifically does AI changing affect the value proposition? Does it make your product more essential, or could AI replace what you're building?" The latter is actually the risk the founder should be thinking about.

### The Builder Mode Questions — Generative Logic

Builder mode is not interrogative — it's generative. The goal is to find the most exciting version of the idea, not to validate demand.

**Q1: Coolest version** — "What would make someone say 'whoa'?" 
*Logic*: Forces toward the genuine creative ambition, not the conservative first draft.

**Q2: Who you'd show it to first** — "What reaction are you hoping for?"
*Logic*: Reveals the actual target audience and the emotional core of the value proposition.

**Q3: Fastest path to shareable** — "What's the minimum to show someone?"
*Logic*: Builder mode's equivalent of the narrowest wedge — prioritizes shipping and feedback over completeness.

**Q4: What's closest** — "How is yours different?"
*Logic*: Forces awareness of the landscape and a differentiation claim.

**Q5: The 10x version** — "If you had unlimited time?"
*Logic*: Reveals the full vision, which often clarifies what the core is and what's expandable.

### Phase 3: Premise Challenge — The Logic

After the questions, the premise challenge does something distinct: it converts implicit assumptions into explicit claims that can be agreed with or challenged.

Every plan rests on premises. Unstated premises are dangerous because they can be wrong without anyone noticing. The premise challenge forces them into the open.

**How to identify premises**: Look at the alternatives (Phase 4 candidates) and ask "what has to be true for this to work?" Those are the premises.

Example for a productivity app:
- "Users want to manage this from a single interface" — true or false?
- "The problem is discovery, not execution" — true or false?
- "The narrowest wedge is the power user, not the occasional user" — true or false?

The answers determine which alternatives make sense. If a premise turns out to be false, the entire plan may need revision.

### Phase 4: Alternatives — Why Three and Why Mandatory

The alternatives phase is non-optional because it prevents **premature convergence** — the tendency to develop the first viable idea and stop exploring.

**Why three alternatives specifically**:
- One: the obvious path (already in the person's head)
- Two: the alternative (what if we did it differently?)
- Three: the lateral move (what if we were wrong about the framing?)

The three alternatives should represent different **positions in the trade-off space**, not just different implementations of the same idea. Common dimensions: minimal vs. complete, fast vs. thorough, narrow vs. broad, incremental vs. transformative.

**The mandatory recommendation**: After presenting alternatives, give a specific recommendation. "RECOMMENDATION: Approach A because [one-line reason]." The skill is not a vending machine of options — it's an advisor with a position.

### The Design Note — What Gets Saved and Why

The output is a structured Markdown note in Obsidian. Structure serves a purpose:

- **The Reframe**: Captures how the idea was re-understood — this is the most valuable output of startup mode
- **Demand Evidence through Future-Fit**: Creates a permanent record of what was validated and how
- **Premises**: Documents the load-bearing assumptions so they can be revisited if the plan fails
- **Approaches + Recommendation**: Documents the decision and its reasoning
- **The Assignment**: Creates accountability — one concrete action before next session
- **What I noticed about how you think**: Mentor-mode observation using specific quotes; not generic praise

The note is designed to be readable months later as a record of the thinking at the time.

### Design Lineage & Cross-Session Discovery

When starting a new office-hours session, the skill should check for prior GStack notes on the same topic:

```
ls obsidian/GStack/*-office-hours-*.md
```

If related design notes exist, surface them: "Prior designs on related topics: [titles + dates]. Should we build on one of these or start fresh?"

This creates a revision chain — you can trace how an idea evolved across multiple sessions. The new note gets a `Supersedes:` field referencing the prior note if the user chooses to build on it.

Cross-skill discovery also applies: when starting ceo-review, check for prior office-hours notes. When starting eng-review, check for both. The chain is maintained through explicit references, not implicit assumptions.

### Thinking Quality Signals

During the session, track which of these signals appear in the user's responses:

1. **Articulated a real problem** — not hypothetical, describes someone's actual pain
2. **Named specific users** — people, not categories ("Sarah at Acme" not "enterprises")
3. **Pushed back on premises** — conviction, not compliance; disagreed with a challenge and had reasons
4. **Domain expertise** — knows this space from the inside, not from research
5. **Showed taste** — cared about getting details right, rejected "good enough"
6. **Showed agency** — already building or testing, not just planning
7. **Solves a problem others need** — not just a personal itch

These signals feed the "What I noticed about how you think" section of the design note. The observation must use specific quotes from the session — "You didn't say 'small businesses,' you said 'the ops manager at a 50-person logistics company.' That specificity matters." — not generic characterizations like "you showed good product thinking."

---

## Skill 2: `ceo-review` — Strategic/Founder Thinking

### The Core Framework

CEO review applies **Brian Chesky's 10-star thinking** to any plan or idea. Chesky's framework: describe the 1-star experience (terrible), describe the 5-star experience (what Airbnb currently provides), describe the 10-star experience (impossible, absurd), then work backward from 10-star to find the 7-star experience (possible, delightful, unexpected).

The insight: almost everyone starts at 5-star and optimizes. 10-star thinking forces you to conceive of a different category entirely. "What does a 10-star experience look like?" is a different question than "how do we improve this?"

Applied to product/idea review: not "how do we implement this ticket," but "what is the ideal version of what this is trying to accomplish?"

### The Four Modes — Logic and Design

The four scope modes are a key design choice in GStack. The reasoning:

**Why four modes, not one?** Because the right cognitive posture depends entirely on where the person is in their decision process:
- Still exploring → Expansion (need to see what's possible)
- Partially committed but open → Selective Expansion (want opportunities without obligation)
- Committed, need rigor → Hold Scope (execution-oriented)
- Over-committed, need to cut → Reduction (scope creep has happened)

Presenting options in the wrong mode is actively harmful. Running EXPANSION when someone needs REDUCTION gives them more rope to hang themselves with. Running HOLD SCOPE when they're still exploring prevents them from seeing the better path.

**Mode logic in detail**:

**EXPANSION**: 
- Posture: enthusiastic, ambitious, the model thinks like a founder at the beginning of the journey
- Rule: every expansion is a specific opt-in decision; never silently expand
- The CEO cognitive pattern active: temporal depth (5-year arcs), willfulness (push hard in one direction), leverage obsession (find the 10x input)
- Output: a list of specific expansion opportunities, each with effort and risk

**SELECTIVE EXPANSION**:
- Posture: rigorous on current scope, opportunistic on expansions; neutral recommendation stance
- Rule: surface each opportunity individually; present neutrally; let the person cherry-pick
- The CEO cognitive pattern active: speed calibration (most things are two-way doors; fast decisions), classification instinct (reversible vs. irreversible)
- Output: current scope bulletproofed + a menu of opt-in expansions

**HOLD SCOPE**:
- Posture: paranoid reviewer; make this bulletproof; no scope changes of any kind
- Rule: rigor without change — neither secretly expand nor secretly cut
- The CEO cognitive pattern active: inversion reflex (what would make this fail?), proxy skepticism (are we measuring the right things?)
- Output: the existing plan with failure modes found, edge cases named, gaps identified

**SCOPE REDUCTION**:
- Posture: surgeon; what is the minimum viable version that achieves the core outcome?
- Rule: cut ruthlessly; never sneak scope back in; be specific about what's cut and why
- The CEO cognitive pattern active: focus as subtraction (Jobs: 350 products → 10), subtraction default (if it doesn't earn its pixels, cut it)
- Output: a reduced plan with explicit list of what was cut and why

**Critical rule**: Once a mode is selected, commit. Never drift between modes. If the model silently drifts from EXPANSION to HOLD SCOPE because the plan looks risky, that's a violation of the user's decision. The user made a choice about what kind of review they wanted.

### The 18 CEO Cognitive Patterns — The Full List

These are not a checklist to enumerate — they are thinking instincts to internalize and apply throughout the review. The model should think like a CEO who has internalized these patterns, not enumerate them.

1. **Classification instinct** (Bezos): Categorize every decision by reversibility × magnitude. One-way doors are irreversible and consequential — slow down. Two-way doors are reversible — move fast. Most decisions are two-way doors.

2. **Paranoid scanning** (Grove): Continuously scan for strategic inflection points, cultural drift, talent erosion, process-as-proxy disease. "Only the paranoid survive."

3. **Inversion reflex** (Munger): For every "how do we win?", also ask "what would make us fail?" Invert the problem. Many more paths to failure than to success.

4. **Focus as subtraction** (Jobs): Primary value-add is what to NOT do. Going from 350 products to 10. Removing features, not adding them. The hardest skill.

5. **People-first sequencing** (Horowitz): People, then products, then profits. In that order. Always. Talent density solves most other problems.

6. **Speed calibration** (Bezos): Fast is default. 70% of the information is enough to decide. Only slow down for irreversible + high-magnitude decisions. Regret from inaction >> regret from wrong action in most cases.

7. **Proxy skepticism** (Bezos Day 1): Are our metrics still serving users, or have they become self-referential? Day 2 companies optimize for proxies.

8. **Narrative coherence**: Hard decisions need clear framing. Make the "why" legible — not everyone happy. Happiness is a proxy for good framing.

9. **Temporal depth** (Bezos): Think in 5-10 year arcs. Apply regret minimization for major bets — would you regret this at 80?

10. **Founder-mode bias** (Chesky/Graham): Deep involvement in product details is not micromanagement if it expands (not constrains) the team's thinking.

11. **Wartime awareness** (Horowitz): Correctly diagnose peacetime vs. wartime. Peacetime habits kill wartime companies. Different rules apply.

12. **Courage accumulation**: Confidence comes FROM making hard decisions, not before them. The struggle is the job.

13. **Willfulness as strategy** (Altman): Be intentionally willful. The world yields to people who push hard in one direction long enough. Most give up too early.

14. **Leverage obsession** (Altman): Find the inputs where small effort creates massive output. Technology is the ultimate leverage.

15. **Hierarchy as service**: Every interface decision answers "what should the user see first, second, third?" This respects their time.

16. **Edge case paranoia (design)**: What if the name is 47 characters? Zero results? Network fails mid-action? First-time user vs. power user? Empty states are features.

17. **Subtraction default** (Rams): "As little design as possible." If a UI element doesn't earn its pixels, cut it.

18. **Design for trust**: Every interface decision either builds or erodes user trust. Pixel-level intentionality about safety, identity, and belonging.

### The 10-Section Review — Why Each Section

The review has 10 sections because each one tests a different failure mode that plans commonly exhibit:

1. **Problem Definition**: Is this the right problem, or a symptom? Plans fail because they solve the visible problem, not the actual one.

**Mode downgrade**: If Section 1 reveals that the problem definition itself is fundamentally wrong — not just needs refinement, but the entire framing is off — the right move is to pause the CEO review and redirect to office-hours. Say: "I think we need to step back. The problem definition doesn't hold up — before I can review the plan, we need to re-examine what we're actually solving. Let's do an office-hours session on this." This is not a failure of the CEO review; it's the review doing its job.

2. **The 10-Star Product**: What is the ideal version? Plans fail when they start from "what we can build" instead of "what would be ideal."

3. **Target User**: Is this a specific human or a category? Plans fail when the customer is fictional.

4. **Value Proposition**: Why this, why now, why you? Plans fail when the value is generic or the timing is wrong.

5. **Scope Assessment**: Is the scope right? Plans fail both from scope too large (can't execute) and scope too small (doesn't matter).

6. **Competitive Reality**: What does the status quo look like? Plans fail when they underestimate the inertia of "doing nothing."

7. **Risk Landscape**: What's the biggest bet? Plans fail when risks are unacknowledged.

8. **Team/Execution**: What capabilities are needed? Plans fail when the capability gaps aren't named.

9. **Success Metrics**: How do you know if it's working? Plans fail when success is unmeasurable.

10. **Recommendation**: PROCEED / PIVOT / STOP — a direct verdict. Plans fail when they're never actually decided upon.

### Prime Directives (from GStack, adapted)

These are engineering preferences that should influence every recommendation in the review. Not a checklist — internalized and applied:

- **Zero silent failures**: Every failure mode must be visible. Silent failures are critical defects in the plan.
- **Every error has a name**: Don't say "handle errors" — name the specific failure class, what triggers it, what the user sees.
- **Data flows have shadow paths**: Every data flow has a happy path and three shadow paths: nil input, empty input, upstream error.
- **Observability is scope, not afterthought**: Dashboards, alerts, and runbooks are first-class deliverables.
- **Diagrams are mandatory**: No non-trivial flow goes undiagrammed.
- **Optimize for the 6-month future**: If this plan solves today's problem but creates next quarter's nightmare, say so explicitly.

---

## Skill 3: `investigate` — Systematic Root-Cause Debugging

### The Core Framework

The Iron Law: **no fixes without root cause investigation first.**

This is not just a process rule — it's a theory about why debugging usually fails. The common failure mode: see a symptom → form a hypothesis → apply a fix → symptom goes away temporarily → a new symptom appears → apply another fix → whack-a-mole indefinitely.

The Iron Law says: this loop fails because fixes without root cause are fixes to symptoms, not causes. The underlying problem remains. You need to trace back from symptom to cause before touching anything.

**The framework applies to any domain**, not just code:
- A startup that keeps losing customers to churn (symptom) might have a product problem, a pricing problem, or an expectation-setting problem at sale (potential causes)
- An investor who keeps making bad timing calls (symptom) might have a wrong mental model about market cycles, inadequate research, or confirmation bias (potential causes)
- A project that keeps slipping deadlines (symptom) might have a scope problem, a dependency problem, or an estimation methodology problem (potential causes)

The framework is domain-agnostic. The discipline — trace to root cause before fixing — is universal.

### The Phases — Logic and Design

**Phase 1: Symptom Collection** 
Purpose: Separate observation from interpretation. Before forming a hypothesis, the symptom must be described precisely.

Three required pieces of information:
1. **What is observed** — the symptom, precisely described, not interpreted. "The API call returns 401" not "authentication is broken."
2. **Onset** — when did this start? Was it working before? Regressions are easier to debug than novel failures because the root cause is in the change.
3. **Reproduction** — reliable or intermittent? Intermittent failures are almost always race conditions, state corruption, or external dependency failures.

Do not form a hypothesis until all three are known. This is a hard rule. Premature hypotheses anchor thinking and cause people to interpret subsequent evidence in favor of the hypothesis rather than objectively.

**Phase 2: Pattern Matching**
Purpose: Before doing any original analysis, check whether the symptoms match known failure patterns. Most bugs are instances of a small number of recurring patterns.

The known patterns (adapted for general use):
| Pattern | Signature | Diagnostic question |
|---|---|---|
| Race condition | Intermittent, timing-dependent | Does frequency change with concurrent load? |
| Missing context | Null errors, empty results | What data should be there but isn't? |
| Configuration drift | Works in env A, not env B | What's different between the environments? |
| Integration failure | Timeout, unexpected response | Has the external thing changed recently? |
| Wrong mental model | More wrong than random | Is the problem different from what was assumed? |
| State corruption | Inconsistent data, partial writes | Has something left things in a partial state? |
| Order/timing | Works in one sequence, not another | Is there a required ordering that's violated? |

Matching the pattern narrows the hypothesis space. If symptoms match "configuration drift," hypotheses should be about configuration differences, not code bugs.

**Phase 3: Root Cause Hypothesis**
Form a specific, testable claim: "The root cause is [X] because [Y]. The evidence that would confirm this: [Z]."

Quality check for the hypothesis:
- Is it specific? (Not "something is wrong with auth" but "the JWT token is missing the `sub` claim when user has an org affiliation")
- Is it testable? (Can we design an experiment that would confirm or refute it?)
- Does it explain all the symptoms? (If hypothesis X is true, do all observed symptoms follow from it?)

**Phase 4: The Iron Law Check**
Before any fix: confirm that what we have is evidence of root cause, not a plausible hypothesis. The question to ask: "If this hypothesis is correct, what specific evidence should we see? Do we actually see that evidence?"

**The 3-Strike Rule**: The most important meta-rule in the framework. After three failed hypotheses, stop. Don't continue generating and testing hypotheses. The failure of three hypotheses is itself evidence — usually that the problem is at a different layer than assumed.

Common 3-strike situations:
- Three code-level hypotheses all fail → the problem is at the infrastructure or configuration level
- Three technical hypotheses all fail → the problem may be a wrong mental model about the system
- Three implementation hypotheses all fail → the problem may be architectural

After three strikes, the right move is to step back and ask: "Are we looking at the right layer? Are we solving the right problem?"

**Phase 5: Solution Path**
Once root cause is confirmed by evidence:
1. Fix the root cause, not the symptom
2. Minimal change — fewest things touched
3. Write a test that fails without the fix and passes with it
4. Define what evidence confirms the fix worked

The solution should be as narrow as the root cause. If root cause is in one function, don't refactor the module. Blast radius discipline: how far does this fix need to reach?

### The Red Flags

These are conditions that should trigger an explicit warning, not silent continuation:

- **"Quick fix for now"**: There is no "for now." Fix it right or escalate. Temporary fixes become permanent.
- **Proposing a fix before tracing data flow**: You're guessing. Guessing without a confirmed hypothesis is the failure mode the Iron Law prevents.
- **Each fix reveals a new problem elsewhere**: You're at the wrong layer. Stop and question the architecture.
- **Three hypotheses failed**: Don't generate a fourth — step back.
- **Fix touches more than 5 things**: Flag the blast radius. Large-blast-radius fixes are either addressing a root cause that's very widely distributed (architectural problem) or over-engineered.

---

## Skill 4: `eng-review` — Technical Architecture Review

### The Core Framework

Engineering review answers one question: **Is this plan buildable?**

Not "is it a good plan" (that's CEO review's job), not "should we do it" (that's office-hours' job). The eng review assumes the direction is set and asks: if we try to build this, what happens? What will break? What assumptions are hidden? What tests would give us confidence?

The key insight from GStack: **diagrams force hidden assumptions into the open**. When you try to draw the architecture, you discover the things you hadn't thought through. The act of drawing is itself an analysis tool. That's why diagrams are mandatory — not because they're a deliverable, but because drawing them is part of the thinking.

### The 8 Technical Questions — Full Logic

#### Prime Directives (Engineering Instincts)

These are not a checklist — they are engineering instincts that should inform every question and every recommendation throughout the review:

- **Zero silent failures**: Every failure mode must be visible. Silent failures are the most dangerous class of defect.
- **Every error has a name**: Don't say "handle errors" — name the specific failure class, what triggers it, and what the user sees.
- **Data flows have shadow paths**: Every data flow has a happy path and three shadow paths: nil input, empty input, upstream error. All four must be traced.
- **Observability is scope, not afterthought**: Dashboards, alerts, and runbooks are first-class deliverables, not follow-up items.
- **Diagrams are mandatory**: No non-trivial flow goes undiagrammed. Drawing is thinking.
- **Optimize for the 6-month future**: If this plan solves today's problem but creates next quarter's nightmare, say so explicitly.

**Q1: Architecture Boundaries**

What are the components, and what are the hard boundaries between them?

*Purpose*: Fuzzy boundaries are where bugs live. When component A does "some" of what component B does, and it's unclear which is responsible for what, you get a class of bugs that are hard to trace because the error could be in either component.

*What to force*: For every component, state not just what it does but what it explicitly does NOT do. "The API layer handles HTTP. It does NOT do business logic." Explicit non-responsibilities are as important as responsibilities.

*What bad architecture looks like*: "It kind of depends" on which component handles X. "The service handles it when..." (conditional responsibilities). "The controller does some validation and the model does some validation" (unclear ownership).

**Q2: Data Flow — All Four Paths**

For every data flow, trace: happy path, nil/empty input, partial failure, upstream error.

*Purpose*: Happy paths are easy to design. The three shadow paths reveal the structure that wasn't thought through.

Shadow path definitions:
- **Nil/empty input**: What happens if the input is null, empty, or missing? Does the system fail gracefully, fail silently, or fail with a confusing error?
- **Partial failure**: What happens if a multi-step operation completes partially? Is partial state preserved, rolled back, or left corrupted?
- **Upstream error**: What happens if an external dependency returns an error? Does the system propagate the error cleanly, absorb it silently, or crash?

*Red flag*: "We'll handle errors" without specifying what handling means for each shadow path.

**Q3: Synchronous vs. Asynchronous**

Which steps must be synchronous (user waits), which can be async (background)?

*Purpose*: This decision has major implications for user experience, system reliability, and complexity. Unnecessary synchronous operations slow users down and create single points of failure. Async operations without proper status signaling leave users confused.

*The full decision tree*:
- Does the user need the result to continue? → Must be sync
- Can the user continue without the result? → Can be async
- What does the user see while waiting (sync) or while processing (async)?
- What happens if the async job fails? How does the user find out?
- How does partial completion of an async job work?

**Q4: Failure Modes**

For each component, what happens when it fails?

*Purpose*: Failures are inevitable. The question is whether they're visible, graceful, and recoverable.

*For each component, the required analysis*:
```
What triggers failure:
What the system does when it fails:
What the user sees:
Is data lost? Y/N
Is the failure visible or silent?
Recovery path:
Time to recovery:
```

*The critical distinction*: Silent failures are categorically more dangerous than loud ones. A system that crashes visibly is easier to debug than one that continues operating with corrupted state.

**Q5: Edge Cases**

What inputs break the happy path?

*Purpose*: Edge cases are the discrepancy between what the system is designed to handle and what users actually do.

*Minimum 5 edge cases to name for any system*:
1. Scale edge: maximum realistic load
2. Empty state: zero items, no data, first-time user
3. Error state: the operation failed, what now?
4. Concurrent state: two users doing the same thing simultaneously
5. Stale state: data that was valid when loaded is no longer valid when submitted

*For UI systems, additional edge cases*:
- Double-click: what happens if the action is triggered twice?
- Navigate away mid-action: what state is preserved?
- Back button after completing an action: does it re-trigger?
- Slow connection: what does the user experience during a 5-second load?

**Q6: Trust Boundaries**

What is trusted? What must be validated?

*Purpose*: Security problems are almost always trust boundary violations — treating untrusted input as trusted. The question forces explicit declaration of what the system trusts and what it validates.

*Trust boundary analysis*:
- What comes from the user/client? (Must validate)
- What comes from authenticated internal services? (Validate but with reduced paranoia)
- What comes from the database? (Generally trusted, but verify schemas match expectations)
- What comes from third-party APIs? (Validate — external systems change without notice)

*Red flag*: "We trust the client" for any security-sensitive operation. "The ID comes from the URL" without authorization check.

**Q7: Observability**

How do you know if something is going wrong?

*Purpose*: A system without observability is a black box. When it fails (and it will), you won't know it failed until users complain, and you won't be able to diagnose it quickly.

*Three layers of observability*:
1. **Logs**: What events are logged? At what level? Can you trace a specific request through the system?
2. **Metrics**: What numbers are measured? What baselines exist? What triggers an alert?
3. **Traces**: For distributed systems, can you trace a request across services?

*Minimum observability for any new feature*:
- Error rate metric with alert threshold
- Success path logged at INFO level
- Error paths logged at ERROR level with context
- At least one operational metric (latency, throughput, or queue depth)

**Q8: Test Matrix**

What tests would give genuine confidence?

*Purpose*: A test matrix is a structured way of identifying coverage gaps. You can have 100 tests and still have zero coverage of the critical path.

*Test matrix format*:
```
Scenario | Test type | Exists | Confidence | Gap
Happy path | Integration | Yes | High | None
Null input | Unit | No | None | CRITICAL
Auth failure | Unit | Yes | Medium | None
Upstream timeout | Integration | No | None | HIGH
```

*Test quality calibration*:
- High confidence: test fails without the fix and passes with it
- Medium confidence: test passes with the fix but may not catch regressions
- Low confidence: test exercises the path but doesn't verify the outcome

### The Diagrams — Why Mandatory

Diagrams are mandatory because:
1. **Drawing forces specificity**: "The service communicates with the database" → how? What protocol? What queries? Through which interface?
2. **Diagrams reveal gaps**: If you can't draw a step, you haven't designed it yet
3. **Diagrams are reviewable**: You can check a diagram in a way you can't check prose
4. **Diagrams communicate assumptions**: Different reviewers often interpret prose differently; a diagram is less ambiguous

Required diagrams for any non-trivial system:
- Component diagram (what are the pieces, how do they connect)
- Data flow diagram (where does data enter, what transforms happen, where does it land)
- State machine diagram (what are the possible states, what transitions between them)

For code systems, also useful:
- Sequence diagram (which components call which other components, in what order)
- Dependency graph (what does each component depend on)

ASCII art is sufficient. The goal is to make the structure legible, not to produce a beautiful diagram.

---

## Skill 5: `retro` — Weekly Reflection

### The Core Framework

The retro is the only skill that looks backward. Every other skill asks "what should we do" — the retro asks "what actually happened, what does it mean, and what changes as a result."

GStack's retro was designed for engineering teams reviewing a week of commits. This port adapts it for **personal + project retrospective** — not just engineering work, but everything Steve is doing. The adaption changes the data sources (Obsidian memory files instead of git history) but preserves the analysis structure.

### The Data Layer — Memory-Driven Analysis

Unlike other skills, the retro starts with data collection, not questions. Before asking Steve anything, the skill should read:
- `memory/YYYY-MM-DD.md` files for the past 7 days
- `memory/active-tasks.md` for the current task list
- Prior retro notes in Obsidian (last 2) for trend comparison

Then synthesize: "From what I can see in your memory files, [here's what happened this week]. Does this match your experience?"

This serves two purposes:
1. It's faster — Steve doesn't have to reconstruct the week from memory
2. It's more accurate — what got written down is different from what felt salient in the moment

If memory files are sparse (common), the skill should ask Steve to self-report. The question: "Walk me through the week — what were you working on, and what actually got done?"

### Multi-Agent Contribution Tracking

In environments with multiple AI agents (e.g., OpenClaw with multiple instances or sub-agents), the retro should also track agent-level contributions:

- What did each agent complete this week?
- Which cron jobs ran successfully vs. failed?
- Sub-agent task completion rate
- Cross-agent collaboration moments (e.g., one agent's output fed another's input)

This extends the retro from single-person reflection to system-level reflection — appropriate when the "team" includes AI agents with autonomous task completion.

### The Three Analysis Layers

**Layer 1: What happened (descriptive)**
- What was completed
- What was started and stalled
- Where time actually went
- Surprises (unexpected problems or wins)

**Layer 2: What it means (analytical)**
- Is the pattern of completion healthy?
- Are the same items stalling repeatedly? (Signal: structural problem, not execution problem)
- Is time being spent on the highest-leverage things?
- What do the surprises reveal about incorrect assumptions?

**Layer 3: What changes (prescriptive)**
- The Three Lists: wins, improvements, next-week habits
- Explicit commitments, not vague intentions

### The Three Lists — Why This Structure

GStack's retro ends with three specific lists. This structure is not arbitrary:

**Top 3 Wins**: Requires specificity. Not "had a good week" — names exactly what was accomplished. This matters because people systematically undercount their progress. Writing wins explicitly creates an accurate record and corrects for negativity bias in self-assessment.

**Top 3 Improvements**: Requires actionability. Not "focus better" — names what specifically would change. Vague improvements don't change behavior. Specific ones do. "Stop checking messages during focused work blocks" is actionable. "Be more focused" is not.

**3 Habits for Next Week**: Requires concreteness. Habits are checkable commitments, not aspirations. "Meditate for 10 minutes each morning" is checkable. "Be more mindful" is not. The checkability is the accountability mechanism.

### Trend Analysis — What to Look For

When two or more prior retros are available, compare:

**Momentum trend**: Are completions increasing or decreasing? Is velocity going up or down? Declining momentum is usually a leading indicator of a problem — it shows up in the retro before it shows up in outcomes.

**Repeat stalls**: If the same item appears on the "stuck" list two weeks in a row, this is almost certainly a structural problem, not an execution problem. Name it explicitly. "This is the second week [X] has been stuck — this is a signal, not a coincidence. What's the root cause?"

**Focus ratio**: Is time being spent on the highest-leverage things? Compare intended vs. actual. Drift between intended and actual is common; acknowledging it is the first step to correcting it.

**Energy patterns**: When are energy peaks? When are troughs? If high-leverage work is consistently happening during low-energy times (and vice versa), that's an optimization opportunity.

### The Biggest Win and Biggest Learning

These two items are mandatory because they force qualitative reflection that the metrics don't capture:

**Biggest Win**: The specific thing you'd tell someone if asked "what was the best thing that happened this week?" Forces prioritization among completions.

**Biggest Learning**: "What do you know now that you didn't know Monday?" This question surfaces insights that aren't reflected in completions. Sometimes the most important week is one where very little was shipped but a fundamental assumption was found to be wrong.

---

## The Chain: How Skills Connect

```
New Idea
    ↓
[office-hours]
Creates: design note with problem statement, demand evidence, premises, approaches, recommendation
    ↓
[ceo-review]
Reads: office-hours note (problem statement, chosen approach)
Creates: strategic review note with scope decision, 10-star version, recommendation
    ↓
[eng-review]
Reads: office-hours + ceo-review notes (plan, scope, constraints)
Creates: technical review note with architecture, failure modes, test matrix
    ↓
[investigate] (when blocked at any stage)
Reads: description of the specific problem
Creates: investigation note with root cause, fix path
    ↓
[retro] (weekly)
Reads: all memory files + all prior skill outputs for the week
Creates: retrospective note with wins, improvements, habits
```

**Chain mechanism**: In GStack, the chain is automated through the file system — design docs are named and placed in locations that downstream skills scan automatically. In OpenClaw, the chain is maintained conversationally. When starting a downstream skill, ask: "Should I look at your last [upstream skill] note?" If yes, read the Obsidian note and use it as context.

**Why the chain matters**: Each skill assumes the previous one ran. eng-review assumes the problem is well-defined (office-hours) and the direction is set (ceo-review). Skipping upstream skills and jumping to downstream ones produces analysis that lacks grounding.

**When to skip steps**: If the idea is very simple and well-understood, skipping office-hours and going directly to ceo-review is fine. If the problem is purely technical with no strategic ambiguity, skipping ceo-review and going directly to eng-review is fine. The chain is a recommendation, not a requirement. But: never skip investigate when there's a genuine root-cause problem to trace.

---

## Cross-Skill Design Principles (Repeated in Every Skill)

These principles appear in every skill because they're foundational to how all five skills work:

### 1. One Question at a Time

Never batch questions. This is the single most important enforcement rule across all skills. Batching allows shallow answers. A single question in focus requires engagement.

### 2. Push Until Specific

"Interest" → "demand"  
"Categories" → "named people"  
"Progress" → "specific completions"  
Comfort = not deep enough. Always push.

### 3. Questions Are Diagnostic, Not Conversational

Every question tests a specific quality of thinking. Know what you're testing and what answer patterns indicate problems.

### 4. The Assignment

Every skill ends with one concrete next action. Not a strategy. Not a list of things to think about. One action.

### 5. Obsidian as the File System

Every skill saves to `obsidian/GStack/YYYY-MM-DD-[skill]-[slug].md`. The chain works because downstream skills can read upstream notes.

### 6. Status Reporting

Every session ends with: DONE / DONE_WITH_CONCERNS / BLOCKED / NEEDS_CONTEXT.

Not ceremony. Forces accountability for completeness.

### 7. Escape Hatch

Every skill must have an escape hatch. If the user says "just do it," expresses impatience, provides a fully formed plan, or explicitly asks to skip ahead — fast-track to the alternatives/solution phase.

The logic: the forcing questions exist to surface gaps in thinking. If the user's thinking is already clear (or they've been through this before), the questions become interrogation rather than diagnosis. An advisor who can't read the room is a bad advisor.

Implementation: if the user provides a complete, specific plan at any point, skip the remaining questions but still run the Premise Challenge and Alternatives phases. Even well-formed plans benefit from premise checking and forced alternatives.
