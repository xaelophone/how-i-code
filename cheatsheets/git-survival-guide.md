# Git Survival Guide

The "social protocols" of version control—what developers take for granted but nobody teaches you.

---

## The Truth About Git

> "The hardest part wasn't learning to review AI-written code... The hill was learning how to work with other engineers on the same repo, where we all rely on the engine running smoothly."

Git isn't just version control. It's a coordination protocol. The commands are easy; the etiquette is hard.

---

## Core Concepts

| Concept | What It Is | Why It Matters |
|---------|------------|----------------|
| **Branch** | A parallel version of the code | Isolates your work from others |
| **Commit** | A snapshot of changes | Creates history you can navigate |
| **PR (Pull Request)** | A proposal to merge your branch | Where review and discussion happen |
| **Main/Master** | The "source of truth" branch | What's deployed to production |
| **Merge** | Combining branches | Integrates your work into main |
| **Conflict** | Two people changed the same thing | Requires manual resolution |

---

## The Basic Workflow

```
1. Pull latest main         → git pull origin main
2. Create a branch          → git checkout -b feature/my-thing
3. Make changes             → [write code]
4. Stage changes            → git add .
5. Commit                   → git commit -m "Add my thing"
6. Push to remote           → git push -u origin feature/my-thing
7. Open PR                  → [on GitHub]
8. Get review & merge       → [on GitHub]
9. Delete branch            → git branch -d feature/my-thing
```

---

## Branch Naming Conventions

| Type | Pattern | Example |
|------|---------|---------|
| Feature | `feature/description` | `feature/user-dashboard` |
| Bug fix | `fix/description` | `fix/login-redirect` |
| Refactor | `refactor/description` | `refactor/api-client` |
| Experiment | `experiment/description` | `experiment/new-layout` |

Keep names short, lowercase, hyphenated. No spaces.

---

## Commit Message Etiquette

**Good commits:**
```
Add user dashboard layout
Fix redirect loop on login
Refactor API client to use SDK
Remove unused analytics code
```

**Bad commits:**
```
WIP
fix
updates
asdfasdf
```

**Pattern**: Start with a verb (Add, Fix, Update, Remove, Refactor). Be specific enough that someone can understand without reading the code.

---

## PR Etiquette

### Size
✅ Small, focused PRs (< 400 lines changed)
❌ Giant PRs that touch everything

### Description
Include:
1. **What** this PR does (1-2 sentences)
2. **Why** (link to issue or explain context)
3. **How to test** (if not obvious)

### Review
- Respond to all comments before merging
- Don't take feedback personally—it's about the code
- When you disagree, explain your reasoning

### Merging
- Get at least one approval (or follow your team's rules)
- Make sure CI passes
- Delete the branch after merging

---

## Common Situations

### "I need to update my branch with latest main"

```bash
git checkout main
git pull origin main
git checkout your-branch
git merge main
# resolve any conflicts
git push
```

### "I made changes to the wrong branch"

```bash
# Stash your changes
git stash

# Switch to correct branch
git checkout correct-branch

# Apply changes
git stash pop
```

### "I need to undo my last commit"

```bash
# Undo commit but keep changes
git reset --soft HEAD~1

# Undo commit and discard changes (careful!)
git reset --hard HEAD~1
```

### "I have merge conflicts"

1. Open the conflicted file
2. Look for `<<<<<<<`, `=======`, `>>>>>>>`
3. Decide which version to keep (or combine)
4. Remove the conflict markers
5. Stage and commit

### "I need to see what changed"

```bash
# See uncommitted changes
git diff

# See what's staged
git diff --staged

# See recent commits
git log --oneline -10
```

---

## Working With Others

### The Golden Rules

1. **Pull before you push**: Always get latest changes first
2. **Don't force push to shared branches**: You'll overwrite others' work
3. **Communicate about conflicts**: If you're both editing the same file, coordinate
4. **Keep main deployable**: Never merge broken code

### When You Break Something

1. Don't panic
2. Tell your team immediately
3. Either fix it fast or revert
4. Learn from it (no shame—everyone does this)

---

## CI/CD (The Pipeline)

When you open a PR, automated checks run:

| Check | What It Does | If It Fails |
|-------|--------------|-------------|
| **Build** | Compiles the code | You broke something |
| **Tests** | Runs automated tests | You broke a test or behavior |
| **Lint** | Checks code style | Format your code |
| **Type check** | Validates types | Fix type errors |

**Rule**: Don't merge if CI is red. Fix the issues first.

---

## Git + AI Workflow

Let Claude handle git operations:

```
Create a branch for this feature and commit my changes with a descriptive message.
```

```
I have merge conflicts in [file]. Help me understand what's conflicting and how to resolve it.
```

```
Open a PR for this branch with a summary of what we built.
```

But **understand what's happening**. Don't blindly accept git commands you don't understand—that's how you accidentally delete work.

---

## Quick Reference

| I want to... | Command |
|--------------|---------|
| See current status | `git status` |
| See branches | `git branch` |
| Switch branch | `git checkout branch-name` |
| Create & switch | `git checkout -b new-branch` |
| Stage all changes | `git add .` |
| Commit | `git commit -m "message"` |
| Push | `git push` |
| Pull latest | `git pull` |
| See history | `git log --oneline` |
| See diff | `git diff` |

---

## The Mindset

Git feels like a technical tool, but it's really a **communication system**:

- Commits tell the story of what changed
- Branches isolate experiments from stable code
- PRs create space for discussion and review
- History lets you understand why decisions were made

Treat git as a conversation with your future self and your teammates, not just a save button.
