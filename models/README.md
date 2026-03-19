# Model Breakdowns

Real-world notes on how each AI model performs for PM-led development.

These aren't benchmark scores or marketing claims—they're observations from actually shipping code with each model. I update these as I learn more and as new models drop.

---

## How I Evaluate Models

I care about a few things when choosing a model for coding work:

| Dimension | What I'm Looking For |
|-----------|---------------------|
| **Context retention** | Does it hold the plan over long autonomous sessions? |
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
| [Claude Opus 4.6 (1M)](./claude-opus-4-6.md) | Everything—my daily driver, autonomous long-running tasks | ★★★★★ |
| [GPT 5.4](./gpt-5-x.md) | Formalized code review via delegation, deep context gathering, end-to-end workflows | ★★★★ |
| [Gemini 3.0](./gemini-3-0.md) | Front-end design, asset generation (best in AntiGravity) | ★★★ |

---

## The Delegation System

I don't use one model exclusively. Different models combine to form what I call an [Agent Phalanx](../frameworks/05-agent-phalanx.md)—a formalized delegation system:

- **Spears (Execution)**: Claude Opus 4.6 works autonomously through multi-PR projects in DSP mode
- **Shields (Analysis)**: GPT-5.4 High performs structured code review via Codex MCP delegation, with five expert roles (Architect, Plan Reviewer, Scope Analyst, Code Reviewer, Security Analyst)

The right model depends on the task. These breakdowns help you build intuition for when to use which.

---

## Updates

I add new breakdowns when significant models drop. Star this repo to get notified.
