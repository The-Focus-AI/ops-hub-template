# CLAUDE.md

Context for Claude Code about this workspace.

## About

Operations hub for [COMPANY_NAME]. Tracking client projects, product development, labs research, and marketing. The dashboard is `README.md` - updated daily via `/daily`.

## Organization

**GitHub Org**: [GITHUB_ORG]
**Stack**: [STACK] <!-- e.g. TypeScript, pnpm, Vercel/Supabase -->

## Active Client Projects

<!-- Add rows as you onboard clients. This table is read by /daily, /weekly, and /client-update. -->

| Client | Contact | Status |
|--------|---------|--------|
| <!-- Example: Acme Corp --> | <!-- Jane Smith --> | <!-- Phase 1 - Active --> |

Details: `projects/clients/*.md`
Weekly reports: `projects/clients/*/YYYY-W*.md`

## Team

| Person | Role | Projects |
|--------|------|----------|
| <!-- Your Name --> | <!-- Lead --> | <!-- All --> |

## Key Files

| File | Purpose |
|------|---------|
| `README.md` | Live dashboard (updated via /daily, regenerated via /weekly) |
| `invoices.md` | All invoices (paid/outstanding) |
| `tasks.md` | Task backlog |
| `sales.md` | Sales pipeline |
| `content.md` | Newsletter history, ideas, schedule |
| `projects/clients/` | Client project docs |
| `projects/clients/*/meetings/` | Client meeting transcripts |
| `projects/clients/*/YYYY-W*.md` | Weekly activity reports |
| `projects/internal/` | Internal projects |
| `projects/labs/` | Labs/research projects |
| `projects/product/` | Product development |
| `hiring/` | Job postings and applications |
| `hiring/meetings/` | Interview transcripts |
| `sales/meetings/` | Sales call transcripts |
| `team/` | Employee contracts and HR docs |
| `finances/` | Financial tracking system |
| `finances/subscriptions.md` | Recurring subscriptions (KEEP/CANCEL/INVESTIGATE) |
| `finances/expenses.md` | Monthly expense breakdown by category |
| `finances/contractors.md` | Contractor rates & hours |

## Commands

| Command | Purpose |
|---------|---------|
| `/sync` | Pull from external sources (GitHub activity, optional: meetings, newsletter) |
| `/daily` | Morning briefing + update README.md text |
| `/weekly` | Weekly review + update all files + regenerate README |
| `/push` | Auto-commit and push |
| `/client-update <client>` | Create DRAFT status email for client (never sends directly) |

## Skills

### Finance Tracking

**Key Files:**
- `invoices.md` - Master invoice log (paid/outstanding by client)
- `finances/subscriptions.md` - Recurring subscriptions audit
- `finances/expenses.md` - Monthly expense breakdown
- Bank statements in `finances/*.csv`

**When updating finances:**

1. **Revenue tracking** - Use `invoices.md` as source of truth:
   - Mark invoices paid when confirmed (wire/ACH received)
   - Update README.md "Paid This Month" from paid invoices
   - Update README.md "Outstanding" from unpaid invoices
   - Cross-reference with bank statement deposits

2. **Expense tracking** - Update `finances/expenses.md`:
   - Categorize expenses by your defined categories
   - Common categories: Contractors, Software, Office, Travel

3. **Subscription audit** - Keep `finances/subscriptions.md` current:
   - KEEP = actively used for business
   - CANCEL = not needed, add to tasks.md
   - INVESTIGATE = unclear what it's for

4. **Monthly reconciliation** (during `/weekly`):
   - Compare invoices.md paid amounts to bank deposits
   - Compare subscriptions.md to actual charges
   - Flag any discrepancies

<!-- ====================================================================
OPTIONAL SKILLS - Uncomment and configure as needed
======================================================================== -->

<!-- OPTIONAL: Talent Search — uncomment if using hiring/

### Talent Search

When asked to find candidates with specific skills:

1. **Ask clarifying questions first:**
   - What skills/experience are you looking for?
   - Is this for a specific project or general pipeline building?
   - Any rate/timezone constraints?

2. **Search through our talent pool:**
   - `hiring/applications/*.md` - All job applicants with evaluations
   - `hiring/meetings/*.md` - Interview transcripts
   - `team/*.md` - Current team members and contracts

3. **For each relevant candidate, extract:**
   - Name and contact (email, LinkedIn, GitHub)
   - Rate and location/timezone
   - Relevant experience (why they match)
   - Current status (hired, declined, pending, etc.)
   - Any red flags or concerns noted

4. **Draft a summary** with:
   - Table of candidates with rates, locations, links
   - Explanation of why each is relevant
   - Clear recommendation on next steps
-->

<!-- OPTIONAL: Newsletter — requires Buttondown or similar

### Newsletter

**API Key**: [Where your API key is stored]

**Pull Newsletter Stats** (use in `/sync` and `/weekly`):
- Get subscriber count
- Get recent emails with engagement stats

**Create Newsletter Draft**:
- Create draft via API
- Review before scheduling/sending

**CRITICAL**: Deliver full text in newsletter. No summaries, no excerpts, no "click to read more".
-->

<!-- OPTIONAL: Image Generation — requires an image generation tool/API

### Infographic Generation

**Brand Colors** (customize for your company):
- Background: [BG_COLOR]
- Primary: [PRIMARY_COLOR]
- Accent: [ACCENT_COLOR]
- Font: [FONT]

Used by `/weekly` to generate visual status infographics.
-->

## Style

- Be direct, skip fluff
- Document as you go
- Ship -> Document -> Market -> Follow-up
- Use tasks.md to track tasks
