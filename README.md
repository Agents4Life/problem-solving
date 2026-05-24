# Problem Solving Router

Open-source AI agent skill that diagnoses software problems and routes them to the right mental model and resolution method.

Compatible with any agent that supports `SKILL.md` (OpenClaw, Claude Code, Codex, Cursor, and 50+ more).

## Install

```bash
npx skills add VanessaPellegrini/problem-solving
```

## What it does

Given a vision, idea, bug, decision, or problem, the skill:

1. **Classifies** the problem type
2. **Selects** the appropriate resolution method
3. **Guides** with minimum questions
4. **Produces** a concrete artifact
5. **Suggests** the next action

## 15 Resolution Methods

| # | Method | When to use | Artifact |
|---|--------|-------------|----------|
| 1 | Heuristic Resolution (Pólya) | Fuzzy idea, don't know where to start | Problem Brief |
| 2 | Problem Modeling | Idea exists but not modeled as a system | Domain Model |
| 3 | Design Thinking / Double Diamond | User/product uncertainty | Problem Statement + Prototype |
| 4 | Lean / Build-Measure-Learn | Product hypothesis to test | Experiment Card |
| 5 | ADR + Trade-off Analysis | Technical or architectural decision | ADR |
| 6 | Divide and Conquer | Vision too large | Work Breakdown + Milestone Plan |
| 7 | Knowledge Reuse | Repetitive work detected | Template / Pattern |
| 8 | Root Cause Analysis | Recurring bug or incident | RCA Report |
| 9 | Observability / SRE | Operational uncertainty | Observability Plan |
| 10 | Incremental Refactor / Strangler Fig | Legacy / tech debt | Migration Plan |
| 11 | Technical Spike | Technical feasibility unknown | Spike Report |
| 12 | Rapid Prototyping | UX / interaction validation | Prototype |
| 13 | Systematic Debugging | Something doesn't work | Bug Report |
| 14 | Heuristics / Approximation | Too many combinations, no cheap optimal | Heuristic Strategy |
| 15 | Problem Reduction | Unfamiliar or unique problem | Problem Mapping |

## How it works

```
User describes problem
        ↓
Skill classifies type
        ↓
Skill selects method
        ↓
Skill asks guiding questions
        ↓
Skill produces artifact
        ↓
Skill suggests next step + validation metric
```

## Example

```
You: "I want to build a personal finance app but I don't know where to start"
Agent: [loads problem-solving]
Agent: "Problem type: Fuzzy idea → Heuristic Resolution"
Agent: "Let's clarify: What do you want to achieve? What do you know? What constraints exist?"
Agent: [produces Problem Brief with goal, context, constraints, and first step]
```

```
You: "Should I use PostgreSQL or SQLite for this offline-first app?"
Agent: "Problem type: Technical decision → ADR + Trade-off Analysis"
Agent: [produces ADR with options, trade-offs, decision, and reversal criteria]
```

```
You: "This bug keeps coming back in production"
Agent: "Problem type: Recurring bug → Debugging + Root Cause Analysis"
Agent: [produces RCA Report with 5 Whys, corrective action, and prevention checklist]
```

## Common Method Sequences

| Situation | Sequence |
|-----------|----------|
| New product idea | Fuzzy Idea → Modeling → Design Thinking → Lean |
| Technical migration | ADR → Divide and Conquer → Strangler Fig → Observability |
| Recurring bug | Debugging → RCA → Knowledge Reuse |
| Large vision | Fuzzy Idea → Divide and Conquer → per-part method |
| Legacy system | ADR → Strangler Fig → Observability → Refactor |

## Philosophy

> Don't prescribe before diagnosing. First decide **how to think** about the problem, then help build the solution.

The skill doesn't generate code directly. It acts as a **strategy diagnostician** — selecting the right mental model, asking the right questions, and producing the right artifact before any implementation begins.

## Contributing

Open project. Contributions welcome.

## License

MIT

---

_Made with curiosity by Van & Purim 🐶_
