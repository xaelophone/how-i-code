# Claude Code Cheatsheet

Quick reference for Claude Code workflows and settings.

---

## Model Selection

| Task | Model | Why |
|------|-------|-----|
| Planning | Opus 4.6 (1M) | Best reasoning, 1M context handles extended exploration |
| Implementation | Opus 4.6 (1M) | Autonomous in DSP mode, less context degradation |
| Review | GPT-5.4 High via Codex MCP | Structured delegation, catches what Claude misses |

**Bottom line**: Opus 4.6 for everything except code review, which goes to GPT-5.4 via delegation.

---

## Essential Settings

| Setting | Value | Why |
|---------|-------|-----|
| DSP mode | **Enabled by default** | Autonomous execution—alias `claude` to start in `--dangerously-skip-permissions` mode |
| Output mode | **Explanatory** | See Claude's reasoning—helps you learn during interviews |
| Always Thinking | **Enabled** | Deep reasoning on every response |
| Workflow | **Standard mode + interview** | Explore codebase, Claude interviews you, then plans sequential PRs |

---

## Terminal-First Workflow

I run Claude Code standalone in the terminal. The 1M context window and autonomous execution model mean I spend less time watching changes in an editor and more time reviewing PRs after the fact.

The review happens at the PR level (GPT code review, CI checks, diff inspection) — not at the file-edit level.

---

## The Core Loop

```
1. Explore & Interview → 2. Plan (plans/) → 3. Autonomous loop per PR → 4. Ship & clean up
```

See [QUICKSTART.md](../QUICKSTART.md) for details.

---

## Memory System

Claude Code maintains persistent context across sessions:

- **MEMORY.md**: Architecture decisions, gotchas, learned patterns. Claude updates these automatically. When you start a new session, Claude already knows what it learned last time.
- **CLAUDE.md**: Project-level instructions at the repo root. Claude reads this on every session start. Use it for project conventions, commands, and rules.

These create a "third brain" — persistent context you don't manage manually.

---

## Plugin Ecosystem

Plugins auto-inject domain knowledge when you touch relevant files:

| Plugin | What It Does |
|--------|--------------|
| **Vercel** | Injects deployment, Next.js, and AI SDK documentation |
| **Supabase** | Database, auth, and storage guidance |
| **Compound Engineering** | Code review, workflow automation, parallel processing |
| **Stripe** | Payment integration patterns |
| **Playwright** | Browser automation and testing |

**Skills** like `/simplify` and code review carry domain-specific knowledge and multi-step workflows. You invoke them by name.

This is **ambient context** — Claude gets relevant documentation without you providing it.

---

## GPT Delegation via Codex MCP

After Claude implements and runs `/simplify`, delegate to GPT-5.4 for code review:

The delegation uses five expert roles:
- **Architect** — system design, tradeoff analysis
- **Code Reviewer** — code quality, bugs, security (most common)
- **Plan Reviewer** — validates plans before execution
- **Scope Analyst** — catches requirement ambiguities
- **Security Analyst** — vulnerabilities, threat modeling

Each role operates in **advisory mode** (read-only analysis) or **implementation mode** (make changes directly).

---

## Autonomous Mode

DSP mode (`--dangerously-skip-permissions`) enables multi-PR autonomous execution:

- **Plans directory**: `plans/` (gitignored) stores the PR sequence and autonomous instructions
- **The loop**: implement → `/simplify` → draft PR → GPT review → fix → open PR → CI → update plan → next PR
- **Human intervention points**: the initial interview, reviewing GPT's findings, merge decisions

**When to use**: Multi-PR projects where you've completed the interview phase and trust the plan.

**When not to use**: Exploratory debugging, unfamiliar codebases, first-time experiments.

---

## Context Management

**Do:**
- Clear context between projects (not between tasks within a project)
- Let the plan doc anchor long sessions
- Trust persistent memory (MEMORY.md) for cross-session knowledge
- Externalize decisions to GitHub Issue comments or the plan doc

**Don't:**
- Mix unrelated projects in one session
- Ignore GPT's review findings without considering them
- Keep plan docs after projects ship — delete them

**Rule of thumb**: If you're crossing project boundaries in one session, start fresh.

---

## Voice Dictation

**Tool**: WisprFlow (or similar)

**Why voice for the interview phase?**
- Typing forces pre-editing
- Voice externalizes raw, messy thoughts
- Claude structures your answers into the plan

**Pattern**: Answer Claude's interview questions stream-of-consciousness. Let it organize your thoughts.

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

After each PR merges:

```
Update the plan doc with what actually shipped. Note:
- What was planned vs. what was built
- Any divergences and why
- Context the next PR needs

After the project completes, post a summary on the GitHub Issue.
```

This creates a trail: planned → actual → learned.

---

## Red Flags

| Signal | Problem | Fix |
|--------|---------|-----|
| Can't explain the code | You're accumulating slop | Ask for bilingual explanation (developer + end-user) |
| Crossing project boundaries | Context pollution | Clear and start fresh session |
| AI referencing old ideas | Stale context | Check the plan doc is current, consider restarting |
| PR touches many things | Scope creep | Break into atomic PRs per the plan |
| Claude stopped following the plan | Plan doc unclear or context drifted | Restart session with explicit plan reference |

---

## Quick Commands

| Action | What to Say |
|--------|-------------|
| Start a project | "Explore the codebase for [goal], then interview me" |
| Break into PRs | "Break this into sequential PRs in the plans/ directory" |
| Start implementation | "Work autonomously through the plan, starting with PR 1" |
| Request GPT review | Invoke Codex MCP delegation with Code Reviewer role |
| Explain a bug | "Explain this from both a developer and end-user perspective" |
| Clear context | Start a new chat |

---

## The Meta-Skill

Your daily practice of working with AI becomes raw material for teaching it to work like you.

Every workflow hack you discover → a reusable skill
Every debugging session → a pattern to recognize
Every explanation you request → knowledge you retain

Document your process. It compounds.
