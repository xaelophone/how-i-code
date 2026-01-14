# Context Engineering

AI agents have a context window—a limited memory of your conversation. How you manage that memory determines the quality of the AI's output.

## The Problem

When you iterate on a feature plan, the context window fills with:
- Your initial (probably wrong) ideas
- Dead-end explorations
- Outdated requirements you've since refined
- The AI's verbose explanations of things you already understood

By the time you say "okay, implement it," the AI is holding onto all of that noise. It gets confused. It references old ideas. It produces inconsistent code.

## The Solution: Externalize, Then Reset

The fix is simple: **document the final plan outside the conversation, then start fresh.**

My workflow:
1. **Plan in conversation** — messy, iterative, lots of back-and-forth
2. **Externalize to GitHub Issues** — ask the AI to distill the plan into atomic issues
3. **Clear context** — start a brand new chat
4. **Implement from the issue** — the AI reads the clean, distilled plan

The GitHub Issue becomes the "source of truth." The planning conversation can be forgotten.

## Why GitHub Issues?

I used to have Claude create README files for features, migrations, even one-off tasks. My repo got littered with documentation that went stale immediately.

GitHub Issues are better because:
- **Progress tracking**: Issues have status, comments, references to PRs
- **Cleaner repos**: Documentation lives in the right place (issues/PRs), not cluttering your codebase
- **AI-friendly provenance**: When you need to revisit a feature, the Issue contains the plan, the implementation notes, and links to the actual code

By November, this became my standard practice. I implemented 14 new features while *deleting* 6,000+ lines of code. That was only possible because I started treating git as the source of truth for context engineering.

## The Two-Layer Approach

I've since refined this into two complementary layers:

| Layer | Where | Purpose |
|-------|-------|---------|
| **Strategic** | GitHub Issues | Team visibility, stakeholder access, cross-project planning, provenance trail |
| **Tactical** | Local files (PRD.md + progress.txt) | Within-session task tracking, context recovery, granular progress |

**Strategic layer (GitHub Issues):**
- High-level feature planning
- "What are we building this week?"
- Comments preserve planned → actual → learned
- Visible to team and stakeholders

**Tactical layer (PRD.md + progress.txt):**
- Granular 15-30 minute tasks
- "What's Claude working on right now?"
- Automatic context injection on session resume
- Claude reads these directly (no API needed)

The workflow becomes:
1. Plan feature → externalize to **GitHub Issue**
2. Break issue into atomic tasks → **PRD.md**
3. Claude works, logs to **progress.txt**
4. Summarize phase → post comment on **Issue**

This lets you keep the benefits of GitHub (visibility, provenance, PR linking) while adding local files for the granular execution Claude needs. I built a tool called [ralph-gh](https://github.com/xaelophone/ralph-setup) that can bridge the two automatically.

## The Provenance Loop

At the end of each implementation session, ask Claude:

> "Summarize what we implemented. Note any divergences from the original plan and anything we learned. Post this as a comment on the GitHub Issue."

This creates a record:
- **Planned**: What we said we'd build
- **Actual**: What we actually built
- **Learned**: What we discovered along the way

When you implement Issue #2 in a sequence, the AI can read the comments on Issue #1 to understand what actually happened—not just what was planned.

## Context Hygiene Rules

1. **One task, one context**: Don't implement multiple features in the same chat
2. **Reset after planning**: Always start implementation in a fresh context
3. **Clear after completion**: Even if you *could* continue, start fresh for the next task
4. **Externalize decisions**: If you made an important decision, document it before clearing context

## When to Break the Rules

Sometimes you need continuity. If you're debugging something that emerged *during* implementation, don't reset—you'll lose the debugging context. But as soon as you've resolved the issue, clear context and continue from a clean state.

The goal isn't rigid process. It's recognizing that **context is a resource you manage**, not just something that accumulates.

---

## Next

Now that you know how to manage context, learn how to structure your work for maximum reversibility:
→ [Atomic Features](./03-atomic-features.md)
