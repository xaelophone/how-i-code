# Comprehensible Code

The most important rule for coding with AI: **understand everything it writes.**

## The Rule

You should be able to explain how any piece of AI-generated code works to another engineer. Not line-by-line syntax, but the logic: what it does, why it's structured that way, and how it fits into the larger system.

If you can't explain it, you don't ship it.

## Why This Matters

"Slop" is AI-generated code that works but that you don't understand. Slop accumulates. It becomes a black box you're afraid to touch. When something breaks, you can't debug it—you can only ask the AI to "fix it," which often creates more slop.

I learned this the hard way during a Vercel CI/CD debugging nightmare. The only reason I figured out a wrong API URL fallback was because I actually read the workflow logs myself and investigated with Claude. If I'd been shipping code I didn't understand, I would've been stuck.

## How to Learn From AI

When you don't understand something, don't just accept it. Ask:

> "Explain how this code works. I want to be able to write something similar myself in the future."

The key is adding context about *your* objective. "Explain this code" gets you a generic walkthrough. "Explain this so I can write similar code myself" gets you a teaching moment.

This applies beyond code:
- **Logs**: "Explain what these logs are telling me about the request lifecycle."
- **Network requests**: "Walk me through what's happening in this API call."
- **Error messages**: "What is this error actually saying, and what are the common causes?"

## The Heritage Speaker Analogy

Think of it like being a "heritage speaker" of a programming language. Heritage speakers grew up hearing a language at home—they understand it fluently, can follow conversations, and can express themselves, but they might not have formal grammar training.

You don't need to *write* code from scratch. But you need to *read* it fluently. You need to understand what good code looks like so you can recognize when the AI gives you something weird.

Just like language learning, this requires immersion: comprehensible input (reading good code) and conversational practice (asking the AI to explain things).

## Practical Checkpoints

Before merging any PR, ask yourself:

1. Can I explain what this code does to a colleague?
2. Do I understand *why* it's structured this way (not just *that* it works)?
3. If this breaks at 2am, would I know where to start looking?

If the answer to any of these is "no," you're not done yet.

**Use visualization tools**: Automated PR review agents like Greptile can help here. They generate architecture diagrams and data flowcharts for your PRs, letting you *see* how code changes flow through the system. Sometimes a visual representation makes the logic click in a way that reading code line-by-line doesn't. If the diagram doesn't make sense to you, that's a signal to dig deeper before merging.

---

## The Mindset Shift

You're not trying to become a software engineer. You're trying to become a **technically fluent PM who can ship code**. The goal isn't to write elegant algorithms—it's to understand systems well enough to build, debug, and maintain them.

The AI writes the code. You provide the judgment.

---

## Next

Now that you understand *why* comprehension matters, learn *how* to manage the AI's memory effectively:
→ [Context Engineering](./02-context-engineering.md)
