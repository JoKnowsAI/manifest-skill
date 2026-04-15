---
name: jo-manifest
description: Lightweight project state and decision tracking for agent sessions. Use BEFORE starting work and THROUGHOUT development to track project context, tech decisions, requirements, and phase progress. Agents automatically read .manifest/ to understand project state without re-asking. Triggers on: "initialize project", "start new project", "what was our stack", "what phase are we in", "track this decision", or any request to start building or understand project state.
---

# Manifest — Project State Tracking

Stop re-explaining your project every session. Manifest captures project context once so agents understand your work without asking.

## The Problem It Solves

**Without Manifest:**
- Session 1: Explain your stack, requirements, design decisions — 1 hour
- Session 2: Agent asks "What's your tech stack?" — re-explain 30 min
- Session 3: "What was the requirement for X?" — find it again
- Sessions 4+: Same questions, same waste

**With Manifest:**
- Session 1: Initialize `.manifest/` with project info — 15 min
- Session 2+: Agent reads `.manifest/` automatically, no questions

---

## What Manifest Tracks

### `.manifest/PROJECT.md`
**What are you building and why?**
```markdown
# Project: Studio 23 TTL

## What
Photography/videography studio website with online booking

## Why
- Premium clients want to book online, not email back-and-forth
- Nightclub photography is a niche, need to show it
- Revenue goal: $X/month from bookings

## Success Criteria
- 10+ bookings/month within 3 months
- Mobile-responsive
- Sub-2s homepage load time
```

### `.manifest/STACK.md`
**Tech choices (decided once, not per phase)**
```markdown
# Tech Stack

## Frontend
- Framework: Next.js (server-side rendering, fast, cheap hosting)
- Styling: Tailwind CSS (utility-first, works with shadcn)
- Components: shadcn/ui (accessible, consistent)

## Backend
- Runtime: Node.js
- Database: Postgres (handles concurrent bookings, ACID compliance)
- ORM: Drizzle (type-safe, lightweight)

## Infrastructure
- Hosting: Vercel (frontend), Railway (backend) — both have free tiers
- Email: Resend (transactional emails, clean API)
- Payments: Stripe (handles recurring, subscriptions, webhooks)

## Why These Choices
- Next.js: One language (TypeScript), server-side rendering for SEO
- Postgres: Booking conflicts need proper locking, not SQLite
- Drizzle: Type safety reduces bugs in queries
- Stripe: Better for subscription/retainer clients (common in premium photography)
```

### `.manifest/DECISIONS.md`
**Why you chose things (decision audit trail)**
```markdown
# Architecture Decisions

## Decision: Next.js over plain React
- **Status:** Approved
- **Date:** 2026-04-14
- **Context:** Multiple projects use Next.js (NGTV, future projects)
- **Rationale:** Server-side rendering helps with SEO for "photography near me" searches
- **Trade-offs:** More opinionated than plain React, but learning curve already paid
- **Decision maker:** Jo

## Decision: Postgres over SQLite
- **Status:** Approved
- **Date:** 2026-04-14
- **Context:** Booking system needs to handle concurrent reservations
- **Rationale:** Postgres enforces ACID transactions, prevents double-bookings
- **Trade-offs:** Self-hosting Postgres is slightly more overhead than SQLite file
- **Decision maker:** Jo

## Decision: Resend over Mailchimp
- **Status:** Approved
- **Date:** 2026-04-14
- **Rationale:** Transactional email API (cleaner for booking confirmations), cheaper
- **Trade-offs:** No built-in templates like Mailchimp, but you control sending
- **Decision maker:** Jo
```

### `.manifest/REQUIREMENTS.md`
**What success looks like (test against these)**
```markdown
# Project Requirements

## Phase 1: Booking System
- [ ] Online calendar shows availability (edit hours in admin)
- [ ] Clients can book a time slot
- [ ] Booking confirmation email sent within 2s
- [ ] Admin dashboard shows all bookings
- [ ] Prevent double-booking (concurrent requests handled)

## Phase 2: Portfolio Gallery
- [ ] Nightclub photography portfolio with 20+ images
- [ ] Gallery loads in <2s (lazy-load images)
- [ ] Mobile-responsive layout (vertical on mobile, grid on desktop)
- [ ] Each photo has description, location, date

## Phase 3: Client Testimonials + Payments
- [ ] Payment processing via Stripe (deposit + final payment option)
- [ ] Client testimonials section with photos
- [ ] Email reminders for unpaid invoices
- [ ] Pricing page (tiered: hourly, packages, retainers)

## Non-Functional
- [ ] Mobile-first design
- [ ] Sub-2s page load (Core Web Vitals)
- [ ] Accessible (WCAG 2.1 AA)
- [ ] GDPR-compliant (EU visitors)
```

