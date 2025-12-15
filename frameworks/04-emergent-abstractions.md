# Emergent Abstractions

Don't over-architect early. Build the obvious thing first, feel the pain of duplication or complexity, then abstract. **Let abstractions emerge from real problems, not hypothetical ones.**

## The Trap

When you're new to coding, there's a temptation to "do it right the first time." You've read about design patterns, DRY principles, and clean architecture. You want to build something elegant.

So you spend days architecting a flexible system before you've written a line of feature code. You create abstractions for problems you might have. You build for scale you don't need.

Then requirements change, and your elegant architecture doesn't fit. Or worse—you ship something over-engineered that nobody can understand or maintain.

## The Alternative: Emerge, Don't Anticipate

Build the obvious, simple thing first. When you feel pain—duplication, complexity, brittleness—*then* abstract.

My experience building an AI system:

1. **First attempt**: Used OpenRouter as a hedge across multiple providers
   *Result*: Failed due to poor ergonomics. Learned what I actually needed.

2. **Second attempt**: Implemented direct provider APIs (Anthropic, GPT, Gemini)
   *Result*: Worked, but verbose. Lots of duplicated code across providers.

3. **Third attempt**: Consolidated to Vercel's AI SDK
   *Result*: Removed 3,000+ lines of code. Clean, maintainable, flexible.

Each step taught me something the previous step couldn't. If I'd tried to architect the "right" solution from day one, I would've guessed wrong.

## When to Abstract

Abstract when you feel **real pain**, not anticipated pain:

| Real Pain | Anticipated Pain |
|-----------|-----------------|
| "I've written this same code three times" | "I might need to write this again someday" |
| "Changing this breaks five other things" | "This could get complicated later" |
| "I can't understand my own code anymore" | "Someone might not understand this" |
| "This is slow and I've measured it" | "This might be slow" |

The threshold: **wait until the duplication or complexity actively hurts.** Then the right abstraction becomes obvious because you've lived with the problem.

## How This Works with AI

AI agents love to over-architect. They've been trained on "best practices" and will eagerly suggest design patterns, factory classes, and abstraction layers.

Push back:

> "Let's keep this simple for now. Just implement the straightforward version. We can refactor later if we need to."

Or:

> "I know this duplicates some code from the other file. That's fine—I'd rather have the duplication than a premature abstraction."

The AI will comply. Your job is to hold the line on simplicity.

## The Refactoring Moment

You'll know it's time to abstract when:
- You're copy-pasting code and modifying small parts
- A bug fix requires changes in multiple places
- Adding a new variation requires touching unrelated code
- You dread working in a particular area of the codebase

When that moment comes, *then* you architect. And because you've felt the problem, you'll build the right abstraction—not a guess.

## The Meta-Lesson

This framework applies beyond code:
- Don't build elaborate processes before you've done the task manually
- Don't create complex templates before you've written a few docs freehand
- Don't systematize until you understand what you're systematizing

**Feel the pain first. Then solve it.**

---

## Next

For advanced multi-agent orchestration (using multiple AI models together):
→ [Agent Phalanx](./05-agent-phalanx.md)
