# Agent Phalanx

> **Advanced Framework**: This builds on all previous frameworks. If you're just starting out, master the basics first and return here when you're ready to level up.

Each AI model has its own specialty. Combined strategically, they form a phalanx—a formation where different units cover each other's weaknesses.

## The Formation

In a Greek phalanx, shields protect while spears attack. In my AI workflow:

- **Spears (Execution)**: Claude Opus 4.6 (1M) works autonomously through multi-PR projects—exploring, planning, implementing, opening PRs, and iterating through CI
- **Shields (Analysis)**: GPT-5.4 High performs structured code review and architecture analysis via Codex MCP delegation, catching issues Claude missed

The formation is no longer informal. It's a **delegation system** with defined roles, structured prompts, and automatic triggers.

## The Delegation System

GPT-5.4 operates through five expert roles, each invoked via Codex MCP:

| Expert | Specialty | When to Use |
|--------|-----------|-------------|
| **Architect** | System design, tradeoffs | Architecture decisions, complex debugging, after 2+ failed fixes |
| **Plan Reviewer** | Plan validation | Before starting significant work |
| **Scope Analyst** | Requirements analysis | Vague requirements, pre-planning |
| **Code Reviewer** | Code quality, bugs | After implementation + `/simplify`, before PR opens |
| **Security Analyst** | Vulnerabilities, threats | Auth changes, sensitive data, new endpoints |

Each expert can operate in two modes:
- **Advisory** (read-only): Analysis, recommendations, verdicts
- **Implementation** (write): Actually making changes to fix issues

For code review—the most common use case—advisory mode is the default. GPT reviews and returns a verdict; Claude addresses the feedback.

## My Multi-Agent Workflow

For complex features, I run the phalanx as a structured pipeline:

1. **Explore & Interview**: Claude explores the codebase, then reverse-prompts me—asking about subgoals, design decisions, constraints. This replaces the old "ask both models to propose a plan" approach.

2. **Plan & Sequence**: Claude breaks the project into sequential PRs, documented in a local `plans/` directory. Each PR has clear scope and instructions for autonomous execution.

3. **Autonomous Execution**: Claude works through each PR in DSP mode (dangerously-skip-permissions)—implementing, running `/simplify`, and opening draft PRs.

4. **Structured Review**: I delegate to GPT-5.4 via Codex MCP for code review. The delegation uses a structured 7-section prompt: task, expected outcome, context, constraints, must do, must not do, output format. GPT returns actionable feedback ranked by severity.

5. **Iterate & Merge**: Claude addresses GPT's feedback, the PR opens, CI runs. After merge, Claude updates the plan doc and continues to the next PR.

The human-in-the-loop moments are the initial interview, reviewing GPT's code review findings, and merge decisions. Everything between is autonomous.

## Model Personalities

Through experience, I've developed intuition for each model's tendencies:

| Model | Strength | Weakness | Best For |
|-------|----------|----------|----------|
| Claude Opus 4.6 (1M) | Autonomous execution, strong context retention, follows plans | Can over-commit to an approach | Implementation, multi-PR projects |
| GPT-5.4 High (Codex MCP) | Structured analysis, catches second-order effects, thorough | Slow, pedantic, over-indexes on edge cases | Code review, architecture decisions |

Your model roster may differ. The point is to develop intuition for when to use which.

## When to Break Formation

The phalanx formation is vulnerable to uneven terrain—situations where the structured plan-then-execute approach doesn't fit:

- **Exploratory debugging**: You don't know what's wrong yet
- **Rapid prototyping**: You're feeling your way to a solution
- **Unfamiliar territory**: The AI's suggestions need heavy human judgment
- **Single-file changes**: The overhead of delegation isn't worth it

In these moments, I break formation and work directly with Claude in an interactive session. No plan doc, no delegation, just back-and-forth problem solving.

**The phalanx is a tool, not a religion.** Know when to use it and when to abandon it.

## Competitive Agents as Quality Control

The core quality pattern: use GPT to review Claude's work via structured delegation.

The delegation prompt includes full context—what Claude built, which files changed, what the requirements were. GPT has no ego investment in Claude's code. It will find issues the implementing model missed.

> "Review this PR against the requirements. Check for correctness, security, performance, and maintainability. Return specific issues ranked by severity with your verdict: APPROVE, REQUEST CHANGES, or REJECT."

You synthesize GPT's feedback, decide what matters, and have Claude address the real issues. The competitive tension between models is what catches blind spots.

## Building Your Own Intuition

You'll develop your own agent phalanx through experience:

1. **Start with one model**: Get fluent with Claude before adding GPT
2. **Add review**: When you're ready, use GPT to review Claude's output
3. **Formalize triggers**: Notice which situations benefit from delegation—write them down
4. **Iterate**: Your delegation system will evolve as you learn what works

The goal isn't to copy my exact setup—it's to develop judgment about when to use which model and in what capacity.

---

## The Bigger Picture

The Agent Phalanx framework is really about **developing judgment**. You're not just using AI—you're orchestrating it. You're the conductor, not the instrument.

This connects back to all the previous frameworks:
- **Comprehensible Code**: You understand what each agent produces
- **Context Engineering**: You manage each agent's context across four layers
- **Atomic Features**: Each agent works on well-scoped PRs
- **Emergent Abstractions**: Your delegation system emerges from experience, not theory

Master the fundamentals. The advanced techniques will follow.

---

## Cheatsheets

Ready for quick-reference guides?
→ [Prompting Patterns](../cheatsheets/prompting-patterns.md)
→ [Claude Code Tips](../cheatsheets/claude-code-tips.md)
→ [Git Survival Guide](../cheatsheets/git-survival-guide.md)
