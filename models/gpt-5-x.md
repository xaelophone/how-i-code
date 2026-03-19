# GPT 5.4

> Pedantic, thorough, and direct. My formalized code reviewer and architecture analyst.

---

## Overview

| Attribute | Assessment |
|-----------|------------|
| **Best for** | Structured code review, deep context gathering, architecture analysis |
| **Avoid for** | Quick implementation tasks (too slow, too thorough) |
| **Context retention** | Excellent—spends significant time on search and reasoning |
| **Personality** | Terse, direct, pedantic, tells you exactly what to do |
| **Overall rating** | ★★★★ |

---

## Which Version?

GPT 5.4 comes in multiple versions. The setup depends on your use case:

**For code review via delegation (my primary use):**
Use the **Codex variant (`gpt-5.4-codex`)** through the **Codex MCP server**. The Codex variant's structured, less creative output is actually an advantage for delegation—it follows the prompt format precisely and returns clean, actionable verdicts.

**For direct coding or end-to-end workflows:**
Use standard **GPT-5.4 High** in **Codex CLI** or the VS Code extension. The standard variant is more creative, which matters for implementation.

**Reasoning levels:**
- **High** is the minimum to get value. Below this, Opus 4.6 is faster with comparable results.
- **Medium** doesn't make sense—Opus 4.6 is better at that reasoning level.
- **Extra High** is worth it for particularly difficult architecture reviews.

### Revised Assessment (from January 2026, still holds)

My early impression of GPT 5.2 was skeptical—"confrontational, not loving it." After extended use through 5.4, the conclusion holds: **its trepidation is its power.**

What feels like friction is actually thoroughness. GPT-5.4 High explores the codebase more deeply than other models, surfaces second-order effects you'd miss, and keeps going until it's actually done.

---

## Strengths

**Deep Context Gathering**
GPT-5.4 High will take a prompt and search through as many files as possible to deeply understand the full implications of a change. It spends *way* more time in the search/grep/context collection phase than Opus does.

This makes it excellent for:
- Understanding how a new feature affects the entire file tree
- Finding all the places a bug might manifest
- Gathering context before making architectural decisions

**The Formalized Code Reviewer**
Where Claude is happy to start implementing, GPT-5.4 wants to understand everything first. I've formalized this into a delegation role: after Claude implements a feature and runs `/simplify`, I invoke GPT-5.4 via Codex MCP to review the PR.

The delegation uses a structured 7-section prompt format: task, expected outcome, context, constraints, must do, must not do, output format. GPT-5.4 returns a clean verdict with specific issues ranked by severity.

**Direct Feedback**
Its personality is terse and direct. It tells you exactly what's wrong and exactly what the fix should be. No hedging, no excessive explanation—just the answer.

---

## Formalized Code Review Role

This is the primary way I use GPT-5.4 now. It's wired into my autonomous PR workflow:

1. Claude implements a feature autonomously
2. Claude runs `/simplify` to clean up the code
3. I delegate to GPT-5.4 via Codex MCP in advisory mode (read-only)
4. GPT-5.4 reviews the PR against: correctness, security, performance, maintainability
5. Claude addresses the feedback
6. PR opens for CI

The delegation pattern uses five expert roles, but **Code Reviewer** is the most common:
- **Architect** — system design decisions, tradeoff analysis
- **Plan Reviewer** — validates plans before execution
- **Scope Analyst** — catches ambiguities in requirements
- **Code Reviewer** — code quality, bugs, security issues
- **Security Analyst** — vulnerabilities, threat modeling

Each expert can operate in advisory mode (analysis and recommendations) or implementation mode (make changes directly). For code review, advisory mode is the default.

---

## End-to-End Workflows

GPT-5.4 High is still viable for full implementation, not just review. The complete loop:
1. **Codebase research** — deep exploration of how things connect
2. **Plan writing** — understanding implications before committing
3. **Agentic coding** — implementation with awareness of ripple effects
4. **Code validation** — catching issues it introduced

**When to use end-to-end:**
- You can wait for the result (not time-sensitive)
- The change touches multiple files with interdependencies
- You want second-order effects surfaced proactively

**When to stick with Claude for implementation:**
- Speed matters more than thoroughness
- The change is isolated and well-defined
- You're running the autonomous PR pipeline (Claude implements, GPT reviews)

---

## Weaknesses

**Too Thorough for Quick Tasks**
If you need something done fast, GPT-5.4 is frustrating. It wants to understand everything before acting, which is overkill for simple tasks.

**Pedantic to a Fault**
Sometimes it gets hung up on edge cases that don't matter, or insists on patterns that are overkill for your situation. You need to know when to override its recommendations.

---

## Personality

Pedantic. Terse. Direct.

GPT-5.4 doesn't waste words. It analyzes thoroughly, then gives you a clear verdict. This is refreshing compared to more verbose models, but it can also feel cold.

It's the senior engineer who reviews your code and just writes "this is wrong, do X instead." Helpful, but not warm.

---

## Best Practices

1. **Use Codex variant for MCP delegation**: `gpt-5.4-codex` through Codex MCP for structured code review
2. **Use standard variant for direct work**: GPT-5.4 High in Codex CLI for end-to-end implementation
3. **High reasoning minimum**: Below High, Opus 4.6 is the better choice
4. **Formalized review role**: Invoke via delegation after `/simplify`, before PR opens
5. **Don't use for quick tasks**: The thoroughness isn't worth it for isolated, time-sensitive changes
6. **Advisory mode for review**: Read-only delegation for code review; implementation mode only when you want GPT to make changes directly

---

## vs Other Models

| Compared To | Verdict |
|-------------|---------|
| Claude Opus 4.6 (1M) | GPT-5.4 High is more thorough in review; Opus is faster and better for autonomous implementation. Both can implement—choose based on whether you need speed (Opus) or thoroughness (GPT). For review, GPT catches more. |
| Gemini 3.0 | Both have cleaner design aesthetics than Claude. GPT is better for logic; Gemini for visual front-end. |

---

## Design Aesthetic

Worth noting: the GPT 5 series has a more refined design palette than Claude. The UI code it generates tends to be more brutal, more subtle—less "AI smell." If you care about design quality, GPT often produces cleaner visual output.

---

*Last updated: March 2026*
