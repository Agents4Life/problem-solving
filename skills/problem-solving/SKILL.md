---
name: problem-solving
description: >
  Diagnose and solve software problems by routing them to the right mental model and resolution method.
  Classifies problems by type, selects the appropriate strategy, asks the minimum questions,
  and produces a concrete artifact with next steps.
  Triggers on: problem, idea, vision, bug, incident, decision, architecture, refactor,
  migration, stuck, unsure, how to approach, don't know where to start, troubleshooting,
  RCA, root cause, spike, trade-off, ADR, strategy.
---

# Problem Solving Router

Given a vision, idea, or problem, this skill answers:

1. **What type of problem is this?**
2. **What resolution method fits best?**
3. **What questions should I ask first?**
4. **What artifact should I produce?**
5. **How do I know I'm on the right track?**

## Operating Principles

- **Diagnose before prescribing.** Never jump to solutions without classifying the problem first.
- **Ask the minimum.** Each method has guiding questions — use them, don't invent new ones.
- **One method at a time.** Complex problems may need multiple passes, but start with one.
- **Produce artifacts, not just advice.** Every method produces a concrete output.
- **Match the user's language.** Technical terms stay in English when that's the standard.
- **Re-assess if stuck.** If the chosen method isn't yielding progress, re-classify.

## Step 1 — Classify the Problem

Read the user's description and classify into one of these categories:

| Signal | Category | Method |
|--------|----------|--------|
| "I have an idea but don't know where to start" | Fuzzy idea | Heuristic Resolution (Pólya) |
| "I want an app for X" | Unmodeled idea | Problem Modeling |
| "I don't know what the user needs" | User/Product uncertainty | Design Thinking / Double Diamond |
| "I think this could work" | Product hypothesis | Lean / Build-Measure-Learn |
| "Should I use X or Y?" | Technical decision | ADR + Trade-off Analysis |
| "This is too big" | Oversized problem | Divide and Conquer |
| "I keep doing the same thing" | Repetitive work | Knowledge Reuse / Templates |
| "It broke again" | Bug or incident | Debugging + Root Cause Analysis |
| "Is it working? How do I know?" | Operational uncertainty | Observability / SRE Thinking |
| "This code is a mess but it works" | Legacy / tech debt | Incremental Refactor / Strangler Fig |
| "I don't know if this is technically possible" | Technical unknown | Technical Spike |
| "I need to see if this feels right" | UX / interaction risk | Rapid Prototyping |
| "There are too many combinations/options" | Hard optimization | Heuristics / Approximation |
| "I've never seen this before" | Unknown problem | Problem Reduction |

If multiple signals match, pick the **highest-risk** one first. The skill can re-enter for secondary concerns.

## Step 2 — Apply the Resolution Method

### 1. Heuristic Resolution (Pólya)

**When:** The idea is fuzzy, the user doesn't know where to start.

**Process:**
1. Understand the problem — identify unknowns, data, and constraints
2. Devise a plan — connect to known patterns
3. Execute the plan — smallest possible step
4. Review — does the solution work? Does the method transfer?

**Guiding questions:**
- What do we want to achieve?
- What do we know?
- What don't we know?
- What constraints exist?
- What would a valid first version look like?
- How do we verify it works?

**Artifact:** `Problem Brief` — one-page document with goal, context, constraints, and first step.

---

### 2. Problem Modeling

**When:** The idea exists but hasn't been converted into a system yet.

**Process:**
1. Identify inputs and outputs
2. Define entities and relationships
3. Identify constraints and invariants
4. Find the core transformation
5. Map to a known problem type

**Guiding questions:**
- What are the inputs?
- What are the outputs?
- What entities exist?
- What constraints are there?
- What operation transforms input into output?
- What classic problem does this resemble?

**Artifact:** `Domain Model` — entities, relationships, input/output spec, core operation.

---

### 3. Design Thinking / Double Diamond

**When:** The main risk is not knowing what the user needs or what experience to design.

**Process:**
1. **Discover** — open up the problem space, research, empathize
2. **Define** — focus on the specific problem to solve
3. **Develop** — explore solutions, prototype
4. **Deliver** — test, refine, ship

**Guiding questions:**
- Who has this problem?
- How do they solve it today?
- What real pain exists?
- What alternatives do they have?
- What minimal solution could we test?

**Artifact:** `Problem Statement` + `Prototype` + `Validation Plan`.

---

### 4. Lean / Build-Measure-Learn

