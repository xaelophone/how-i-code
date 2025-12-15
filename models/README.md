# Model Breakdowns

Real-world notes on how each AI model performs for PM-led development.

These aren't benchmark scores or marketing claims—they're observations from actually shipping code with each model. I update these as I learn more and as new models drop.

---

## How I Evaluate Models

I care about a few things when choosing a model for coding work:

| Dimension | What I'm Looking For |
|-----------|---------------------|
| **Context retention** | Does it remember what we discussed 50 messages ago? |
| **Instruction following** | Does it do what I ask, or go rogue? |
| **Code quality** | Is the output clean, or do I get slop? |
| **Reasoning** | Can it think through complex problems, or does it pattern-match? |
| **Speed** | Fast enough to maintain flow? |
| **Personality** | Eager to ship? Overly cautious? Pedantic? |

Different models excel at different things. The goal isn't to find the "best" model—it's to know when to use which.

---

## Current Models

| Model | Best For | My Rating |
|-------|----------|-----------|
| [Claude Opus 4.5](./claude-opus-4-5.md) | Everything—planning, implementation, review (my daily driver) | ⭐⭐⭐⭐⭐ |
| [GPT 5.X](./gpt-5-x.md) | Deep context gathering, code review, strict second opinions | ⭐⭐⭐⭐ |
| [Gemini 3.0](./gemini-3-0.md) | Front-end design, asset generation (best in AntiGravity) | ⭐⭐⭐ |

---

## The Phalanx Approach

I don't use one model exclusively. Different models combine to form what I call an [Agent Phalanx](../frameworks/05-agent-phalanx.md):

- **Shields (Analysis)**: Models that are thorough and catch edge cases
- **Spears (Execution)**: Models that ship fast and handle implementation

The right model depends on the task. These breakdowns help you build intuition for when to use which.

---

## Updates

I add new breakdowns when significant models drop. Star this repo to get notified.

Want to discuss model selection for your specific use case? → [Work with me](../WORK-WITH-ME.md)
