# Claude Opus 4.6 (1M Context)

> My daily driver. The first model I trust to work autonomously.

---

## Overview

| Attribute | Assessment |
|-----------|------------|
| **Best for** | Everything—planning, autonomous implementation, long-running multi-PR projects |
| **Avoid for** | Simple/straightforward tasks where speed matters more than depth |
| **Context window** | 1M tokens—a step change that enables autonomous project execution |
| **Context retention** | Excellent—improved compression means less degradation even at extreme session lengths |
| **Personality** | Balanced, willing to push back, genuine thought partner |
| **Overall rating** | ★★★★★ |

---

## What Changed from Opus 4.5

Opus 4.6 isn't just a spec bump. The 1M context window changes the entire relationship between human and agent. With Opus 4.5, I managed context carefully—clearing after each task, resetting between phases. With 4.6, I can hand Claude an entire multi-PR project and let it work through the sequence without losing the thread.

The instruction following is also markedly better. Opus 4.5 occasionally drifted from plans during long sessions. Opus 4.6 holds the plan. This is what made autonomous execution viable.

---

## Strengths

**Autonomous Execution**
This is the headline capability. Opus 4.6 can work through a sequence of PRs—implementing, simplifying, opening PRs, waiting for CI, updating plan docs, and continuing to the next PR—without losing context or drifting from the plan. No previous model could do this reliably.

**Planning & Long Context**
The 1M window means exploration sessions can be genuinely thorough. Claude can read through large swaths of a codebase, interview you about design decisions, and hold all of that context when breaking the project into sequential PRs. The planning phase no longer feels constrained.

**Instruction Following**
When you give it a structured plan with instructions for autonomous execution, it follows that plan. It doesn't go rogue, add unnecessary features, or reinterpret your requirements. This sounds basic, but it's what makes the trust model work.

**Clean Output**
Less AI slop than previous generations. The output is production-ready more often on the first pass, which matters when the model is working autonomously and you're reviewing after the fact.

---

## The Trust Shift

I now run Claude Code in `--dangerously-skip-permissions` mode by default. I've aliased the `claude` command to start in DSP mode, and enabled it in settings for the desktop app.

This wasn't a casual decision. It's the result of watching Opus 4.6 execute multi-PR projects reliably over weeks. The 1M context window + improved instruction following means Claude can work through complex projects without per-action approval.

The human-in-the-loop moments are now:
1. **The interview phase** — Claude explores, then interviews me about design decisions
2. **GPT code review** — After `/simplify`, GPT-5.4 reviews the PR via Codex MCP delegation
3. **Merge decisions** — I review GPT's findings and decide whether to merge

Everything between those checkpoints is autonomous. This is a fundamentally different trust model than "approve every file edit."

---

## Context Hygiene (Updated)

With 1M tokens, the old "clear after 50 messages" rule doesn't apply. But context hygiene still matters:

- **Clear between projects**, not between tasks within a project
- **The plan doc is your anchor** — as long as Claude can reference the plan, it stays on track
- **Still clear after completion** — when a project ships, start fresh for the next one
- **Memory handles the long game** — MEMORY.md persists architecture decisions across sessions, so you don't need to keep sessions alive for continuity

---

## Weaknesses

**Speed on Simple Tasks**
For quick edits and one-line fixes, Opus is still slower than necessary. But I rarely reach for a different model anymore—the consistency of staying in one model outweighs the speed penalty.

**Can Over-Commit**
In long autonomous sessions, Opus 4.6 occasionally over-commits to an approach that isn't working. The GPT code review step catches this, but it's worth knowing: if the code review surfaces fundamental design issues, don't just patch—consider restarting the PR.

---

## Personality

More balanced than Opus 4.5. Less verbose—it explains when asked but doesn't volunteer lengthy reasoning unprompted. Still willing to push back on bad ideas, which makes it a genuine thought partner during the interview phase.

The personality is well-suited to autonomous work: it's focused, doesn't get chatty, and stays on task.

---

## Best Practices

1. **Enable DSP mode**: `--dangerously-skip-permissions` for autonomous work
2. **Use the interview pattern**: Let Claude explore, then have it interview you before planning
3. **Write plan docs**: Give Claude a plan in `plans/` with explicit PR sequencing and autonomous instructions
4. **Pair with GPT review**: Use Codex MCP delegation for code review between `/simplify` and PR open
5. **Trust but verify**: Review GPT's code review findings and the PR diff before merging

---

## vs Other Models

| Compared To | Verdict |
|-------------|---------|
| GPT-5.4 High | Opus is faster to implement and better for autonomous execution. GPT-5.4 is more thorough in review and catches second-order effects. Use Opus for the spear, GPT for the shield. |
| Gemini 3.0 | Opus is the far better generalist. Gemini has stronger front-end design instincts and multimodal asset generation. |

---

*Last updated: March 2026*
