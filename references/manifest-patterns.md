# Manifest Patterns — How to Use Effectively

Real-world patterns for tracking your projects.

---

## Pattern 1: Multi-Project Stack Reuse

**Scenario:** You have Studio 23 TTL and NGTV using the same tech stack (Next.js, Node.js, Postgres).

### Setup

**Studio 23 STACK.md:**
```markdown
# Tech Stack

## Frontend: Next.js + Tailwind + shadcn/ui
## Backend: Node.js + Postgres + Drizzle
## Hosting: Vercel + Railway
```

**NGTV STACK.md:**
```markdown
# Tech Stack

## Frontend: Next.js + Tailwind + shadcn/ui
(Same as Studio 23 — see ../studio-23-ttl/.manifest/STACK.md)

## Backend: Node.js + Airtable API + Resend
(Different backend, but same frontend stack for consistency)
```

**Benefit:** When you start a new project, copy the STACK.md format, reuse what works, modify what's different. Consistency + speed.

---

## Pattern 2: Phase-Based Development Tracking

**Scenario:** You're building NGTV outreach system across 3 phases, want to track progress without chaos.

### Initial PHASE.md
```markdown
# NGTV Outreach Phases

## Current: Phase 1 (2026-04-15 to 2026-04-30)
- [ ] Lead import + email setup
- [ ] Test with 5 leads
- [ ] Go live with all 67

## Phase 2 (2026-05-01 to 2026-05-15)
- [ ] Dashboard built
- [ ] Manual overrides working

## Phase 3 (2026-05-16+)
- [ ] Auto follow-ups
- [ ] Analytics
```

### When Moving to Phase 2
```bash
/manifest phase-next "Phase 2: Dashboard & Lead Management"
```

Archives Phase 1 to `.manifest/ARCHIVE/Phase-1.md`, creates new PHASE.md for Phase 2.

**Benefit:** Clear progress tracking. Agent knows exactly what phase you're in and what's next.

---

## Pattern 3: Decision Audit Trail

**Scenario:** 6 months from now, you need to remember *why* you chose Airtable over a custom database.

### Log Decisions as You Make Them

**DECISIONS.md (kept current):**
```markdown
## Decision: Airtable vs Custom DB for NGTV Leads
- **Date:** 2026-04-15
- **Status:** Approved
- **Context:** Need to track 67 businesses, automate outreach sequences
- **Rationale:** 
  - Airtable has visual UI (non-technical team can manage)
  - Built-in automation rules (email triggers, status updates)
  - API is clean and well-documented
- **Alternatives:**
  - Custom Postgres DB: More control, but 10+ hours setup, need admin panel
  - Google Sheets: Free, but no API for email integration
- **Trade-offs:** 
  - Airtable costs $10/month (vs free Postgres)
  - Limited to Airtable's API capabilities
  - Data lives in Airtable, not your own DB
- **Decision Maker:** Jo
```

**Benefit:** Future you (or your team) can read why you chose things. If Airtable stops working, you know the original reasoning and can re-evaluate.

---

## Pattern 4: Requirements Verification

**Scenario:** Phase 1 is "done" — but is it actually done?

### REQUIREMENTS.md (Checkboxes)

```markdown
# Phase 1: Booking System Requirements

## Feature: Calendar
- [x] Calendar loads with availability
- [x] Users can see 30 days out
- [x] Admin can block time off
- [ ] Calendar syncs with Google Calendar (DEFERRED to Phase 2)

## Feature: Booking Form
- [x] Users can select time + date
- [x] Email confirmation sent within 2s
- [x] Admin receives email copy
- [ ] SMS reminder 24h before (DEFERRED to Phase 2)

## Non-Functional
- [x] Mobile responsive
- [x] <2s load time
- [x] GDPR compliant
- [ ] Add dark mode (NICE-TO-HAVE, not Phase 1)
```

**When agent asks:** "Is Phase 1 done?"

