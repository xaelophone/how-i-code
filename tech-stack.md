# Default Tech Stack

> Opinionated, battle-tested technologies for shipping apps fast. Two tiers depending on project complexity.

---

## Two Modes

I operate with two stacks depending on what I'm building:

- **Starter Stack** — For workshops, greenfield projects, and solo builders who want simplicity
- **Production Stack** — For complex apps with separate frontend/backend, AI features, and team workflows

Both are battle-tested. Start with the starter stack. Graduate to the production stack when you need more control.

---

## Starter Stack

Best for: solo projects, learning, workshops, anything where "one framework does everything" is a feature.

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

### Architecture

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

### Getting Started

1. `npx create-next-app@latest` with TypeScript and Tailwind
2. `npx shadcn@latest init` for components
3. Create a Supabase project at [supabase.com](https://supabase.com)
4. Deploy to Vercel by connecting your repo

From zero to deployed in under 30 minutes.

---

## Production Stack

Best for: complex apps with AI-powered features, real-time streaming, team workflows, and separate deployment targets.

| Layer | Technology | Why |
|-------|------------|-----|
| **Frontend** | React 19 + Vite 7 | Faster builds, more control than Next.js |
| **UI Components** | shadcn/ui + Radix UI | Same as starter—copy-paste, accessible |
| **Styling** | Tailwind CSS or CSS Modules | Depends on the project |
| **Language** | TypeScript | Non-negotiable |
| **Backend** | Express 5 | Full control over routes, middleware, SSE streaming |
| **Database** | PostgreSQL (Supabase) | Same as starter—real database, managed |
| **Auth** | Supabase Auth + JWKS | Asymmetric JWT verification via `jose` library |
| **AI** | Claude SDK + Claude Agent SDK | Agent SDK for MCP tools, session management, multi-turn agents |
| **Deployment** | Vercel (frontend) + Railway (backend) | Separate scaling, separate deploy targets |
| **Structure** | Monorepo (npm workspaces) | Shared types, coordinated deploys |

### Why Split Frontend and Backend?

The starter stack (Next.js API Routes) works great until you need:

- **SSE streaming** for real-time AI responses with fine-grained control
- **Claude Agent SDK** with MCP tools, session resumption, and multi-turn conversations
- **Separate scaling** — your backend may need different resources than your frontend
- **Independent deploys** — ship backend changes without rebuilding the frontend

When I hit these needs, I split. React + Vite handles the frontend. Express handles the backend. They deploy to different services but share types via the monorepo.

### Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                         YOUR BROWSER                            │
└─────────────────────────────────────────────────────────────────┘
          │                                       │
          ▼                                       ▼
┌──────────────────────┐               ┌──────────────────────┐
│  FRONTEND (Vercel)   │               │  BACKEND (Railway)   │
│                      │  ◄── SSE ──►  │                      │
│  React 19 + Vite 7   │               │  Express 5           │
│  shadcn/ui + Tailwind│               │  Claude Agent SDK    │
│  TypeScript          │               │  MCP tools           │
└──────────────────────┘               └──────────────────────┘
                    │                        │
                    ▼                        ▼
             ┌────────────┐           ┌────────────┐
             │  SUPABASE  │           │  ANTHROPIC │
             │            │           │            │
             │ • Postgres │           │ • Claude   │
             │ • Auth     │           │ • Agent SDK│
             │ • Storage  │           │ • Streaming│
             └────────────┘           └────────────┘
```

### Monorepo Structure

```
my-project/
├── apps/
│   └── web/          # React 19 + Vite 7
├── server/           # Express 5 + Claude Agent SDK
├── packages/
│   └── shared/       # Shared types, utilities
├── package.json      # Workspace root
└── .github/
    └── workflows/    # CI/CD pipeline
```

**Lockfile lesson learned:** Always run `npm install` from the repo root. For isolated server installs (e.g., Railway deploy), use `npm --workspaces=false ci --prefix ./server`. Root lockfile can silently lose transitive deps when adding server packages—always verify both servers start after dep changes.

---

## CI/CD Pipeline

For production projects, I run a full CI/CD pipeline:

```
PR Opened → 5 parallel checks (typecheck, build, test, server-deploy-check, lint)
         → All pass → deploy-staging (Vercel frontend + Railway backend)
         → Merge to main → production deploys
```

GitHub Actions runs the checks. Staging deploys happen on every PR so you can verify before merge. Production deploys trigger on merge to main.

---

## When to Deviate

**Need a separate backend?** Graduate from the starter stack to the production stack.

**Need real-time multiplayer?** Add [Liveblocks](https://liveblocks.io/) or [PartyKit](https://partykit.io/).

**Heavy compute or ML?** Use [Modal](https://modal.com/) or [Replicate](https://replicate.com/) instead of Edge Functions.

**Enterprise requirements?** Swap Supabase for your company's approved database. The rest stays the same.

**Mobile app?** Consider [Expo](https://expo.dev/) + React Native, keeping the Supabase backend.

**Not building with AI?** Drop the Claude SDK. Everything else still applies.

---

## Next

Ready to build? Start with the [QUICKSTART](./QUICKSTART.md) workflow.
