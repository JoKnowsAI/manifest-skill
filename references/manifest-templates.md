# Manifest Templates — Copy & Customize

Use these as starting points for your projects.

---

## PROJECT.md Template

```markdown
# Project: [Project Name]

## What
[One sentence: what are you building?]

## Why
- [Reason 1]
- [Reason 2]
- [Business metric or personal goal]

## Success Criteria
- [Measurable outcome 1]
- [Measurable outcome 2]
- [Technical requirement 1]
- [Technical requirement 2]

## Timeline
- Start date: [date]
- Target completion: [date]
- Status: [Ideation / Planning / In Progress / Shipped]

## Key Stakeholders
- You: [Your role]
- [Other people involved, if any]
```

---

## STACK.md Template

```markdown
# Tech Stack

## Frontend
- Framework: [e.g., Next.js, React, Vue]
- Styling: [e.g., Tailwind, CSS Modules]
- Components: [e.g., shadcn/ui, Material-UI]
- State: [e.g., React Query, Zustand]

## Backend
- Runtime: [e.g., Node.js, Python, Go]
- Framework: [e.g., Express, FastAPI]
- Database: [e.g., Postgres, MongoDB]
- ORM/Query: [e.g., Drizzle, Prisma, SQLAlchemy]

## Infrastructure
- Hosting (Frontend): [e.g., Vercel, Netlify]
- Hosting (Backend): [e.g., Railway, Render, AWS]
- Database Hosting: [e.g., AWS RDS, Supabase]
- Email: [e.g., Resend, SendGrid]
- Authentication: [e.g., Auth0, Clerk, NextAuth]
- Payments: [e.g., Stripe, Lemonsqueezy]

## Why These Choices
[1-2 sentences for each major choice explaining rationale]
- Framework: [why chosen]
- Database: [why chosen]
- Hosting: [why chosen]

## Trade-offs
- [What you gave up to use this stack]
- [What's harder to do with this stack]
- [What you gain in return]
```

---

## DECISIONS.md Template

```markdown
# Architecture Decisions

## Decision: [Decision Title]
- **Status:** [Approved / Pending / Rejected]
- **Date:** [YYYY-MM-DD]
- **Context:** [What problem were you solving?]
- **Rationale:** [Why you chose this option]
- **Alternatives Considered:** [What you didn't choose and why]
- **Trade-offs:** [What you give up]
- **Decision Maker:** [Your name or team]

## Decision: [Decision Title]
[Repeat format above]
```

---

## REQUIREMENTS.md Template

```markdown
# Project Requirements

## Phase 1: [Phase Name]
### Feature: [Feature Name]
- [ ] [Requirement 1]
- [ ] [Requirement 2]
- [ ] [Requirement 3]

### Feature: [Feature Name]
- [ ] [Requirement 1]
- [ ] [Requirement 2]

### Non-Functional Requirements
- [ ] Performance: [metric, e.g., <2s load time]
- [ ] Accessibility: [standard, e.g., WCAG 2.1 AA]
- [ ] Security: [requirement, e.g., HTTPS, input validation]
- [ ] Mobile: [requirement, e.g., responsive design]

## Phase 2: [Phase Name]
[Repeat Phase 1 structure]

## Phase 3: [Phase Name]
[Repeat Phase 1 structure]
```

---

## PHASE.md Template

```markdown
# Project Phase Tracker

## Current Phase
**Phase [N]: [Phase Name]** ([Status: In Progress / Paused / Completed])

## Phase Timeline
- Started: [YYYY-MM-DD]
- Estimated completion: [YYYY-MM-DD]
- Actual completion: [YYYY-MM-DD] (fill when done)

## Current Blockers
- [Blocker 1]
- [Blocker 2]
(Leave blank if none)

## Risks
- [Risk 1 and mitigation]
- [Risk 2 and mitigation]

## Completed Phases
- Phase 1: [Name] (completed [date])
- Phase 2: [Name] (completed [date])

## Next Phases
1. Phase [N+1]: [Name] (start [date])
2. Phase [N+2]: [Name] (start [date])

## Current Phase Deliverables
- [ ] [Deliverable 1]
- [ ] [Deliverable 2]
- [ ] [Deliverable 3]

## Notes
[Any relevant context about current phase]
```

---

## Real Example: Northgate TV Outreach System

### PROJECT.md
```markdown
# Project: NGTV Outreach Automation

## What
Automated email outreach system for selling advertising to 67 local BCS businesses

## Why
- 450K monthly Instagram views but zero revenue
- Manual outreach takes 20+ hours/month
- Automating = can reach all 67 businesses consistently
- Goal: Convert 10% (7 businesses) into $200/month sponsors = $1.4K/month recurring

## Success Criteria
- All 67 businesses contacted in <2 hours (automated)
- Email opens tracked
- Reply rates measured
- Lead status tracked (contacted → interested → closed)
- First sponsor signed within 30 days

## Timeline
- Start: 2026-04-15
- Target: 2026-05-15 (first sponsor)
```

### STACK.md
```markdown
# Tech Stack

## Frontend
- Next.js (dashboard to view leads + send sequences)
- Tailwind CSS

## Backend
- Node.js
- Airtable (lead tracking, automation rules)
- Resend (email sending)

## Infrastructure
- Vercel (Next.js)
- Airtable API
- Resend API

## Why
- Airtable: You already use CSV, Airtable is visual UI + API
- Resend: Clean transactional email API, $0.10 per email
- Next.js: Same stack as Studio 23 (learning curve already paid)
```

### DECISIONS.md
```markdown
# Decisions

## Decision: Airtable over custom database
- **Status:** Approved
- **Rationale:** Lead tracking + automation in one place, visual UI, no database setup
- **Trade-offs:** Airtable costs $10/month (vs free Postgres), but saves 20 hours setup
- **Maker:** Jo

## Decision: Resend over Mailchimp
- **Status:** Approved
- **Rationale:** Transactional API (cleaner), cheaper at scale, integrates with Node.js
- **Maker:** Jo
```

### REQUIREMENTS.md
```markdown
# NGTV Outreach Requirements

## Phase 1: Lead Import + Email Sequence
- [ ] Import 67 businesses from CSV
- [ ] Airtable synced (name, email, category)
- [ ] 3-email sequence defined and tested
- [ ] Personalized emails (Hi [Name], Northgate TV saw you're in [Category])
- [ ] Email tracking (opens, clicks)
- [ ] Lead status workflow (Contacted → Interested → Closed → Sponsor)

## Phase 2: Dashboard
- [ ] View all leads and status
- [ ] Manual override (mark as interested, send follow-up)
- [ ] Analytics (open rate, reply rate, conversion rate)

## Phase 3: Automation
- [ ] Auto follow-up if no reply in 3 days
- [ ] Auto escalate after 3 emails
- [ ] Calendar blocking for manual follow-up calls
```

### PHASE.md
```markdown
# NGTV Outreach Phase Tracker

## Current Phase
**Phase 1: Lead Import + Email Sequence** (In Progress)

## Timeline
- Started: 2026-04-15
- Target completion: 2026-04-30

## Blockers
- None (Airtable account ready, Resend API key ready)

## Deliverables
- [ ] CSV imported to Airtable (67 businesses)
- [ ] Email template #1 written + personalization set up
- [ ] Email template #2 written (follow-up after 3 days)
- [ ] Email template #3 written (final ask)
- [ ] Test sequence sent to self
- [ ] Lead status workflow created in Airtable
```