You check REQUIREMENTS.md:
- ✅ Core features complete (calendar, form, confirmations)
- ⏳ Deferred features listed (know what's not in Phase 1)
- 🎯 Nice-to-haves identified (don't accidentally build them)

**Benefit:** Clear definition of "done" prevents scope creep.

---

## Pattern 5: Risk & Blocker Tracking

**Scenario:** You hit a problem mid-phase.

### PHASE.md Updated in Real-Time

```markdown
# Phase 1: Booking System (In Progress)

## Current Blockers
- [RESOLVED] Postgres self-hosting on Mac Mini: decided to use Railway instead (2026-04-16)
- [ACTIVE] Stripe test keys not validating: debugging (2026-04-17)

## Risks
- Risk: Concurrent booking conflicts under load
  - Mitigation: Load test with 100 concurrent users before Phase 2
- Risk: Email deliverability (welcome emails going to spam)
  - Mitigation: Use Resend (high reputation), set up SPF/DKIM
```

**Benefit:** Agent reads blockers, knows what's hard, can suggest solutions. Risks are documented for future reference.

---

## Pattern 6: Decision Reversals

**Scenario:** You chose X, but it's not working. You change to Y.

### Update DECISIONS.md

```markdown
## Decision: Airtable for lead tracking
- **Status:** [SUPERSEDED] → Use instead: Manifest Decision #5
- **Original Date:** 2026-04-15
- **Reversed Date:** 2026-05-01
- **Why reversed:** Airtable API rate limits hit at 200 leads, needed more flexibility
- **New decision:** Custom Postgres + Node.js API (see Decision #5)
- **Lesson learned:** Airtable great for <50 records, custom DB better for >200
```

**Benefit:** History preserved. You remember why you switched. Pattern recognized for future projects.

---

## Pattern 7: Cross-Project Lessons

**Scenario:** You're starting Project #3 and want to avoid mistakes from Projects #1 and #2.

### DECISIONS.md References Other Projects

```markdown
# NGTV Outreach Decisions

## Decision: Use Next.js (not plain React)
- **Rationale:** Server-side rendering for SEO, same stack as Studio 23
- **Reference:** See Studio 23 TTL .manifest/DECISIONS.md #1 for full reasoning
- **Status:** Approved

## Decision: Use Resend for email
- **Rationale:** Learned from NGTV Phase 1: Mailchimp webhooks unreliable at scale
- **Status:** Approved
```

**Benefit:** Decisions compound. Each project teaches you something; Manifest captures it for the next one.

---

## Pattern 8: Agent Handoff (Multi-Session Projects)

**Scenario:** Session 1 builds Phase 1. Session 2 builds Phase 2. Different agent.

### Session 1 (You + Agent A):
```markdown
# Current Phase: Phase 1 (COMPLETED)
- All Phase 1 requirements done (see REQUIREMENTS.md)
- Code deployed to Vercel + Railway
- Email sequence tested with 5 users

# Next Phase: Phase 2 (READY TO START)
- See PHASE.md for Phase 2 requirements
- See STACK.md for tech stack (no changes)
- See DECISIONS.md for architecture decisions made in Phase 1
```

### Session 2 (You + Agent B):
Agent reads `.manifest/` and knows:
- What Phase 1 built (don't re-ask)
- What Phase 2 requires (clear scope)
- What tech stack to use (no debate)
- Why certain decisions were made (understand context)

**Result:** Agent B builds Phase 2 immediately, no re-explaining.

---

## Quick Tips

### Keep It Updated
- Update `.manifest/` as you build, not after
- Add decisions immediately (don't wait until end of phase)
- Check off requirements as you ship them

### Keep It Lean
- PROJECT.md: 5-10 lines
- STACK.md: 20-30 lines
- DECISIONS.md: grows over time (1 decision = 10 lines)
- REQUIREMENTS.md: ~20 lines per phase
- PHASE.md: 30 lines, updated regularly

### Don't Over-Engineer
- It's not a Jira board
- It's not a spec document
- It's context capture so agents and future-you don't re-ask questions

### Commit It
```bash
git add .manifest/
git commit -m "Updated Phase 1 blockers and requirements"
```

Your `.manifest/` is part of your project history.