### `.manifest/PHASE.md`
**Current progress (agents know where you are)**
```markdown
# Project Phase Tracker

## Current Phase
**Phase 1: Booking System** (In Progress)

## Phase Status
- Started: 2026-04-14
- Estimated completion: 2026-04-28
- Blocker: None
- Risk: Postgres setup on Mac Mini (self-hosted)

## Completed Phases
(none yet)

## Next Phases
1. Phase 2: Portfolio Gallery (start 2026-04-29)
2. Phase 3: Client Testimonials + Payments (start 2026-05-13)

## Phase 1 Deliverables
- [ ] Next.js project scaffolded
- [ ] Postgres + Drizzle schema for bookings
- [ ] Calendar component (check availability)
- [ ] Booking form (client-facing)
- [ ] Admin dashboard (view/edit bookings)
- [ ] Resend email integration (confirmation emails)
- [ ] Deploy to Vercel + Railway
```

---

## How Agents Use It

When you start a session and ask *"Let's continue building the booking system"* or *"What's our stack?"*

Agent reads `.manifest/` and:
1. ✅ Knows the project goal (Studio 23 TTL, photography booking site)
2. ✅ Knows the stack (Next.js, Postgres, Stripe)
3. ✅ Knows why you chose it (why Postgres, not SQLite)
4. ✅ Knows the requirements (what "done" looks like)
5. ✅ Knows the phase (Phase 1, in progress, next phase is portfolio)

**Result:** No re-explaining. Agent starts building immediately.

---

## Manifest Commands

### Initialize a New Project
```
/manifest init "Project Name"
```
Creates `.manifest/` with templates for PROJECT.md, STACK.md, DECISIONS.md, REQUIREMENTS.md, PHASE.md

### Check Project Status
```
/manifest status
```
Reads `.manifest/PHASE.md` and shows current phase, progress, next steps

### Move to Next Phase
```
/manifest phase-next "Phase 2: Feature Name"
```
Archives current phase in `.manifest/ARCHIVE/`, creates new PHASE.md

### Log a Decision
```
/manifest decision "Decision Name" "Why you chose it" "Trade-offs"
```
Appends to `.manifest/DECISIONS.md` with timestamp

### Update Requirements
```
/manifest requirements-check
```
Shows which requirements are done (✅) vs pending (☐)

---

## File Organization

```
project-root/
├── .manifest/
│   ├── PROJECT.md           ← What + Why
│   ├── STACK.md             ← Tech choices (once)
│   ├── DECISIONS.md         ← Why you chose things
│   ├── REQUIREMENTS.md      ← Success criteria per phase
│   ├── PHASE.md             ← Current progress
│   └── ARCHIVE/
│       └── Phase-1.md       ← Previous phases (for reference)
├── src/
├── package.json
├── etc.
```

---

## When to Use This Skill

✅ **Use Manifest:**
- Starting a new project (initialize immediately)
- Continuing a project (read PHASE.md first)
- Making an architecture decision (log it in DECISIONS.md)
- Moving to next phase (run `/manifest phase-next`)
- Asking agent "what's our stack?" (it reads STACK.md)

❌ **Skip Manifest for:**
- Quick bug fixes or one-off scripts
- Exploratory prototyping (doesn't need formal tracking)

---

## The Philosophy

Projects fail not because agents can't code, but because **context gets lost between sessions**. Manifest captures context once so it's always available.

Think of `.manifest/` as your project's **institutional memory**. Your future self (and any agent) can read it and understand: *what you're building, why you chose that tech, what success looks like, and where you are now.*

See `references/manifest-templates.md` for ready-to-use templates.
See `references/manifest-patterns.md` for examples from real projects.
