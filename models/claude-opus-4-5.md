# Claude Opus 4.5

> My favorite model of all time. The best all-around model for AI-assisted development.

---

## Overview

| Attribute | Assessment |
|-----------|------------|
| **Best for** | Planning, long context tasks, instruction following, vision |
| **Avoid for** | Simple/straightforward tasks (can be slow) |
| **Context retention** | Excellent—improved context compression means less degradation |
| **Personality** | Eager but balanced, willing to push back, helpful thought partner |
| **Overall rating** | ⭐⭐⭐⭐⭐ |

---

## Strengths

**Planning & Long Context**
Opus 4.5 excels at planning complex features and maintaining coherence over long sessions. The improved context compression algorithm means you don't see the same performance degradation that plagued earlier models. You can actually have extended conversations without the AI losing track of earlier decisions.

**Instruction Following**
When you tell it to do something, it does that thing. It doesn't go rogue, add unnecessary features, or interpret your request too creatively. This sounds basic, but it's a meaningful improvement over previous generations.

**Vision**
Particularly strong at understanding screenshots. Give it a UI screenshot and it genuinely *sees* and understands the context—layout, components, relationships. This makes the "screenshot trick" (described in the cheatsheets) actually work.

**Clean Output**
Unlike earlier models, Opus 4.5 doesn't litter your repo with unnecessary markdown files, excessive comments, or other artifacts that smell like AI slop. The output is cleaner and more production-ready.

---

## Weaknesses

**Speed on Simple Tasks**
For straightforward tasks, Opus can feel slow. If you just need a quick function or a minor tweak, you might be better off with a faster model or Cursor's Tab completions.

Honestly, there's not much I'd avoid using it for. It's genuinely good at almost everything.

---

## Personality

Opus 4.5 is eager but *balanced*—less trigger-happy than the Sonnet family (3.5 Sonnet, 4 Sonnet, even 4.5 Sonnet). It's willing to push back on my ideas when something doesn't make sense, which makes it a genuine thought partner rather than a yes-machine.

The downside: it can be verbose. It likes to explain its reasoning, which is helpful for learning but sometimes you just want the code.

---

## Best Practices

1. **Use it for everything complex**: Planning, implementation, review—Opus handles the full loop
2. **Leverage its vision**: Give it annotated screenshots when describing UI work
3. **Trust its pushback**: When it questions your approach, actually consider the feedback
4. **Clear context anyway**: Even though context retention is excellent, still clear context between major tasks for best results

---

## vs Other Models

| Compared To | Verdict |
|-------------|---------|
| GPT 5.1 Codex High | Opus is faster to start coding; GPT 5.1 is more thorough in context gathering. Use Opus for implementation, GPT for review. |
| Gemini 3.0 | Opus is the better generalist; Gemini has stronger front-end design instincts. |
| Claude Sonnet | Opus is more balanced and less eager. Sonnet ships faster but with less consideration. |

---

*Last updated: December 2025*
