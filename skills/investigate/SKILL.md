---
name: investigate
version: 1.0.0
description: |
  Systematic root-cause debugging. Iron Law: no fixes without investigation first.
  Works for any domain — code bugs, system failures, personal problems, process
  breakdowns, strategic mistakes. Four phases: collect symptoms, match patterns,
  form hypothesis, confirm before fixing.

  Use when asked to: "investigate this", "why is [X] happening", "debug [X]",
  "root cause analysis", "I can't figure out why [X]", "something's wrong with
  [X]", "help me trace what's happening", "systematic debugging".
triggers:
  - "investigate"
  - "debug"
  - "root cause"
  - "why is this happening"
  - "I can't figure out"
  - "something's wrong"
  - "why isn't this working"
  - "help me trace"
  - "figure out what's wrong"
---

# Systematic Debugging

## The Iron Law

**NO FIXES WITHOUT ROOT CAUSE INVESTIGATION FIRST.**

This is not a process preference — it's a theory about why debugging usually fails.

The common failure mode: see symptom → form hypothesis → apply fix → symptom goes away temporarily → new symptom appears → apply another fix → whack-a-mole indefinitely for hours or days.

This loop fails because fixes without root cause are fixes to symptoms, not causes. The underlying problem remains. Each fix patches over it with new complexity, making the next diagnosis harder.

The Iron Law breaks the loop by making a single rule absolute: before any fix, you must have a confirmed root cause hypothesis. Not a plausible hypothesis. A confirmed one.

**Domain-agnostic**: The Iron Law applies to code bugs, failed systems, recurring personal patterns, organizational dysfunction, strategic mistakes — any situation where something isn't working and the cause is unclear. The framework doesn't change; only the vocabulary does.

---

## The Completeness Principle

Surface-level investigation and deep investigation take the same conversation. Go deep. Don't stop at the first plausible hypothesis — test it. Don't accept "probably" when evidence is available.

---

## Phase 1: Symptom Collection — The Three Required Pieces

**Do NOT form a hypothesis until all three are in hand.** Premature hypotheses anchor thinking — you start interpreting subsequent evidence in favor of the hypothesis rather than objectively.

Collect these ONE question at a time:

**1. The symptom — precisely described, not interpreted:**

> "Describe exactly what's happening. What do you observe? What were you expecting instead?"

Good: "The API call returns a 401 status with no response body."
Bad: "Authentication is broken." (This is already an interpretation.)

Force precision. "It's not working" → "What specifically is not working? What do you see? What do you expect to see instead?"

**2. Onset — was it working before? What changed?**

> "Was this working before? If so, when did it stop? What changed around that time?"

Regressions are categorically easier to debug than novel failures because the root cause is in the change. If something was working yesterday and broken today, the root cause is in what changed.

If it has never worked: that's different. Ask "Is this new code, or has this path always existed?"

**3. Reproduction — reliable or intermittent?**

> "Can you make it happen again deliberately? Or does it happen randomly?"

Intermittent failures are a category signal: they almost always indicate race conditions, state corruption, or external dependency instability. Reliable reproduction means deterministic root cause.

If intermittent: "When it happens, is there anything in common — time of day, load, specific inputs, specific sequence of actions?"

---

## Phase 2: Pattern Matching — The Known Failure Categories

Before doing any original analysis, check whether the symptoms match known patterns. Most failures are instances of a small number of recurring categories. Matching the pattern narrows the hypothesis space dramatically.

| Pattern | Signature | Diagnostic question |
|---|---|---|
| **Race condition** | Intermittent, timing-dependent, more frequent under load | Does frequency increase when multiple things happen at once? |
| **Missing context/data** | Null errors, empty results, "undefined" | What data should be present but isn't? Where should it come from? |
| **Configuration drift** | Works in env A, fails in env B | What's different between the two environments? |
| **Integration failure** | Timeout, unexpected response from external system | Has the external system changed recently? Is it healthy? |
| **Wrong mental model** | Results consistently wrong in a non-random direction | Is the problem different from what was assumed from the start? |
| **State corruption** | Inconsistent data, partial writes, old data showing up | Has something left the system in a partial state? |
| **Order/timing dependency** | Works when done in one sequence, fails in another | Is there a required ordering that isn't being enforced? |
| **Threshold/scale issue** | Works at low volume, fails at high volume | Is there a limit being hit that wasn't expected? |

State the pattern match: "This looks like [pattern] because [specific signature match]. The diagnostic question is [question]."

If symptoms don't clearly match any pattern: state that too. "This doesn't match a clear pattern, which means we need to be more methodical."

