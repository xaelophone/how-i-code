# The 4-Step Workflow for Coding with AI

This is the core loop I use every day. It's simple, but the separation of concerns is what makes it work.

## The Loop

### Step 1: Plan with Voice

Enter Claude Code's **Plan mode** and dictate your feature idea using voice (I use [WisprFlow](https://wisprflow.ai/r?SEAN55)). End every planning prompt with:

> "Ask me any clarifying questions you might have."

This forces the AI to surface assumptions before you've wasted tokens on the wrong solution. Talk through your idea like you're explaining it to a smart colleague who doesn't have context.

**Why voice?** Planning is thinking. Typing forces you to pre-edit your thoughts. Voice lets you externalize messy ideas, and the AI will help you structure them.

### Step 2: Break into GitHub Issues

Once you're happy with the plan, ask Claude to:

> "Break this plan into atomic chunks and post each chunk as a GitHub Issue."

Each issue should be:
- **Single-scope**: One thing, done completely
- **Independently shippable**: Could be merged on its own
- **Sequenced**: Issues reference what comes before/after

This creates a paper trail and—critically—clean context for the next step.

### Step 3: Reset Context, Then Implement

**Start a new chat.** This is non-negotiable.

Your planning session filled the context window with brainstorming, dead ends, and outdated ideas. The GitHub Issue now contains the distilled plan. Point Claude at it:

> "Implement the feature described in Issue #42."

The AI gets clean context. You get focused execution.

### Step 4: Review the PR

This is where you make sure you don't ship slop. Multiple rounds of review between you and Claude ensure quality—without requiring you to read every line of code.

**The workflow:**

1. **Simplify the code.** Run [`/simplify-code`](https://github.com/anthropics/claude-plugins-official/tree/main/plugins/code-simplifier) to clean up and simplify the implementation. This skill refines the code for clarity, consistency, and maintainability before anyone sees it.

2. **Open a draft PR.** Create a draft pull request—not ready for merge yet.

3. **Run code review.** Invoke [`/code-review`](https://github.com/anthropics/claude-plugins-official/tree/main/plugins/code-review) on the draft. This launches 4 parallel review agents that independently audit your changes from different angles: compliance with project guidelines, obvious bugs, and historical context. Each issue gets a confidence score, and only high-confidence issues (80+) surface.

4. **Assess and address feedback.** Review the issues Claude found. Ask Claude to address the relevant feedback—not everything will apply, but the high-confidence issues usually do.

5. **Open the PR.** Convert from draft to open. After multiple rounds of review, this should be easy for anyone to merge.

**Why this works:** I'm not reading every line of code anymore—but I maintain an understanding of the high-level architecture. The multi-round review process (simplify → review → address → review again) catches the details. My job is understanding how features fit into the system, not parsing syntax.

**Visual verification**: I also use [Greptile](https://app.greptile.com/signup?ref=NTM3MTUtMzY3OTU=) to automatically review PRs when I open them. It generates architecture diagrams and data flowcharts for each PR—so I can *see* how code changes flow through the system. This visual layer reinforces the [Comprehensible Code](./frameworks/01-comprehensible-code.md) principle at the architecture level.

---

## The Mental Model

```
┌─────────────┐     ┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│   PLAN      │ ──▶ │   ISSUES    │ ──▶ │  IMPLEMENT  │ ──▶ │   REVIEW    │
│  (messy)    │     │  (clean)    │     │  (focused)  │     │  (critical) │
└─────────────┘     └─────────────┘     └─────────────┘     └─────────────┘
     voice              GitHub            new context          self + human
```

The key insight: **planning and execution require different contexts.** Don't make the AI implement a feature while it's still holding onto 47 messages about "what if we did it this other way instead?"

---

## Quick Tips

- **Model**: Use Opus 4.5 for everything (planning, implementation, review). It suffers significantly less context degradation than other models.
- **Output mode**: Turn on "[Explanatory](https://code.claude.com/docs/en/output-styles)" mode to learn from Claude's reasoning. It's like pair programming with someone who explains their thought process.
- **Clear context**: Even with Opus, clear your context when a task is complete. Fresh context = focused AI.
- **Provenance**: At the end of each implementation, ask Claude to summarize what was built vs. what was planned, and post it as a comment on the Issue. This creates a trail of planned work vs. actual work.

---

## What's Next?

Once you've internalized this loop, dive into the frameworks:
- [Comprehensible Code](./frameworks/01-comprehensible-code.md) — Why understanding the code matters
- [Context Engineering](./frameworks/02-context-engineering.md) — Managing the AI's memory
- [Atomic Features](./frameworks/03-atomic-features.md) — Why small PRs compound

The loop is the foundation. The frameworks are what make you good at it.
