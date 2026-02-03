---
description: Interactive setup wizard for your operations hub
---

# Operations Hub Setup

You are setting up a new operations hub. Guide the user through configuration step by step. Be conversational — this is an onboarding experience, not a form.

## Step 1: Company Basics

Ask the user:

1. **What's your company name?**
2. **What do you do?** (consulting, agency, freelance, etc.) — use this to set the tone of CLAUDE.md
3. **What's your tech stack?** (e.g. "TypeScript, pnpm, Vercel/Supabase" — or "not technical, just tracking")
4. **Do you have a GitHub organization?** If yes, what's the org name?
5. **Who's on your team?** Names, roles, and what they work on.

After getting answers, update `CLAUDE.md`:
- Replace `[COMPANY_NAME]` with their company name
- Replace `[GITHUB_ORG]` with their GitHub org (or remove the line if none)
- Replace `[STACK]` with their stack
- Fill in the Team table
- Update the About section with what they do

## Step 2: Integrations

Ask the user which integrations they want to enable. Present as a checklist:

> Which of these would you like to connect? (You can always add more later)
>
> - **Gmail & Google Calendar** — Pull in recent emails and events to seed tasks and identify clients
> - **Meeting notes (Granola)** — Auto-import meeting transcripts to client folders
> - **Newsletter (Buttondown)** — Track subscribers and create newsletter drafts
> - **GitHub** — Sync commit activity into weekly reports
> - **None for now** — Just use markdown files manually

For each selected integration:

### Gmail & Calendar (google-skill)

Check if the google-skill plugin is installed:
```bash
ls ~/.claude/plugins/cache/focus-marketplace/google-skill/ 2>/dev/null
```

If not installed, tell the user:
```
You'll need to install the Google plugin first. Run:
  claude plugin install google-skill@focus-marketplace
Then restart Claude Code and run /setup again.
```

If installed, trigger the Gmail OAuth flow by using the gmail skill to list recent emails. This will prompt for authentication if needed.

Once authenticated:

1. **Pull recent emails (last 14 days):**
   - Use the gmail skill to search for emails
   - Look for patterns: invoice mentions, client names, meeting scheduling, project discussions
   - Present a summary: "I found emails with these people/companies: [list]. Which of these are clients?"

2. **Pull calendar events (next 7 days + last 7 days):**
   - Use the gmail skill (which includes calendar) to list events
   - Present upcoming meetings: "You have these meetings coming up: [list]. Want me to create task reminders for any of these?"

3. **Seed tasks from emails:**
   - For any emails that look like action items, invoices to send, or follow-ups needed, offer to add them to `tasks.md`
   - Ask: "Want me to add these to your task list?"

### Meeting Notes (granola-skill)

Check if granola-skill is installed. If yes:
- Pull recent meetings (last 14 days)
- For each meeting, ask: "Which client does this belong to?" and route to the right folder
- If no client folders exist yet, use the meeting data to help identify clients (see Step 3)

### Newsletter (buttondown-skill)

Check if buttondown-skill is installed. If yes:
- Pull subscriber count and recent emails
- Update `content.md` with the stats and archive

### GitHub

If they provided a GitHub org:
- Update `.claude/commands/sync.md` — replace `[YOUR_GITHUB_ORG]` with their org
- Fetch recent repos: `gh repo list {ORG} --limit 30 --json name,pushedAt,description --jq '.[] | select(.pushedAt > "DATE_14_DAYS_AGO")'`
- Present the list: "These repos had recent activity. Which ones map to which projects?"
- Build the repo mapping table in `sync.md`
- Run the first sync to generate weekly reports

## Step 3: Identify Clients

Based on what we found in emails, calendar, and meetings, ask:

> Based on what I've seen, it looks like you're working with: [list of names/companies from emails and calendar]
>
> **Who are your active clients?** For each one, I need:
> - Company name
> - Primary contact (name and email)
> - What phase are they in? (discovery, active development, maintenance, etc.)
> - Any repos associated with this client?

For each client identified:
1. Create the client directory: `mkdir -p projects/clients/{client-slug}/meetings`
2. Create the client overview file from `_template.md`
3. Fill in what we know from emails/calendar
4. Add to the Active Client Projects table in `CLAUDE.md`
5. Add an invoice section in `invoices.md`

Ask: "Do you have any existing documents for these clients — proposals, scopes, contracts? You can drop PDFs into the `scopes/` folder and I'll extract the details."

## Step 4: Process Dropped Documents

Check for any files in these folders:

```bash
ls invoices/*.pdf invoices/*.PDF scopes/*.pdf scopes/*.PDF team/*.pdf team/*.PDF 2>/dev/null
```

For each PDF found:

### Invoices (`invoices/`)
- Read the PDF and extract: client name, invoice number, amount, date, description
- Add to `invoices.md` under the matching client section
- Add to `finances/revenue.md`
- Ask: "Is this invoice paid or outstanding?"

### Scopes (`scopes/`)
- Read the PDF and extract: client name, project scope, phases, amounts, timeline
- Update the matching client's project file with scope details
- If the client doesn't exist yet, ask if this is a new client and create them

### Team documents (`team/`)
- Read the PDF and extract: person name, role, rate, terms
- Add to `finances/contractors.md` if it's a contractor agreement
- Save key details to `team/{name}.md`

## Step 5: Financial Setup

Ask:
> Do you want to set up financial tracking? I can help with:
> - **Expense categories** — What categories make sense for your business? (defaults: Contractors, Software, Office, Travel, Professional)
> - **Recurring costs** — Any subscriptions or recurring charges to track?
> - **Bank statements** — You can drop CSV exports into `finances/` and I'll categorize them

If yes:
- Customize expense categories in `finances/expenses.md`
- Add any known subscriptions to `finances/subscriptions.md`
- Process any CSV files in `finances/`

## Step 6: Generate First Dashboard

Now generate the initial `README.md` dashboard with all the data we've collected:

1. Set the company name in the title
2. Fill in the invoice summary from `invoices.md`
3. Create the "Urgent This Week" table from `tasks.md`
4. Fill in the Client Health Overview from the client files
5. Add Active Client Projects sections
6. Fill in Sales Pipeline from `sales.md`
7. Add Team section
8. Add Revenue Summary
9. Set "Last updated" to today

## Step 7: Summary

Output a final summary:

```
SETUP COMPLETE

Company: {name}
Clients: {count} configured
  {list with status}

Integrations:
  ✓ Gmail & Calendar (connected)
  ✓ GitHub ({org})
  ✗ Meeting notes (not configured)
  ✗ Newsletter (not configured)

Files updated:
  - CLAUDE.md (company context)
  - README.md (dashboard)
  - tasks.md ({count} tasks)
  - invoices.md ({count} invoices)
  - projects/clients/ ({count} clients)

Documents processed:
  - {count} invoices from invoices/
  - {count} scopes from scopes/
  - {count} team docs from team/

NEXT STEPS:
  /daily    — Run your first morning briefing
  /push     — Commit everything to git
  /weekly   — Run at end of week for full review

Drop more PDFs into invoices/, scopes/, or team/ anytime — Claude will process them.
```

## Notes for Claude

- Be conversational throughout. Don't dump all questions at once — go step by step.
- If the user says "skip" or "later" for any section, move on. Everything can be configured later.
- When creating files, use the existing templates in `projects/clients/_template.md`
- The `_example-client/` directory is for reference — don't modify it, but you can point the user to it as an example.
- If plugins aren't installed, don't block — tell the user how to install and come back.
- Always ask before writing to files. Show what you plan to add and confirm.
