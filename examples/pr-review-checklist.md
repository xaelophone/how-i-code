# PR Review Checklist

Use this checklist when reviewing your own PRs (or asking Claude to review them).

---

## The Checklist

### Functionality
- [ ] Does this PR do what the issue asked for?
- [ ] Have I tested the happy path manually?
- [ ] Have I tested edge cases (empty states, errors, boundaries)?
- [ ] Does it work on different screen sizes (if UI)?

### Code Quality
- [ ] Can I explain every piece of code to someone else?
- [ ] Is there any code I don't understand? (If yes, don't merge—ask for explanation)
- [ ] Is anything overly clever when simple would work?
- [ ] Is there obvious duplication that should be addressed?

### Scope
- [ ] Does this PR do ONE thing?
- [ ] Is there any scope creep (unrelated changes)?
- [ ] Are there files changed that shouldn't be in this PR?

### Safety
- [ ] No hardcoded secrets, API keys, or credentials?
- [ ] No obvious security vulnerabilities (injection, XSS, etc.)?
- [ ] No console.logs or debug code left in?
- [ ] No commented-out code that should be deleted?

### Git Hygiene
- [ ] Commit messages are clear and descriptive?
- [ ] Branch is up to date with main?
- [ ] CI checks are passing?

### Documentation
- [ ] If this changes behavior, is it documented somewhere?
- [ ] If this adds a new pattern, is there an example?
- [ ] Would a new team member understand this code?

---

## Review Prompt for Claude

```
Review this PR against the following checklist. Be critical and specific.

**Functionality**
- Does this do what Issue #[X] asked for?
- What edge cases might break?
- Any obvious bugs?

**Code Quality**
- Is anything confusing or overly complex?
- Any code smells or anti-patterns?
- Suggestions for improvement?

**Safety**
- Any security concerns?
- Any hardcoded values that shouldn't be?
- Any debug code left in?

**Scope**
- Is this PR focused on one thing?
- Any unrelated changes that should be separate?

Give me specific line-by-line feedback where relevant.
```

---

## Self-Review Questions

Before requesting review, ask yourself:

1. **Would I approve this if someone else wrote it?**
   If not, fix it first.

2. **What's the riskiest part of this change?**
   Call it out explicitly in the PR description.

3. **If this breaks at 2am, could I debug it?**
   If not, you don't understand it well enough.

4. **Is there anything I'm hoping the reviewer won't notice?**
   Fix that thing before submitting.

---

## PR Description Template

```markdown
## What

[1-2 sentences: what does this PR do?]

## Why

[Link to issue or explain the context]

## How

[Brief explanation of the approach, if not obvious from the code]

## Testing

[How did you verify this works?]
- [ ] Tested locally
- [ ] Tested edge cases: [list them]
- [ ] [Other relevant testing]

## Screenshots

[If UI changes, include before/after screenshots]

## Risks

[What could go wrong? What should reviewers pay attention to?]

---

Closes #[issue number]
```

---

## Example PR Description

```markdown
## What

Adds a weekly activity chart to the user dashboard.

## Why

Part of the dashboard feature (Issue #42). Users need to see activity trends at a glance.

## How

- Used recharts (already in project) for the line chart
- Fetches data from existing `/api/user/activity` endpoint
- Added loading and empty states

## Testing

- [x] Tested locally with real API data
- [x] Tested empty state (new user with no activity)
- [x] Tested loading state (throttled network)
- [x] Tested on mobile viewport

## Screenshots

[Before: dashboard without chart]
[After: dashboard with chart]

## Risks

- Chart library is new to me—might have missed best practices
- API response shape assumed to be stable

---

Closes #42
```

---

## The 2am Test

> "If this breaks at 2am, would I know where to start looking?"

If the answer is no:
1. You don't understand the code well enough
2. Ask Claude to explain it
3. Add comments where the logic isn't obvious
4. Consider simplifying

Never merge code you can't debug.
