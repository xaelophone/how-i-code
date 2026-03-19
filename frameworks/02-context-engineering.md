# Context Engineering

AI agents have a context window—a limited memory of your conversation. How you manage that memory determines the quality of the AI's output.

## The Problem

When you iterate on a feature plan, the context window fills with:
- Your initial (probably wrong) ideas
- Dead-end explorations
- Outdated requirements you've since refined
- The AI's verbose explanations of things you already understood

By the time you say "okay, implement it," the AI is holding onto all of that noise. It gets confused. It references old ideas. It produces inconsistent code.

## The Solution: Layered Context

The fix isn't just "reset and restart" anymore. It's managing context across four layers, each serving a different purpose.

## The Four-Layer Approach

| Layer | Where | Purpose | Lifecycle |
|-------|-------|---------|-----------|
| **Strategic** | GitHub Issues | Team visibility, stakeholder access, provenance trail | Permanent |
| **Tactical** | `plans/` directory (gitignored) | Multi-PR project plans, autonomous agent working memory | Ephemeral—deleted when project ships |
| **Persistent** | Claude Code MEMORY.md | Architecture decisions, gotchas, learned patterns | Automatic—persists across sessions |
| **Ambient** | Plugins, skills, CLAUDE.md | Domain knowledge auto-injected when touching specific files | Always-on—no manual management |

### Strategic Layer (GitHub Issues)

This is where team-visible planning lives:
- High-level feature planning
- "What are we building this week?"
- Comments preserve planned → actual → learned
- Visible to team and stakeholders

### Tactical Layer (`plans/` directory)

This is where autonomous agent working memory lives:
- Multi-PR project plans broken into sequential PRs
- Instructions for autonomous execution (implement → simplify → review → merge → next)
- Claude reads and updates these docs as it works through the sequence
- **Gitignored and ephemeral** — deleted when the project ships
- Exists purely as agent context, not documentation

For single-feature work, GitHub Issues alone are sufficient. The `plans/` directory is for multi-PR projects where the agent needs structured working memory.

### Persistent Layer (Claude Code Memory)

Claude Code maintains MEMORY.md files that persist across sessions:
- Architecture decisions ("Auth uses `jose`, not `jsonwebtoken`")
- Gotchas and workarounds ("Supabase client doesn't expose AbortSignal")
- Learned patterns ("Dev port is 5176, not the default")

You don't manage these manually. Claude updates them as it learns. When you start a new session, Claude already knows what it learned last time.

### Ambient Layer (Plugins, Skills, CLAUDE.md)

This is context you never think about:
- **CLAUDE.md** files at project root give Claude permanent project-level instructions
- **Plugins** (Vercel, Supabase, Compound Engineering) auto-inject relevant documentation when you touch certain files or run certain commands
- **Skills** (`/simplify`, code review, etc.) carry domain-specific knowledge

The ambient layer means Claude has access to framework docs, platform conventions, and project rules without you providing them. It's context engineering that happens in the background.

## The Provenance Loop

At the end of each implementation session—or when a PR merges—ask Claude:

> "Summarize what we implemented. Note any divergences from the original plan and anything we learned. Post this as a comment on the GitHub Issue."

This creates a record:
- **Planned**: What we said we'd build
- **Actual**: What we actually built
- **Learned**: What we discovered along the way

When you implement the next PR in a sequence, the AI can read the comments on previous Issues to understand what actually happened—not just what was planned.

## Context Hygiene Rules

1. **One project, one context**: Don't mix unrelated projects in the same session
2. **Clear between projects**: When a project ships, start fresh for the next one
3. **Let the plan doc be the anchor**: As long as Claude can reference the plan, it stays on track during long autonomous sessions
4. **Trust persistent memory**: Architecture decisions carry over via MEMORY.md—you don't need to re-explain them
5. **Externalize decisions**: If you made an important decision, it should land in a GitHub Issue comment, the plan doc, or MEMORY.md—not just in conversation

## When to Break the Rules

Sometimes you need continuity. If you're debugging something that emerged *during* implementation, don't reset—you'll lose the debugging context. But as soon as you've resolved the issue, clear context and continue from a clean state.

With the 1M context window on Opus 4.6, sessions can run much longer than before. The threshold for "time to clear" is now project boundaries, not message count.

The goal isn't rigid process. It's recognizing that **context is a resource you manage across multiple layers**, not just something that accumulates in a single conversation.

---

## Next

Now that you know how to manage context, learn how to structure your work for maximum reversibility:
→ [Atomic Features](./03-atomic-features.md)
