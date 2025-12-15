# Agent Phalanx

> **Advanced Framework**: This builds on all previous frameworks. If you're just starting out, master the basics first and return here when you're ready to level up.

Each AI model has its own specialty. Combined strategically, they form a phalanx—a formation where different units cover each other's weaknesses.

## The Formation

In a Greek phalanx, shields protect while spears attack. In my AI workflow:

- **Shields (Analysis & Planning)**: Models like GPT-5 that are pedantic about context, thorough in analysis, and careful in planning
- **Spears (Execution)**: Models like Claude Code that are context-rich, eager to ship, and fast in implementation

The rigidity of this formation is both its strength and weakness. When the terrain is clear, the formation is unstoppable. When it's uneven, you need to break formation and adapt.

## My Multi-Agent Workflow

For complex features, I'll run multiple agents in parallel:

1. **Planning phase**: Ask both Claude and GPT to propose a plan for the same feature
   - GPT tends to be more conservative, surfacing edge cases
   - Claude tends to be more pragmatic, focusing on shipping
   - I synthesize the best of both

2. **Execution phase**: Claude Code implements while I spot-check with other models
   - If something feels off, I'll ask GPT to review Claude's approach
   - Competitive tension catches blind spots

3. **Review phase**: Multiple models critique the work
   - Different models catch different issues
   - I make the final call as the human in the loop

I've described this as a "groupchat"—bouncing between models until I'm satisfied with the direction.

## Model Personalities

Through experience, I've developed intuition for each model's tendencies:

| Model | Strength | Weakness | Best For |
|-------|----------|----------|----------|
| Claude (Opus) | Pragmatic execution, strong context retention | Can be too eager to ship | Implementation, refactoring |
| GPT-5.X | Thorough analysis, edge case awareness | Pedantic, slow to commit | Planning, architecture review |
| Cursor Tab | Fast inline completions | Limited context | Quick edits, in-the-moment coding |

Your model roster may differ. The point is to develop intuition for when to use which.

## When to Break Formation

The phalanx formation is vulnerable to uneven terrain—situations where the structured plan-then-execute approach doesn't fit:

- **Exploratory debugging**: You don't know what's wrong yet
- **Rapid prototyping**: You're feeling your way to a solution
- **Unfamiliar territory**: The AI's suggestions need heavy human judgment

In these moments, I break formation and lead the charge myself. I'll use Cursor's Tab model for quick inline changes, manually write code when I know exactly what I want, or simply think through the problem without AI assistance.

**The phalanx is a tool, not a religion.** Know when to use it and when to abandon it.

## Building Your Own Intuition

You'll develop your own agent phalanx through experience:

1. **Experiment with multiple models**: Try the same task with different AIs
2. **Notice the differences**: Which model gave better output? Why?
3. **Document your findings**: Build a mental (or literal) model of each AI's personality
4. **Iterate**: Your intuition will refine over time

The goal isn't to find the "best" model—it's to understand the strengths of each and deploy them strategically.

## Competitive Agents as Quality Control

One powerful pattern: use agents competitively to catch errors.

> "Here's the code Claude wrote. Review it critically. What could go wrong? What would you do differently?"

The second model has no ego investment in the first model's code. It will find issues the original model missed. You synthesize both perspectives to arrive at better solutions.

---

## The Bigger Picture

The Agent Phalanx framework is really about **developing judgment**. You're not just using AI—you're orchestrating it. You're the conductor, not the instrument.

This connects back to all the previous frameworks:
- **Comprehensible Code**: You understand what each agent produces
- **Context Engineering**: You manage each agent's context window
- **Atomic Features**: Each agent works on well-scoped tasks
- **Emergent Abstractions**: Your multi-agent workflow emerges from experience, not theory

Master the fundamentals. The advanced techniques will follow.

---

## Cheatsheets

Ready for quick-reference guides?
→ [Prompting Patterns](../cheatsheets/prompting-patterns.md)
→ [Claude Code Tips](../cheatsheets/claude-code-tips.md)
→ [Git Survival Guide](../cheatsheets/git-survival-guide.md)
