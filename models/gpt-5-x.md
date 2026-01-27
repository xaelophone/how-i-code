# GPT 5.X

> Pedantic, thorough, and direct. My "strict reviewer" for when Claude moves too fast.

---

## Overview

| Attribute | Assessment |
|-----------|------------|
| **Best for** | Deep context gathering, understanding feature implications, code review |
| **Avoid for** | Quick implementation tasks (too slow, too thorough) |
| **Context retention** | Excellent—spends significant time on search and reasoning |
| **Personality** | Terse, direct, pedantic, tells you exactly what to do |
| **Overall rating** | ⭐⭐⭐⭐ |

---

## Which Version?

GPT 5.X comes in multiple versions. The only one worth your time for coding work is **GPT-5.2 High** in **Codex CLI** (or the VS Code extension).

**Reasoning levels:**
- **High** is the minimum setting to get the most out of this model. Below this, the thoroughness that makes it valuable disappears.
- **Medium** doesn't make sense—Opus 4.5 is about the same speed with similar results. No reason to use GPT-5.2 at that level.
- **Extra High** is worth it for particularly difficult tasks, but shouldn't be your default.

**Model variant:**
Use standard GPT-5.2, not the Codex variant (`gpt-5.2-codex`). The Codex variant is less creative with no perceptible performance benefit.

**Harness matters:**
Always use Codex CLI or the VS Code extension. Cursor, AntiGravity, Cline, and other harnesses don't surface GPT-5.2's strengths the same way.

### Revised Assessment

My early impression of GPT 5.2 was skeptical—"confrontational, not loving it." After extended use, I've reversed course: **its trepidation is its power.**

What felt like friction is actually thoroughness. GPT-5.2 High explores the codebase more deeply than previous iterations, surfaces second-order effects you'd miss, and keeps going until it's actually done. The slowness is the tradeoff, but for certain workflows, it's worth it.

---

## Strengths

**Deep Context Gathering**
GPT 5.1 Codex High will take a prompt and search through as many files as possible to deeply understand where and how the full implications of a feature or bug might ripple through your codebase. It spends *way* more time in the search/grep/context collection phase than Opus does.

This makes it excellent for:
- Understanding how a new feature affects the entire file tree
- Finding all the places a bug might manifest
- Gathering context before making architectural decisions

**The Strict Reviewer**
Where Claude is happy to start coding pretty quickly after receiving a prompt, GPT 5.1 wants to understand everything first. This makes it an excellent "second opinion" model.

My workflow: Let Claude implement a feature, then have GPT 5.1 review the PR. It will catch things Claude missed because it actually looks at more of the codebase.

**Direct Feedback**
Its personality is terse and direct. It tells you exactly what the solution should be, or exactly what's wrong with a PR. No hedging, no excessive explanation—just the answer.

---

## End-to-End Workflows

This is the big update: **GPT-5.2 High is now viable for implementation**, not just review.

The strongest argument for end-to-end adoption is the complete loop:
1. **Codebase research** — deep exploration of how things connect
2. **Plan writing** — understanding implications before committing to an approach
3. **Agentic coding** — implementation with awareness of ripple effects
4. **Code validation** — catching issues it introduced

What makes this work is that GPT-5.2 High keeps going until done. It doesn't stop early, doesn't assume it's finished when it isn't. The thorough, slow approach that makes it frustrating for quick tasks becomes an advantage when you need sustained focus across multi-file changes.

**When to use end-to-end:**
- You can wait for the result (not time-sensitive)
- The change touches multiple files with interdependencies
- You want second-order effects surfaced proactively
- The task benefits from deep codebase understanding before action

**When to stick with Claude for implementation:**
- Speed matters more than thoroughness
- The change is isolated and well-defined
- You're iterating quickly and need fast feedback loops

---

## Weaknesses

**Too Thorough for Quick Tasks**
If you need something done fast, GPT 5.1 is frustrating. It wants to understand everything before acting, which is overkill for simple tasks.

**Pedantic to a Fault**
Sometimes it gets hung up on edge cases that don't matter, or insists on patterns that are overkill for your situation. You need to know when to override its recommendations.

---

## Personality

Pedantic. Terse. Direct.

GPT 5.1 doesn't waste words. It analyzes thoroughly, then gives you a clear verdict. This is refreshing compared to more verbose models, but it can also feel a bit cold.

It's the senior engineer who reviews your code and just writes "this is wrong, do X instead." Helpful, but not warm.

---

## Best Practices

1. **Use GPT-5.2 High in Codex CLI**: Other versions/harnesses aren't worth it for coding
2. **Plan design and critique**: Excellent for writing plans and reviewing plans others wrote
3. **End-to-end when you can wait**: If speed isn't critical, GPT-5.2 High can handle full implementation
4. **Review for Claude's work**: Let Claude implement fast, then have GPT-5.2 review the PR
5. **Don't use it for quick tasks**: The slowness isn't worth it for isolated, time-sensitive changes
6. **Acknowledge the tradeoff**: You're trading speed for thoroughness—know when that's the right trade

---

## vs Other Models

| Compared To | Verdict |
|-------------|---------|
| Claude Opus 4.5 | GPT-5.2 High is more thorough; Opus is faster to ship. Both can implement—choose based on whether you need speed (Opus) or thoroughness (GPT). For review, GPT catches more. |
| Gemini 3.0 | GPT and Gemini both have cleaner design instincts than Claude. GPT is better for logic; Gemini for visual front-end. |

---

## Design Aesthetic

One thing worth noting: the GPT 5 series has a more refined design palette than Claude. The UI code it generates tends to be more brutal, more subtle—less "AI smell." If you care about design quality, GPT often produces cleaner visual output.

---

*Last updated: January 2026*
