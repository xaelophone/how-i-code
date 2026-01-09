# Comprehensible Code

The most important rule for coding with AI: **understand what you're shipping.**

## The Rule

You should be able to explain how any AI-generated feature works at the architecture level. Not every line of syntax, but the system: what it does, how it connects to existing code, and how data flows through it.

If you can't explain the architecture, you're not ready to ship it.

## Why This Matters

"Slop" is AI-generated code that works but that you don't understand. Slop accumulates. It becomes a black box you're afraid to touch. When something breaks, you can't debug it—you can only ask the AI to "fix it," which often creates more slop.

The solution isn't reading every line—it's building a review process that catches problems before they ship.

## How I Avoid Slop

I don't read every line of code anymore. Instead, I run multiple rounds of AI review before anything merges:

1. **[`/simplify-code`](https://github.com/anthropics/claude-plugins-official/tree/main/plugins/code-simplifier)** — Cleans up the implementation for clarity and maintainability
2. **[`/code-review`](https://github.com/anthropics/claude-plugins-official/tree/main/plugins/code-review)** — Launches 4 parallel review agents that audit from different angles (guidelines compliance, bug detection, historical context)
3. **Address feedback** — I assess what Claude found and ask it to fix the relevant issues
4. **Repeat if needed** — The PR gets refined until there are no high-confidence issues

This multi-round process catches the line-level details. My job is understanding the architecture—how the feature fits into the system, how data flows, what the entry points are.

## When to Dig Deeper

Sometimes you need to understand specific code. Ask:

> "Explain how this code works. I want to be able to write something similar myself in the future."

The key is adding context about *your* objective. "Explain this code" gets you a generic walkthrough. "Explain this so I can write similar code myself" gets you a teaching moment.

This applies beyond code:
- **Logs**: "Explain what these logs are telling me about the request lifecycle."
- **Network requests**: "Walk me through what's happening in this API call."
- **Error messages**: "What is this error actually saying, and what are the common causes?"

## The Heritage Speaker Analogy

Think of it like being a "heritage speaker" of a programming language. Heritage speakers grew up hearing a language at home—they understand it fluently, can follow conversations, and can express themselves, but they might not have formal grammar training.

You don't need to parse every line of syntax. But you need to understand systems. You need to follow how data flows through your app, how components connect, and how new features integrate with existing architecture.

This is comprehension at the architecture level—not line-by-line translation, but understanding how the pieces fit together. The multi-round review process handles the details. Your job is knowing the shape of the system.

## Practical Checkpoints

Before merging any PR, ask yourself:

1. Can I explain what this *feature* does and how it fits into the system?
2. Do I understand how the *pieces connect*—what calls what, how data flows?
3. If this breaks, do I know the *entry points* to start investigating?

If the answer to any of these is "no," you're not done yet. Run another review round, ask Claude to explain the architecture, or dig into the specific piece that's unclear.

**Use visualization tools**: Automated PR review agents like Greptile can help here. They generate architecture diagrams and data flowcharts for your PRs, letting you *see* how code changes flow through the system. If the diagram doesn't make sense to you, that's a signal to dig deeper before merging.

---

## The Mindset Shift

You're not trying to become a software engineer. You're trying to become a **technically fluent PM who can ship code**. The goal isn't to parse every line—it's to understand systems well enough to build, debug, and maintain them.

The AI writes the code. The AI reviews the code. You provide the architectural judgment and decide when it's ready to ship.

---

## Next

Now that you understand *why* comprehension matters, learn *how* to manage the AI's memory effectively:
→ [Context Engineering](./02-context-engineering.md)