**When:** The problem is a hypothesis that needs testing fast.

**Process:**
1. State the hypothesis
2. Build the smallest experiment
3. Measure the result
4. Learn and decide

**Guiding questions:**
- What hypothesis am I testing?
- What's the smallest experiment?
- What metric validates or invalidates this?
- What will I learn even if it fails?

**Artifact:** `Experiment Card` — hypothesis, experiment, metric, learning log.

---

### 5. ADR + Trade-off Analysis

**When:** The problem is a technical or architectural decision.

**Process:**
1. State the decision to make
2. List options (2-5)
3. Evaluate trade-offs per option
4. Decide and document
5. Define reversal criteria

**Guiding questions:**
- What decision must we make?
- What context forces it?
- What options exist?
- What trade-offs does each have?
- What consequence do we accept?
- What would make us reverse this?

**Trade-off tensions to consider:**
- Speed vs. maintainability
- Cost vs. scalability
- Control vs. simplicity
- Native UX vs. cross-platform velocity
- Automation vs. human oversight
- Performance vs. clarity

**Artifact:** `ADR` (Architecture Decision Record):

```markdown
# ADR-NNN: Title

## Status
[Proposed | Accepted | Deprecated | Superseded by ADR-XXX]

## Context
What is the issue that we're seeing that is motivating this decision?

## Options
### Option A: ...
- Pros: ...
- Cons: ...

### Option B: ...
- Pros: ...
- Cons: ...

## Decision
What have we decided and why?

## Consequences
What becomes easier or harder after this decision?

## Reversal criteria
What would make us reconsider this decision?
```

---

### 6. Divide and Conquer

**When:** The vision is too large to tackle at once.

**Process:**
1. Break into independent parts
2. Identify dependencies between parts
3. Find the critical path (what unblocks the most)
4. Sequence milestones
5. Identify what can be parallelized or postponed

**Guiding questions:**
- What are the independent parts?
- Which part unblocks the others?
- What can be built in parallel?
- What can be postponed?

**Artifact:** `Work Breakdown` + `Milestone Plan` + `Dependency Map`.

---

### 7. Knowledge Reuse / Pattern Extraction

**When:** Repetitive work is detected — solving the same type of problem over and over.

**Process:**
1. Identify what's being repeated
2. Extract the common pattern
3. Generalize into a template or checklist
4. Document for future use

**Guiding questions:**
- What have I already solved before?
- What pattern repeats?
- What can I turn into a template?
- What knowledge should live in the wiki/docs?

**Artifact:** `Reusable Pattern` / `Prompt Template` / `Component Template` / `Checklist`.

---

### 8. Root Cause Analysis

**When:** Something fails or the same problem keeps recurring.

**Process:**
1. Define the symptom
2. Apply investigation method:
   - **5 Whys** — for simple/medium problems
   - **Fishbone (Ishikawa)** — when multiple causes are possible
   - **Fault Tree Analysis** — for complex/critical failures
3. Identify root cause(s)
4. Propose corrective action
5. Define prevention

**Guiding questions:**
- What did I expect?
- What actually happened?
- What changed recently?
- Where is the boundary between working/broken?
- How do I reproduce the error?

**Artifact:** `RCA Report` — symptom, investigation, root cause, corrective action, prevention checklist.

**Important:** 5 Whys should never end by blaming a person. Look for processes, conditions, or decisions to improve.

---

### 9. Observability / SRE Thinking

**When:** The question is about operation, reliability, or measuring success.

**Process:**
1. Define what "healthy" looks like
2. Identify signals (metrics, logs, events)
3. Set up alerts
4. Establish feedback loops
5. Learn from failures (postmortems)

**Guiding questions:**
- What signal indicates health?
- What event should I log?
- What metric matters?
- What alert would make sense?
- What did we learn from the last failure?

**Artifact:** `Observability Plan` — metrics, logs, alerts, SLOs, postmortem template.

---

### 10. Incremental Refactor / Strangler Fig

**When:** Existing code needs improvement but a full rewrite is too risky.

**Process:**
1. Identify what to replace
2. Build the new alongside the old
3. Route traffic/calls incrementally
4. Remove the old once the new is proven

**Guiding questions:**
- What part can I isolate?
- What do I replace first?
- What contract maintains compatibility?
- What old part still works fine?

**Artifact:** `Migration Plan` — phases, compatibility contracts, rollback strategy.

---

### 11. Technical Spike

**When:** Technical feasibility is uncertain.

