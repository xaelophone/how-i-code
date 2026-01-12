# Default Tech Stack

> My go-to technologies for shipping apps fast. Opinionated, battle-tested, designed for solo builders and small teams.

---

## Quick Reference

| Layer | Technology | Why |
|-------|------------|-----|
| **Frontend** | Next.js + React | Full-stack in one framework, great DX |
| **UI Components** | shadcn/ui + Radix UI | Copy-paste components, accessible by default |
| **Styling** | Tailwind CSS | Fast iteration, no context switching |
| **Language** | TypeScript | Catches bugs before runtime, better AI output |
| **Backend** | Next.js API Routes | No separate server to manage |
| **Database** | PostgreSQL (Supabase) | Real database with managed hosting |
| **Auth** | Supabase Auth | OAuth in minutes, not hours |
| **Storage** | Supabase Storage | File uploads without AWS headaches |
| **AI** | Anthropic Claude SDK | Best reasoning, streaming built-in |
| **Deployment** | Vercel | Push to deploy, zero config |

---

## Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                         YOUR BROWSER                            │
└─────────────────────────────────────────────────────────────────┘
                                │
                                ▼
┌─────────────────────────────────────────────────────────────────┐
│                    NEXT.JS APPLICATION                          │
│  ┌───────────────────────────────────────────────────────────┐  │
│  │  FRONTEND (React + TypeScript)                            │  │
│  │  • Pages & Components                                     │  │
│  │  • shadcn/ui + Radix UI                                   │  │
│  │  • Tailwind CSS                                           │  │
│  └───────────────────────────────────────────────────────────┘  │
│  ┌───────────────────────────────────────────────────────────┐  │
│  │  BACKEND (Next.js API Routes)                             │  │
│  │  • RESTful endpoints                                      │  │
│  │  • Streaming responses                                    │  │
│  │  • Server-side auth                                       │  │
│  └───────────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────────┘
          │                    │                    │
          ▼                    ▼                    ▼
   ┌────────────┐       ┌────────────┐       ┌────────────┐
   │  SUPABASE  │       │  ANTHROPIC │       │   VERCEL   │
   │            │       │  (Claude)  │       │            │
   │ • Postgres │       │            │       │ • Hosting  │
   │ • Auth     │       │ • AI/LLM   │       │ • Edge     │
   │ • Storage  │       │ • Streaming│       │ • CI/CD    │
   └────────────┘       └────────────┘       └────────────┘
```

---

## Why This Stack

### Next.js + React
One framework handles frontend, backend, and deployment. No separate Express server. No CORS headaches. The App Router gives you server components by default—faster pages, simpler data fetching.

### shadcn/ui + Tailwind
You copy the component code into your repo. No fighting with library updates. Radix handles accessibility. Tailwind means you style in the same file you're coding—no CSS file switching.

### TypeScript
AI writes better code when it has types to work with. You catch bugs before they hit production. The investment pays off immediately.

### Supabase
PostgreSQL without DevOps. Auth, storage, and real-time subscriptions from one dashboard. The free tier handles side projects. Row Level Security means your data rules live in the database, not scattered across API routes.

### Vercel
Git push → live site. Preview deployments for every PR. Edge functions when you need them. The integration with Next.js is seamless—they made both.

### Claude SDK
Best reasoning of any model. Streaming responses work out of the box. The TypeScript SDK has good types.

---

## When to Deviate

**Need real-time multiplayer?** Add [Liveblocks](https://liveblocks.io/) or [PartyKit](https://partykit.io/).

**Heavy compute or ML?** Use [Modal](https://modal.com/) or [Replicate](https://replicate.com/) instead of Edge Functions.

**Enterprise requirements?** Swap Supabase for your company's approved database. The rest stays the same.

**Mobile app?** Consider [Expo](https://expo.dev/) + React Native, keeping the Supabase backend.

**Not building with AI?** Drop the Claude SDK. Everything else still applies.

---

## Getting Started

1. `npx create-next-app@latest` with TypeScript and Tailwind
2. `npx shadcn@latest init` for components
3. Create a Supabase project at [supabase.com](https://supabase.com)
4. Deploy to Vercel by connecting your repo

From zero to deployed in under 30 minutes.

---

## Next

Ready to build? Start with the [QUICKSTART](./QUICKSTART.md) workflow.
