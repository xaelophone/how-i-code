# Atomic Features

Large, multi-feature PRs are hard to review, debug, and rollback. The solution is counterintuitive: **ship more often, not less.**

## The Problem with Big PRs

When you bundle multiple changes into one PR:
- **Reviews take forever**: Reviewers get overwhelmed and skim
- **Bugs hide**: It's hard to isolate which change broke something
- **Rollbacks are painful**: You can't undo one feature without undoing everything
- **Merge conflicts multiply**: The longer a branch lives, the more it diverges

I've seen PRs sit in review for weeks because they tried to do too much. Meanwhile, the main branch moved on, and the PR became a merge conflict nightmare.

## The Atomic Approach

Ship multiple single-scope PRs throughout the day. Each PR should be:

- **One thing**: A single feature, fix, or refactor—not three
- **Complete**: The feature works end-to-end, even if it's small
- **Reviewable**: Someone can understand the change in 5-10 minutes
- **Revertible**: If something breaks, you can roll back just this change

The mental model: **branches are cheap and disposable.** Don't be precious with them.

## What "Atomic" Looks Like

**Not atomic**: "Add user dashboard with charts, notifications, and settings page"

**Atomic**:
1. "Add dashboard layout skeleton"
2. "Add chart component to dashboard"
3. "Add notifications panel to dashboard"
4. "Add settings page linked from dashboard"

Each of these can be reviewed, merged, and potentially reverted independently.

## The Tradeoff

Yes, you end up shipping multiple branches throughout the day. Yes, that's more PRs to create and merge. But:

- Each PR is trivial to review (often self-mergeable after AI review)
- Problems are isolated to specific changes
- You maintain momentum—shipping is a habit, not an event
- Your git history becomes a readable changelog

Automated PR review tools like Greptile make this even smoother—small, focused PRs get reviewed in seconds, not hours. The architecture diagrams they generate are especially useful for atomic PRs because you can instantly see the *one thing* that changed.

Being precious with branches feels like misplaced caution. The risk isn't "too many branches"—it's "too much change bundled together."

## How This Works with AI

When you ask Claude to implement a feature, scope it to one atomic unit:

> "Implement the chart component for the dashboard. Don't touch notifications or settings—those are separate issues."

If the AI starts expanding scope, stop it:

> "Let's keep this PR focused on just the chart. We'll handle notifications in the next PR."

The [Context Engineering](./02-context-engineering.md) framework helps here: each GitHub Issue should represent one atomic unit of work.

## Signs You're Not Being Atomic

Your PR has 20+ files changed
The PR description needs multiple bullet points to explain
You're nervous about merging because "a lot could break"
Review is taking days because reviewers can't find time
You're debugging and can't figure out which change caused the issue

## The Compound Effect

Atomic features compound over time:
- **Speed**: Smaller PRs merge faster, so you ship faster
- **Confidence**: Each change is low-risk, so you're less anxious
- **Learning**: Frequent shipping creates tight feedback loops
- **Trust**: Stakeholders see consistent progress, not long silences followed by big bangs

This connects to [Speed Compounds Trust](./05-agent-phalanx.md)—velocity builds stakeholder confidence faster than perfect execution on delayed timelines.

---

## Next

Now that you know how to structure your work atomically, learn when *not* to abstract early:
→ [Emergent Abstractions](./04-emergent-abstractions.md)
