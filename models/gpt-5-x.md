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

GPT 5.X comes in multiple versions. **Codex High** is the only one worth your time for coding work. The reasoning capabilities at the "high" setting are what make it useful—lower settings don't bring the same depth.

I haven't fully tested **GPT 5.2** for coding yet. Early impressions: its personality as a general-purpose agent is more confrontational, and I'm not loving it. Will update when I've used it more.

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

1. **Use Codex High**: Other versions aren't worth it for coding
2. **Use it for review, not implementation**: Let Claude code, let GPT review
3. **Leverage its thoroughness**: When you need to understand implications across a codebase, this is your model
4. **Don't use it for quick tasks**: It's too slow and thorough for simple stuff

---

## vs Other Models

| Compared To | Verdict |
|-------------|---------|
| Claude Opus 4.5 | GPT is more thorough; Opus is faster to ship. Use both: Opus implements, GPT reviews. |
| Gemini 3.0 | GPT and Gemini both have cleaner design instincts than Claude. GPT is better for logic; Gemini for visual front-end. |

---

## Design Aesthetic

One thing worth noting: the GPT 5 series has a more refined design palette than Claude. The UI code it generates tends to be more brutal, more subtle—less "AI smell." If you care about design quality, GPT often produces cleaner visual output.

---

*Last updated: December 2025*
