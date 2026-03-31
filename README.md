# claude-code-boss-mode

> Not a Claude Code clone. A boss layer for Claude Code.
>
> If Claude Code is the engineer, this plugin is the boss.

## What This Does

**Boss Mode for Claude Code** is a ruthless decision-making framework that forces three questions before any engineering work proceeds:

1. **Is this worth doing at all?** (ROI gate)
2. **What is the minimum shippable version?** (scope gate)  
3. **What should we explicitly NOT do?** (cut gate)

It combines three boss perspectives—CEO, Engineering Manager, PM—into a structured evaluation system that catches overengineering, kills scope creep, and pushes for shippable solutions.

## The Problem

Claude Code is an incredible engineer. But engineers optimize for correctness, completeness, and elegance. They do not optimize for shipping speed, scope control, or business outcomes.

- Engineers propose massive refactors "while we are at it"
- Engineers build perfect abstractions for hypothetical future needs
- Engineers want to make every system resilient, scalable, and documented
- Engineers rarely ask "do we actually need this?"

A boss asks that question constantly.

## The Solution

Four slash commands that slot directly into your Claude Code workflow:

| Command | Use Case | Output |
|---------|----------|--------|
| `/boss` | Evaluate an idea before coding | SHIP / REVISIT / KILL with cuts |
| `/boss-pr` | Review code like a boss | MERGE / REVISE / CLOSE with red flags |
| `/boss-plan` | Cut scope from a roadmap | Must-have → Nice-to-have → Cut |
| `/boss-roast` | Honest feedback on overengineering | Savage but actionable |

Plus one meta-command:

| Command | Use Case |
|---------|----------|
| `/boss-vs-engineer` | Dual-agent debate: engineer proposes, boss cuts, both negotiate |

## Examples

### Before: Engineer Proposes

```
User: "Build a caching layer for this API"

Engineer: "I will build Redis with:
- Connection pooling
- Automatic key expiration
- Cache invalidation strategies
- Distributed tracing
- Memory limit alerts
- Metrics collection
Estimated: 3 weeks"
```

### After: Boss Steps In

```
User: "Build a caching layer for this API"

Engineer: [same proposal as above]

/boss-pr (or /boss-vs-engineer)

Boss: "REVISE

WHAT THIS ACTUALLY DOES:
Add 3 weeks of infrastructure for a problem you haven't proven exists.

RED FLAGS:
- No benchmark showing the API is slow
- No monitoring of cache hit rate
- No rollback story if Redis breaks
- Over-engineered for potential future scale

SHIP BLOCKERS:
- Benchmark the current API. Is it actually slow?
- Define the metric: what hit rate makes this worth it?
- Rollback plan: how do we remove Redis without breaking things?

MINIMUM VERSION:
Simple in-process LRU cache (100 lines). Measure the impact. 
If cache hits are >60%, then consider Redis."
```

Result: 3 weeks → 3 days. Real impact measurement upfront.

## Three Boss Perspectives

### CEO Boss

Optimizes for: **speed to user, demo-ability, market timing**

- "Can I show a customer this next week?"
- Hates: infrastructure work, premature optimization, refactoring that delays shipping
- Loves: rough features that work, clear next iteration

### Engineering Manager Boss

Optimizes for: **risk, on-call sanity, reversibility**

- "What happens when this breaks at 3am?"
- Hates: undocumented implicit contracts, no rollback story, cutting corners
- Loves: boring, conservative, recoverable systems

### PM Boss

Optimizes for: **scope, timeline, measurable outcomes**

- "How do I know this worked? What metric moves?"
- Hates: backend-only work users never see, over-scoped MVPs
- Loves: clear success metrics, milestone-gated scope

## Core Philosophy

Boss Mode is not role-play. It is a structured decision framework.

1. **Every output must contain at least one cut.** A boss who approves everything is not a boss.
2. **Be specific.** "Remove the caching layer" not "simplify the architecture".
3. **Name the failure mode.** "If this breaks at 3am, users cannot log in" not "there is risk".
4. **Read the actual code.** Never hallucinate about diffs you have not seen.
5. **Verdicts are binary.** SHIP/REVISIT/KILL or MERGE/REVISE/CLOSE. No custom verdicts.

## How to Use

### Before Starting a Feature

