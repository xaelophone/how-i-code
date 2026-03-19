# The Workflow for Coding with AI

This is the core loop I use every day. For multi-PR projects, it runs autonomously. For single features, it's a lighter version of the same principles.

## The Autonomous Pipeline

For any project that spans more than one PR, this is the workflow:

### Step 1: Explore & Interview

Start Claude in **standard mode** (not plan mode) and describe your project:

> "I want to build [project]. Explore the codebase to understand the current landscape, then interview me about subgoals, design decisions, and anything ambiguous."

Claude will:
1. Read through your codebase to understand the existing architecture
2. Reverse-prompt you — asking about implementation preferences, design constraints, scope boundaries
3. Surface assumptions before any code gets written

Voice dictation is still the best way to answer the interview questions. Planning is thinking—voice lets you externalize messy ideas without pre-editing.

### Step 2: Write the Plan

Once the interview is complete:

> "Break this project into sequential PRs. Write the plan to the `plans/` directory with instructions for autonomous execution."

Claude writes a plan doc to `plans/` (gitignored) containing:
- **PR sequence**: ordered list of PRs, each with clear scope
- **Per-PR scope**: what's included, what's explicitly excluded
- **Autonomous instructions**: implement → `/simplify` → draft PR → pause for review → address feedback → open PR → wait for CI → update plan → next PR

For team-visible planning, also ask Claude to create GitHub Issues (the [strategic layer](./frameworks/02-context-engineering.md)).

### Step 3: Autonomous Execution

Claude works through the PR sequence in DSP mode (`--dangerously-skip-permissions`):

```
For each PR in the sequence:
  1. Implement the feature
  2. Run /simplify to clean up the code
  3. Open a draft PR
  4. ← You invoke GPT-5.4 code review via Codex MCP
  5. Claude addresses the feedback
  6. Open the PR, wait for CI
  7. After merge: update plan doc with what shipped + context for next PR
  8. Continue to next PR
```

**Your intervention points:**
- Reviewing GPT's code review findings (accept, reject, or discuss)
- Merge decisions
- Course corrections if the plan needs adjustment mid-project

Everything else is autonomous.

### Step 4: Ship & Clean Up

After the final PR merges:
1. Post a summary on the GitHub Issue: planned vs. actual vs. learned
2. Delete the plan doc from `plans/` — it's ephemeral working memory, not documentation
3. Start fresh for the next project

---

## The Simple Flow (Single Features)

For isolated features that don't need the full pipeline:

1. **Plan** — Describe the feature, let Claude ask clarifying questions
2. **Issue** — Ask Claude to create a GitHub Issue with the distilled plan
3. **Implement** — New session, point Claude at the Issue
4. **Review** — Run `/simplify`, then delegate code review to GPT-5.4 via Codex MCP

Same principles (explore → plan → implement → review), just lighter weight.

---

## The Mental Model

```
┌─────────────┐     ┌─────────────┐     ┌─────────────────────────────────────┐
│   EXPLORE   │ ──▶ │    PLAN     │ ──▶ │     AUTONOMOUS LOOP (per PR)        │
│  & INTERVIEW│     │  (plans/)   │     │                                     │
│             │     │             │     │  implement → simplify → GPT review  │
│  standard   │     │  sequential │     │  → fix → open PR → CI → merge      │
│  mode       │     │  PR docs    │     │  → update plan → next PR           │
└─────────────┘     └─────────────┘     └─────────────────────────────────────┘
     voice +             local                     DSP mode
     exploration         gitignored                autonomous
```

The key insight: **planning and execution are separate phases, but execution is now autonomous.** You invest heavily in the interview and plan, then let Claude run. The quality gates (GPT review, CI checks) catch problems without requiring you to supervise every edit.

---

## Quick Tips

- **Model**: Use Opus 4.6 (1M context) for everything. The 1M window handles the full autonomous loop without context degradation.
- **DSP mode**: Enable `--dangerously-skip-permissions` for autonomous work. Alias the `claude` command to start in DSP mode by default.
- **Plans directory**: Keep `plans/` in your `.gitignore`. Plans are agent working memory, not repo documentation.
- **GPT delegation**: Invoke Codex MCP with GPT-5.4 High for code review between `/simplify` and PR open.
- **Output mode**: Keep "[Explanatory](https://code.claude.com/docs/en/output-styles)" mode on to learn from Claude's reasoning during the interview phase.
- **Provenance**: After each PR merges, ask Claude to update the plan doc with what actually shipped. After the project completes, post a summary on the GitHub Issue.

---

## What's Next?

Once you've internalized this loop, dive into the frameworks:
- [Comprehensible Code](./frameworks/01-comprehensible-code.md) — Why understanding the code matters
- [Context Engineering](./frameworks/02-context-engineering.md) — Managing context across four layers
- [Atomic Features](./frameworks/03-atomic-features.md) — Why small PRs compound

The loop is the foundation. The frameworks are what make you good at it.
