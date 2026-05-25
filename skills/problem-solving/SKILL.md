---
name: problem-solving
description: >
  Route problems to the right mental model. Classify -> select strategy -> ask minimum questions -> produce artifact.
  Triggers on: problem, idea, vision, bug, incident, decision, architecture, refactor,
  migration, stuck, unsure, how to approach, don't know where to start, troubleshooting,
  RCA, root cause, spike, trade-off, ADR, strategy.
---

# Problem Solving Router

Given a vision, idea, or problem, answer:

1. **What type of problem?**
2. **What method fits?**
3. **What questions to ask first?**
4. **What artifact to produce?**
5. **How to know if on right track?**

## Operating Principles

- Diagnose before prescribing. Classify first.
- Ask minimum. Use each method's guiding questions.
- One method at a time. Complex problems may need multiple passes.
- Produce artifacts, not just advice.
- Match user's language. Technical terms in English when standard.
- Re-assess if stuck.

## Step 1 — Classify

| Signal | Category | Method |
|--------|----------|--------|
| "I have an idea but don't know where to start" | Fuzzy idea | Heuristic Resolution (Polya) |
| "I want an app for X" | Unmodeled idea | Problem Modeling |
| "I don't know what the user needs" | User/Product uncertainty | Design Thinking / Double Diamond |
| "I think this could work" | Product hypothesis | Lean / Build-Measure-Learn |
| "Should I use X or Y?" | Technical decision | ADR + Trade-off Analysis |
| "This is too big" | Oversized problem | Divide and Conquer |
| "I keep doing the same thing" | Repetitive work | Knowledge Reuse / Templates |
| "It broke again" | Bug or incident | Debugging + RCA |
| "Is it working? How do I know?" | Operational uncertainty | Observability / SRE |
| "This code is a mess but it works" | Legacy / tech debt | Incremental Refactor / Strangler Fig |
| "I don't know if this is technically possible" | Technical unknown | Technical Spike |
| "I need to see if this feels right" | UX / interaction risk | Rapid Prototyping |
| "There are too many combinations/options" | Hard optimization | Heuristics / Approximation |
| "I've never seen this before" | Unknown problem | Problem Reduction |

Multiple signals match -> pick **highest-risk** first. Re-enter for secondary concerns.

## Step 2 — Apply Method

### 1. Heuristic Resolution (Polya)

**When:** Fuzzy idea, user doesn't know where to start.

**Process:** Understand (unknowns, data, constraints) -> Plan (connect known patterns) -> Execute (smallest step) -> Review (works? transfers?)

**Questions:** What to achieve? What known? What unknown? What constraints? Valid first version? How verify?

**Artifact:** `Problem Brief` — goal, context, constraints, first step.

---

### 2. Problem Modeling

**When:** Idea exists, not yet converted to system.

**Process:** Identify inputs/outputs -> Define entities/relationships -> Identify constraints/invariants -> Find core transformation -> Map to known problem type.

**Questions:** Inputs? Outputs? Entities? Constraints? Core operation? Classic problem it resembles?

**Artifact:** `Domain Model` — entities, relationships, I/O spec, core operation.

---

### 3. Design Thinking / Double Diamond

**When:** Main risk = not knowing what user needs.

**Process:** Discover (research, empathize) -> Define (focus specific problem) -> Develop (explore solutions, prototype) -> Deliver (test, refine, ship).

**Questions:** Who has this problem? How solve today? Real pain? Alternatives? Minimal solution to test?

**Artifact:** `Problem Statement` + `Prototype` + `Validation Plan`.

---

### 4. Lean / Build-Measure-Learn

**When:** Hypothesis needing fast test.

**Process:** State hypothesis -> Build smallest experiment -> Measure -> Learn + decide.

**Questions:** What hypothesis? Smallest experiment? Validating metric? Learn even if fails?

**Artifact:** `Experiment Card` — hypothesis, experiment, metric, learning log.

---

### 5. ADR + Trade-off Analysis

**When:** Technical or architectural decision.

**Process:** State decision -> List options (2-5) -> Evaluate trade-offs -> Decide + document -> Define reversal criteria.

**Questions:** What decision? What context forces it? Options? Trade-offs each? Consequence accepted? Reversal trigger?

**Trade-off tensions:** Speed vs maintainability, Cost vs scalability, Control vs simplicity, Native UX vs cross-platform, Automation vs human oversight, Performance vs clarity.

**Artifact:** `ADR`:

```markdown
# ADR-NNN: Title

## Status
[Proposed | Accepted | Deprecated | Superseded by ADR-XXX]

## Context
What issue motivates this decision?

## Options
### Option A: ...
- Pros: ... Cons: ...
### Option B: ...
- Pros: ... Cons: ...

## Decision
What decided and why?

## Consequences
Easier or harder after this?

## Reversal criteria
What would trigger reconsideration?
```

---

### 6. Divide and Conquer

**When:** Vision too large to tackle at once.

**Process:** Break into independent parts -> Identify dependencies -> Find critical path -> Sequence milestones -> Identify parallelizable/postponable.

**Questions:** Independent parts? Which unblocks others? Parallelizable? Postponable?

**Artifact:** `Work Breakdown` + `Milestone Plan` + `Dependency Map`.

---

