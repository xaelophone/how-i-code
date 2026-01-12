# Updates

A log of how my coding practices are evolving.

> **What belongs here:** Only commits that change how I work—new workflows, shifted mental models, tool choices, process changes. Not every commit to this repo.

<!--
To generate a new entry, run:
git log -1 --pretty=format:"## %ad%n%n**%s**%n%n[Add narrative here]%n%n**Files changed:** " --date=format:"%B %d, %Y" --name-only

Then edit to add the narrative paragraph explaining the "why" behind the change.
-->

---

## January 12, 2026

**Documented default tech stack**

Added [tech-stack.md](./tech-stack.md) capturing my go-to technologies: Next.js, React, TypeScript, Tailwind, Supabase, Vercel. Includes architecture diagram showing how the pieces connect. This is the stack I reach for by default when starting a new project.

**Files changed:** `tech-stack.md`, `README.md`

---

## January 9, 2026

**Shifted from line-by-line to architecture-level comprehension**

Updated the [Comprehensible Code](./frameworks/01-comprehensible-code.md) framework. The old approach was understanding every line. The new approach: trust multi-round AI review (`/simplify-code` → draft PR → `/code-review` → address feedback) to catch details while focusing on architectural judgment.

**Files changed:** `QUICKSTART.md`, `frameworks/01-comprehensible-code.md`

---

## December 15, 2025

**Initial release**

First public version of "Learning to Speak Code"—frameworks, cheatsheets, and examples for non-technical people shipping code with AI.