**Process:**
1. Define the specific risk to clear
2. Set a time-box
3. Build the minimal proof
4. Document findings
5. Make a go/no-go decision

**Guiding questions:**
- What technical risk am I clearing?
- What's the minimal proof?
- How much time do I give it?
- What result lets me decide?

**Artifact:** `Technical Spike Report` — question, approach, findings, go/no-go decision.

---

### 12. Rapid Prototyping

**When:** The question is "does this feel right?" rather than "does this scale?"

**Process:**
1. Identify what must feel real
2. Fake everything else
3. Test with real users or yourself
4. Note what feels wrong
5. Iterate or discard

**Guiding questions:**
- What can I simulate without building everything?
- What screen demonstrates the idea?
- What part must feel real?
- What part can be fake for now?

**Artifact:** `Clickable Prototype` / `UI Spike` / `Fake Door Test`.

---

### 13. Debugging (Systematic)

**When:** Something doesn't work and the cause isn't obvious.

**Process:**
1. Reproduce the error reliably
2. Isolate the boundary (works above, breaks below)
3. Binary search through the code path
4. Fix the minimal root cause
5. Add regression test

**Guiding questions:**
- What did I expect?
- What actually happened?
- What changed recently?
- Where is the boundary between working and broken?
- What's the smallest isolated test case?

**Artifact:** `Bug Report` — reproduction steps, root cause, fix notes, regression test.

---

### 14. Heuristics / Approximation

**When:** The problem has too many combinations or no cheap perfect solution.

**Process:**
1. Determine if optimal is needed or "good enough"
2. Identify constraints that can be relaxed
3. Find special cases that are solvable
4. Apply practical heuristics

**Guiding questions:**
- Do I need the optimal solution or a good-enough one?
- What constraint can I relax?
- What special case can I solve?
- What practical heuristic works here?

**Artifact:** `Heuristic Strategy` — approach, constraints relaxed, expected accuracy.

---

### 15. Problem Reduction

**When:** The problem seems unique or unfamiliar.

**Process:**
1. Describe the problem abstractly
2. Check if it maps to a known category:
   - Search problem?
   - Sorting/classification?
   - Scheduling?
   - Recommendation?
   - Matching?
   - Flow?
   - State machine / transitions?
3. Apply known solutions from that category
4. Adapt to specific constraints

**Guiding questions:**
- Does this resemble search?
- Classification?
- Scheduling?
- Recommendation?
- Matching?
- Flow?
- State/transitions?

**Artifact:** `Problem Mapping` — original problem → known pattern → adapted solution.

---

## Step 3 — Produce the Output

After applying the method, produce a structured response:

```markdown
## Problem Classification
- **Type:** [category from Step 1]
- **Method:** [method applied]

## Why this method
[1-2 sentences explaining the fit]

## Key Questions
- [question 1]
- [question 2]
- [question 3]

## Artifact
[the concrete artifact for this method]

## Next Step
[one actionable next step]

## Risks
- [risk 1]
- [risk 2]

## Validation Metric
[how to know this is working]
```

## Step 4 — Re-assess if Stuck

If the chosen method isn't making progress after one full pass:

1. Stop and re-classify — maybe the problem type was wrong
2. Consider if it's actually a compound problem (needs two methods in sequence)
3. Check if the real blocker is emotional/organizational, not technical
4. Apply **Heuristic Resolution (Pólya)** as fallback — it's the most general method

## Common Sequences

Some problems naturally chain methods:

| Situation | Sequence |
|-----------|----------|
| New product idea | Fuzzy Idea → Problem Modeling → Design Thinking → Lean Experiment |
| Technical migration | ADR → Divide and Conquer → Strangler Fig → Observability |
| Recurring bug | Debugging → Root Cause Analysis → Knowledge Reuse |
| Large vision | Fuzzy Idea → Divide and Conquer → [per-part method] |
| Legacy system | ADR → Strangler Fig → Observability → Incremental Refactor |

## Rules

- Never jump to implementation without classifying first.
- Always produce a concrete artifact — advice alone is not enough.
- If uncertain between two methods, explain both and let the user choose.
- Respect time constraints — if the user needs a quick answer, use Greedy/Heuristic approach.
- When a problem triggers strong opinions, switch to Trade-off Analysis to keep it structured.
- Never blame people in RCA — look for systemic causes.

## Language

- Match the user's language for communication.
- Keep technical terms in English when that is the standard.
- Artifact templates in English by default (universal in engineering).