### 7. Knowledge Reuse / Pattern Extraction

**When:** Repetitive work detected.

**Process:** Identify repetition -> Extract pattern -> Generalize to template/checklist -> Document.

**Questions:** Solved before? Pattern repeats? Template material? What belongs in wiki/docs?

**Artifact:** `Reusable Pattern` / `Prompt Template` / `Component Template` / `Checklist`.

---

### 8. Root Cause Analysis

**When:** Something fails or same problem recurs.

**Process:** Define symptom -> Investigate (**5 Whys** for simple, **Fishbone** for multiple causes, **Fault Tree** for complex/critical) -> Root cause(s) -> Corrective action -> Prevention.

**Questions:** Expected vs actual? What changed? Working/broken boundary? Reproduction steps? Smallest isolated test?

**Artifact:** `RCA Report` — symptom, investigation, root cause, corrective action, prevention checklist.

**Important:** 5 Whys never blame people. Look for systemic causes.

---

### 9. Observability / SRE Thinking

**When:** Question about operation, reliability, or measuring success.

**Process:** Define "healthy" -> Identify signals (metrics, logs, events) -> Set alerts -> Establish feedback loops -> Learn from failures (postmortems).

**Questions:** Health signal? Events to log? Key metric? Useful alert? Learned from last failure?

**Artifact:** `Observability Plan` — metrics, logs, alerts, SLOs, postmortem template.

---

### 10. Incremental Refactor / Strangler Fig

**When:** Existing code needs improvement, full rewrite too risky.

**Process:** Identify replacement target -> Build new alongside old -> Route traffic/calls incrementally -> Remove old once proven.

**Questions:** What to isolate? Replace first? Compatibility contract? What old part still works?

**Artifact:** `Migration Plan` — phases, compatibility contracts, rollback strategy.

---

### 11. Technical Spike

**When:** Technical feasibility uncertain.

**Process:** Define risk -> Time-box -> Build minimal proof -> Document -> Go/no-go.

**Questions:** Technical risk? Minimal proof? Time budget? Decision-enabling result?

**Artifact:** `Technical Spike Report` — question, approach, findings, go/no-go.

---

### 12. Rapid Prototyping

**When:** "Does this feel right?" > "Does this scale?"

**Process:** Identify what must feel real -> Fake everything else -> Test with users -> Note what feels wrong -> Iterate or discard.

**Questions:** Simulate without building everything? Demo screen? Must-feel-real part? Can-be-fake part?

**Artifact:** `Clickable Prototype` / `UI Spike` / `Fake Door Test`.

---

### 13. Debugging (Systematic)

**When:** Something broken, cause not obvious.

**Process:** Reproduce reliably -> Isolate boundary (works above, breaks below) -> Binary search code path -> Fix minimal root cause -> Add regression test.

**Questions:** Expected vs actual? What changed? Working/broken boundary? Smallest isolated test?

**Artifact:** `Bug Report` — reproduction steps, root cause, fix notes, regression test.

---

### 14. Heuristics / Approximation

**When:** Too many combinations, no cheap perfect solution.

**Process:** Optimal or good-enough? -> Relax constraints -> Find solvable special cases -> Apply practical heuristics.

**Questions:** Optimal needed? Relaxable constraint? Solvable special case? Practical heuristic?

**Artifact:** `Heuristic Strategy` — approach, constraints relaxed, expected accuracy.

---

### 15. Problem Reduction

**When:** Problem seems unique or unfamiliar.

**Process:** Describe abstractly -> Map to known category (search? sorting? scheduling? recommendation? matching? flow? state machine?) -> Apply known solutions -> Adapt to constraints.

**Artifact:** `Problem Mapping` — original -> known pattern -> adapted solution.

---

## Step 3 — Produce Output

```markdown
## Problem Classification
- **Type:** [category]
- **Method:** [method applied]

## Why this method
[1-2 sentences]

## Key Questions
- [Q1]
- [Q2]
- [Q3]

## Artifact
[concrete artifact]

## Next Step
[one actionable step]

## Risks
- [risk 1]
- [risk 2]

## Validation Metric
[how to know it works]
```

## Step 4 — Re-assess if Stuck

If method stalls after one pass:
1. Re-classify — maybe wrong problem type
2. Compound problem? (needs two methods in sequence)
3. Real blocker emotional/organizational, not technical?
4. Fallback: Heuristic Resolution (Polya) — most general

## Common Sequences

| Situation | Sequence |
|-----------|----------|
| New product idea | Fuzzy Idea -> Problem Modeling -> Design Thinking -> Lean |
| Technical migration | ADR -> Divide and Conquer -> Strangler Fig -> Observability |
| Recurring bug | Debugging -> RCA -> Knowledge Reuse |
| Large vision | Fuzzy Idea -> Divide and Conquer -> [per-part method] |
| Legacy system | ADR -> Strangler Fig -> Observability -> Incremental Refactor |

## Rules

- Classify before implementing
- Always produce concrete artifact
- Uncertain between two methods -> explain both, let user choose
- Time-constrained user -> use Greedy/Heuristic approach
- Strong opinions triggered -> switch to Trade-off Analysis
- Never blame people in RCA -> find systemic causes

## Language

- Match user's language
- Technical terms in English when standard
- Artifact templates in English (universal in engineering)
