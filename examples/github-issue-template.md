# GitHub Issue Template

Use this template when Claude creates issues for your feature plan.

---

## Template

```markdown
## Summary

[1-2 sentences describing what this issue accomplishes]

## Context

[Why this matters / what it enables / how it fits into the larger feature]

## Requirements

- [ ] [Specific requirement 1]
- [ ] [Specific requirement 2]
- [ ] [Specific requirement 3]

## Technical Notes

[Any relevant implementation details, constraints, or considerations]

## Dependencies

- Blocked by: #[issue number] (if applicable)
- Blocks: #[issue number] (if applicable)

## Definition of Done

- [ ] Feature works as described
- [ ] Code is comprehensible (I can explain it)
- [ ] PR has been reviewed
- [ ] No obvious bugs or regressions

---

Sequence: [X of Y] in [Feature Name]
```

---

## Example: Real Issue

```markdown
## Summary

Add a chart component to the user dashboard that displays weekly activity.

## Context

This is part of the user dashboard feature. Users need to see their activity trends at a glance. This issue handles just the chart—the dashboard layout was completed in #41.

## Requirements

- [ ] Display a line chart showing daily activity for the past 7 days
- [ ] X-axis: days of the week
- [ ] Y-axis: activity count
- [ ] Fetch data from existing `/api/user/activity` endpoint
- [ ] Handle loading and empty states gracefully

## Technical Notes

- Use the existing chart library (recharts) already in the project
- Follow the component patterns in `src/components/charts/`
- The API endpoint already exists; no backend work needed

## Dependencies

- Blocked by: #41 (dashboard layout)
- Blocks: #43 (notifications panel needs chart to be in place)

## Definition of Done

- [ ] Chart renders correctly with real data
- [ ] Loading spinner while fetching
- [ ] Empty state when no data
- [ ] Responsive on mobile
- [ ] Code reviewed and merged

---

Sequence: 2 of 4 in User Dashboard
```

---

## Tips for Good Issues

### Be Specific
Bad: "Add charts to dashboard"
Good: "Add weekly activity line chart to dashboard"

### Include Context
Don't assume the reader (or AI) knows the bigger picture. Explain where this fits.

### Define Done
Ambiguous completion = scope creep. Be explicit about what "done" means.

### Note Dependencies
If this issue depends on another, say so. If other issues depend on this one, say that too.

### Sequence Your Work
Number your issues (1 of 4, 2 of 4, etc.) so the implementation order is clear.

---

## Prompt to Generate Issues

```
Break this plan into atomic GitHub Issues. For each issue:
1. Write a clear summary (1-2 sentences)
2. Explain the context and why it matters
3. List specific requirements as checkboxes
4. Note any technical considerations
5. Identify dependencies (what blocks this, what this blocks)
6. Define what "done" means
7. Number the sequence (e.g., "2 of 5 in [Feature Name]")

Make each issue independently shippable—someone should be able to implement just this issue and merge it.
```