```
/boss "Build an advanced analytics dashboard"

Boss: REVISIT

WHY NOW:
You haven't validated that users care about analytics.

MINIMUM SHIPPABLE VERSION:
Three charts: active users, retention, top features. Read-only, no export.

CUT LIST:
- Real-time updates (use daily snapshot)
- Custom date ranges (just 30/90 days)
- Drill-down drill-down (too many clicks)

RISK:
If nobody uses it, you wasted 2 weeks. Validate with 5 users first.
```

### Before Merging a PR

```
/boss-pr

Boss: MERGE

WHAT THIS ACTUALLY DOES:
Adds rate limiting to the auth endpoint.

GOOD PARTS:
Clean implementation, well-tested, rollback story is clear.
```

Or:

```
/boss-pr

Boss: REVISE

WHAT THIS ACTUALLY DOES:
Adds a caching abstraction to every database query.

RED FLAGS:
- Adds 800 lines of code for a problem you haven't measured
- Cache invalidation logic is implicit and fragile
- No metrics on cache hit rate

SHIP BLOCKERS:
1. Remove the generic cache abstraction. Start with one specific query.
2. Add cache hit/miss metrics.
3. Define invalidation strategy explicitly.
```

### During Planning

```
/boss-plan [paste your roadmap]

Boss: MUST-HAVE (v1)
1. User sign-up
2. Create posts
3. Share with link

NICE-TO-HAVE (v2)
- Post drafts
- Scheduled posts
- Email notifications

CUT NOW
- Real-time collaboration (GitHub and Figma do this; do not compete)
- Admin analytics dashboard (gather data via CSV export instead)
```

## Installation

### Claude Code

```bash
mkdir -p .claude/skills
git clone https://github.com/huyuelin/claude-code-boss-mode .claude/skills/boss-mode
```

### OpenClaw

```bash
git clone https://github.com/huyuelin/claude-code-boss-mode ~/.openclaw/workspace/skills/boss-mode
```

## Project Structure

```
claude-code-boss-mode/
├── SKILL.md                      # Entry point (this doc)
├── README.md                     # You are here
├── commands/
│   ├── boss.md                   # /boss prompt template
│   ├── boss-pr.md                # /boss-pr prompt template
│   └── boss-plan.md              # /boss-plan prompt template
├── agents/
│   ├── ceo-boss.md               # CEO perspective
│   ├── eng-manager-boss.md       # EM perspective
│   └── pm-boss.md                # PM perspective
├── bosses/
│   └── example_startup_ceo/      # Example custom boss
│       ├── persona.md            # Decision style
│       ├── context.md            # Company context
│       └── meta.json             # Metadata
├── prompts/
│   ├── boss_builder.md           # Template for /create-boss
│   └── roast_engine.md           # Template for /boss-roast
├── skills/
│   └── boss-mode/
│       └── SKILL.md              # Bundled skill registry entry
└── LICENSE                       # MIT
```

## Why This Matters

Software teams ship late because of scope creep and overengineering. Not because engineers are lazy. Because nobody says "stop".

A boss layer that runs **before** major decisions accelerates shipping by 2-3x:

- Fewer overengineered solutions that need to be ripped out
- Clearer priorities (must-have vs. nice-to-have)
- Fewer surprises on launch day

Boss Mode automates the ruthless questions.

## Creating Custom Bosses

You can create a custom boss profile tailored to your team's culture:

```
/create-boss

What kind of boss are you distilling?
> My CTO at my startup

[similar to /create-colleague]

Generated: /bosses/my_startup_cto
Use: /my_startup_cto or /boss-pr my_startup_cto
```

Custom bosses inherit the decision framework but with your company's OKRs, risk tolerance, and style.

## Core Principles

1. **Shipping beats perfection.** A rough feature in users' hands is better than a perfect feature in development.
2. **Measurement comes first.** Guess later. Measure now.
3. **Scope is the enemy.** Cut scope before it kills the timeline.
4. **Risk is a business decision.** Not an engineering problem.
5. **Simplicity scales.** Complex systems are hard to operate. Start boring.

## License

MIT License © [huyuelin](https://github.com/huyuelin)

---

**Not a Claude Code clone. A boss layer for Claude Code.**

If Claude Code is the engineer, this plugin is the boss.