---

## Phase 3: Root Cause Hypothesis

State a specific, testable hypothesis:

> "My hypothesis: the root cause is [X] because [Y]. The evidence that would confirm this is [Z]. The evidence that would refute this is [W]."

**Quality check for the hypothesis:**

1. **Is it specific?** Not "something is wrong with auth" — specific: "The JWT token is missing the `sub` claim when the user has an org affiliation, causing the auth check to fail."

2. **Is it testable?** Can you design an experiment that confirms or refutes it? If you can't describe what evidence would prove it wrong, the hypothesis isn't a hypothesis — it's a belief.

3. **Does it explain all the symptoms?** If hypothesis X is true, do all observed symptoms follow from it? If some symptoms are unexplained by the hypothesis, it may be incomplete.

4. **Is it the cause, not a symptom?** "The error message says Y" is not a root cause — it's another symptom. Keep tracing back until you reach the cause that has no parent cause in this causal chain.

Ask: "Does this match what you're seeing? What evidence would help us confirm or rule this out?"

---

## Phase 4: The Iron Law Check — Confirm Before Fixing

Before proposing any fix:

> "Do we have confirmed evidence that [hypothesis] is the root cause? Or do we have a plausible hypothesis that still needs to be tested?"

**Confirmed** = evidence directly demonstrates the root cause, not just evidence consistent with it.

Examples:
- "We can trigger the bug by removing [X]" → confirmed
- "The bug disappears when [X] is present" → confirmed
- "The error message matches what [hypothesis] would produce" → not confirmed (consistent, not proven)
- "It seems like it would be [hypothesis]" → not confirmed

If not confirmed, determine how to confirm: "To confirm this hypothesis, we need to [specific test or observation]."

Do not proceed to Phase 5 until confirmed.

### The 3-Strike Rule

**After three failed hypotheses, STOP. Do not generate a fourth.**

Three failed hypotheses is evidence — usually that the problem is at a different layer than assumed:
- Three code-level hypotheses fail → investigate infrastructure or configuration
- Three technical hypotheses fail → question the mental model of the system
- Three implementation hypotheses fail → question the architecture

When 3 strikes are reached:

> "Three hypotheses tested and none match. This usually means we're looking at the wrong layer. Let's step back.
>
> A) New angle: I think the problem is actually in [completely different layer] — here's why.
> B) Need more information: I can't proceed without knowing [specific thing].
> C) This may be architectural: the problem isn't a bug, it's a design issue that requires rethinking [specific thing]."

Do not guess a fourth hypothesis. Choose A, B, or C.

---

## Phase 5: Solution Path

Once root cause is confirmed:

**1. Fix the root cause, not the symptom.**
Describe exactly what needs to change, referenced to the specific root cause. The fix should eliminate the cause, not suppress the symptom.

**2. Minimal blast radius.**
The fix should touch as few things as possible. If the fix touches more than 3-5 things, ask: is the root cause really at this layer, or is the fix compensating for a design issue?

**3. The verification evidence.**
Before implementing: "After this fix is applied, here is the specific evidence we should see that confirms it worked: [evidence]."

Not "it should work" — specific evidence. If the bug was a 401 return, the evidence is "the API call returns 200." If the bug was data corruption, the evidence is "the data check returns clean."

**4. What could go wrong with the fix.**
Every fix has risks. Name them: "The risk with this fix is [X]. Watch for [Y]."

---

## Phase 6: Debug Report

Save to Obsidian and present:

Path: `obsidian/GStack/YYYY-MM-DD-investigate-[slug].md`

```markdown
# Investigation: [Problem Description]
Date: YYYY-MM-DD
Status: DONE | DONE_WITH_CONCERNS | BLOCKED

## Symptom (precisely described)
[What is observed, what is expected — precise, not interpreted]

## Onset
[When started / what changed / regression or new]

## Reproduction
[Reliable / intermittent — how to trigger]

## Pattern Match
[Which known failure pattern this matches, and why]

## Hypotheses Tested
1. [Hypothesis 1] — RULED OUT because [evidence]
2. [Hypothesis 2] — RULED OUT because [evidence]  
3. [Root cause hypothesis] — CONFIRMED because [specific evidence]

## Root Cause
[The confirmed root cause — specific, traced to origin]

## Fix
[What specifically needs to change and why it addresses the root cause, not the symptom]

## Verification
[Specific evidence that will confirm the fix worked]

## Blast Radius
[What else this fix might affect]

## What Could Go Wrong
[Risks of the fix itself]
