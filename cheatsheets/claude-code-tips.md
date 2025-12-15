# Claude Code Cheatsheet

Quick reference for Claude Code workflows and settings.

---

## Model Selection

| Task | Model | Why |
|------|-------|-----|
| Planning | Opus 4.5 | Best reasoning, handles ambiguity |
| Implementation | Opus 4.5 | Less context degradation |
| Review | Opus 4.5 | Catches subtle issues |

**Bottom line**: Use Opus 4.5 for everything. The quality difference justifies the cost.

---

## Essential Settings

| Setting | Value | Why |
|---------|-------|-----|
| Output mode | **Explanatory** | See Claude's reasoning—helps you learn |
| Plan mode | Use for all features | Separates thinking from doing |

---

## Editor Integration

**Run Claude Code inside Cursor** for the best of both worlds:

| Cursor Feature | How It Helps |
|----------------|--------------|
| **File tree** | Browse and open files visually while Claude works |
| **Diff viewer** | See exactly what Claude changed with syntax-highlighted diffs |
| **[Tab](https://cursor.com/docs/tab/overview)** | Quick in-line edits when you want to "break formation" |
| **[Debug Mode](https://cursor.com/blog/debug-mode)** | Focused debugging workflow that augments Claude's diagnostic abilities |
| **[Visual Editor](https://cursor.com/blog/browser-visual-editor)** | UI iteration in Cursor Browser that pairs well with Claude's implementation |

**Setup**: Open your project in Cursor, then launch Claude Code from the integrated terminal.

**Why this combo works**: Claude Code is powerful but terminal-only. Cursor provides the visual context—file structure, syntax highlighting, change tracking—that makes it easier to follow along, verify changes, and catch issues before they ship.

---

## The Core Loop

```
1. Plan (voice) → 2. GitHub Issues → 3. New context → 4. Implement → 5. Review
```

See [QUICKSTART.md](../QUICKSTART.md) for details.

---

## Context Management

**Do:**
- Clear context after completing each task
- Start implementation in a fresh chat
- Externalize plans to GitHub Issues before resetting
- Post implementation summaries as Issue comments

**Don't:**
- Implement multiple features in one context
- Let planning conversation pollute implementation
- Continue indefinitely without clearing

**Rule of thumb**: If the context has 50+ messages, you've probably gone too long.

---

## Voice Dictation

**Tool**: WisprFlow (or similar)

**Why voice for planning?**
- Typing forces pre-editing
- Voice externalizes raw, messy thoughts
- Claude structures your ideas for you

**Pattern**: Dictate your idea stream-of-consciousness, end with "ask me any clarifying questions."

---

## The Screenshot Trick

When you can't articulate what you want:

1. Take a screenshot of a reference UI
2. Give it to Claude with annotations
3. Ask: "Describe what you see in terms of UX, components, and layout"
4. Edit the description to match your actual target
5. Use the edited description as your prompt

This "reverse prompting" method works when words fail you.

---

## [Skills](https://github.com/anthropics/skills) (Reusable Workflows)

Watch for repetitive processes and ask Claude to turn them into skills:

**Good candidates:**
- Creating PRs with consistent format
- Reviewing code against a checklist
- Generating GitHub Issues from plans
- Running standard test suites

**Prompt:**
```
I keep doing [process] manually. Can you turn this into a reusable skill I can invoke?
```

---

## Provenance Tracking

At the end of each implementation:

```
Summarize what we implemented. Note:
- What was planned vs. what was built
- Any divergences and why
- What we learned

Format as a comment for the GitHub Issue.
```

This creates a trail: planned → actual → learned.

---

## Red Flags

| Signal | Problem | Fix |
|--------|---------|-----|
| Can't explain the code | You're accumulating slop | Ask for explanation before shipping |
| 50+ messages in context | Context degradation | Clear and restart |
| AI referencing old ideas | Stale context | Externalize plan, reset |
| PR touches many things | Scope creep | Break into atomic PRs |
| "This might break things" | Too much bundled | Ship smaller |

---

## Quick Commands

| Action | What to Say |
|--------|-------------|
| Enter plan mode | "Let's plan this feature..." |
| Exit plan mode | "I'm happy with this plan. Create the GitHub Issues." |
| Start implementation | "Implement Issue #X" |
| Request review | "Review this PR. Be critical." |
| Clear context | Start a new chat |
| Learn from code | "Explain this so I can write similar code myself" |

---

## The Meta-Skill

Your daily practice of working with AI becomes raw material for teaching it to work like you.

Every workflow hack you discover → a reusable skill
Every debugging session → a pattern to recognize
Every explanation you request → knowledge you retain

Document your process. It compounds.
