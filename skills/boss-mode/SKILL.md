---
name: boss-mode
description: Ruthless decision framework for Claude Code. /boss to evaluate ideas, /boss-pr to review PRs, /boss-plan to cut scope.
version: "1.0.0"
user-invocable: true
---

# Boss Mode Skill Library

This directory contains the bundled Boss Mode skill definitions for use within Claude Code.

See the main SKILL.md in the parent directory for detailed documentation and usage.

## Quick Reference

- `/boss` - Evaluate idea (SHIP/REVISIT/KILL)
- `/boss-pr` - Review PR (MERGE/REVISE/CLOSE)
- `/boss-plan` - Cut scope from roadmap
- `/boss-roast` - Savage feedback on overengineering
- `/boss-vs-engineer` - Dual-agent debate

## Three Perspectives

- CEO Boss: speed to user, demo-ability
- EM Boss: risk, on-call sanity, reversibility
- PM Boss: scope, timeline, metrics

Default: blended verdict from all three.

Specify with `/boss ceo`, `/boss-pr em`, etc.
