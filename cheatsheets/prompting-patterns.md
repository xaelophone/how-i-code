# Prompting Patterns

Quick reference for effective AI communication.

---

## Planning Prompts

**Start a project (explore + interview):**
```
I want to build [project]. Explore the codebase to understand the current landscape,
then interview me: ask about subgoals, implementation preferences, design constraints,
and anything ambiguous. Don't start planning until the interview is complete.
```

**Break into sequential PRs:**
```
Break this project into sequential PRs. Write the plan to the plans/ directory with:
- Ordered PR sequence, each with clear scope
- What's included and explicitly excluded per PR
- Instructions for autonomous execution
```

**Break into GitHub Issues (for team visibility):**
```
Break this plan into atomic chunks. Each chunk should be:
- Single-scope (one thing, done completely)
- Independently shippable
- Sequenced with dependencies noted

Post each chunk as a GitHub Issue.
```

**Force clarification:**
```
Before we proceed, what assumptions are you making? What questions should I answer first?
```

---

## Implementation Prompts

**Start clean implementation:**
```
Implement the feature described in Issue #[number].
```

**Scope control (prevent creep):**
```
Let's keep this PR focused on just [specific feature]. We'll handle [other thing] in a separate PR.
```

**Simple over clever:**
```
Let's keep this simple for now. Just implement the straightforward version—we can refactor later if needed.
```

**Allow duplication:**
```
I know this duplicates some code from [other file]. That's intentional—I'd rather have duplication than a premature abstraction.
```

---

## Learning Prompts

**Understand the code:**
```
Explain how this code works. I want to be able to write something similar myself in the future.
```

**Understand logs/errors:**
```
Explain what these [logs/error messages] are telling me. What are the common causes and how would I debug this?
```

**Understand architecture:**
```
Walk me through how [this system/flow] works. Explain it like I'm a PM who needs to understand it well enough to debug issues.
```

---

## Review Prompts

**Self-review:**
```
Review this PR draft and provide feedback. Be critical—what could break? What's unclear? What would you do differently?
```

**Competitive review:**
```
Here's code that [other model/previous session] wrote. Review it critically. What are the issues? What would you improve?
```

**Pre-merge checklist:**
```
Before I merge this, help me verify:
1. Does this do what the Issue asked for?
2. Are there any obvious bugs or edge cases?
3. Is anything confusing that needs comments?
4. Any security or performance concerns?
```

---

## Context Management Prompts

**Summarize for handoff:**
```
Summarize what we implemented. Note any divergences from the original plan and anything we learned. Format this as a comment I can post on the GitHub Issue.
```

**Reset context cleanly:**
```
[Start new chat]
I'm implementing Issue #[number]. Here's the context: [paste issue or link].
```

**Recover lost context:**
```
I'm continuing work on [feature]. Here's what was already done: [summary]. The current state is [description]. Let's continue from here.
```

---

## Debug Prompts

**Investigate an error:**
```
I'm seeing this error: [error]. Here's the relevant code: [code]. Walk me through what's happening and how to fix it.
```

**Trace a flow:**
```
Help me trace what happens when [action]. Start from [entry point] and walk through each step.
```

**Rubber duck:**
```
I'm stuck on [problem]. Let me explain what I've tried, and help me think through what I might be missing.
```

---

## Reverse-Prompt Interview

**Trigger a codebase exploration + interview:**
```
Explore the codebase based on [project goal]. Once you understand the landscape,
interview me: ask about subgoals, implementation preferences, design constraints,
and anything ambiguous. Don't start planning until the interview is complete.
```

This inverts the normal dynamic — instead of you prompting the AI, the AI prompts you. It surfaces questions you didn't know to ask.

---

## Bilingual Bug Explanation

**Get developer + end-user framing:**
```
Explain this bug using non-technical language. Frame it from two perspectives:
(1) what's happening in the system from a developer's view, and
(2) what an end user would experience if this shipped.
```

This builds comprehension at the system level. When you can explain a bug in terms of customer impact, you actually understand the system.

---

## Autonomous PR Instructions

**Set up the autonomous execution loop:**
```
Work autonomously through this plan. For each PR in the sequence: implement the
feature, run /simplify, open a draft PR, then pause for code review. After review
feedback is addressed, open the PR and wait for CI. Once merged, update the plan
doc with what actually shipped and any context the next PR needs. Then continue
to the next PR.
```

This prompt goes into your plan doc. It gives Claude the full autonomous instruction set.

---

## Anti-Patterns to Avoid

| Don't | Do Instead |
|----------|---------------|
| "Fix this" (vague) | "This error occurs when X. I think the issue is Y. Can you verify and fix?" |
| "Make it better" | "Specifically, I want to improve [aspect] by [metric]" |
| Letting scope creep | "Let's keep this focused on X only" |
| Accepting code you don't understand | "Explain this so I can understand it" |
| Long sessions without clearing | Clear context after each completed task |

---

## The Golden Rule

End planning prompts with:
> **"Ask me any clarifying questions you might have."**

This single habit prevents more wasted work than any other.
