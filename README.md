# Ops Hub

An AI-powered operations hub for consulting firms and agencies. Track clients, invoices, tasks, sales pipeline, hiring, and finances — all from markdown files managed by Claude Code.

## What It Does

You manage your business in plain markdown files. Claude Code reads them, understands the context, and gives you a daily briefing, weekly review, auto-generated client status emails, and a live dashboard — all from a conversation in your terminal.

**Built-in commands:**

| Command | What it does |
|---------|-------------|
| `/setup` | Interactive setup wizard — configure your company, connect integrations, import existing data |
| `/daily` | Morning briefing — surfaces priorities, outstanding invoices, what's stuck |
| `/weekly` | End-of-week review — what happened, what didn't, plan next week |
| `/sync` | Pull in GitHub activity, meeting notes, newsletter stats |
| `/client-update` | Generate branded status emails for clients (draft only, never auto-sends) |
| `/push` | Auto-commit and push with a generated commit message |

**Drop-in document processing:**

Put PDFs in these folders and Claude will extract and organize the data:

| Folder | What to drop in |
|--------|----------------|
| `invoices/` | Invoice PDFs — extracted into `invoices.md` and `finances/revenue.md` |
| `scopes/` | Scope documents, SOWs, proposals — extracted into client project files |
| `team/` | Contracts, agreements — extracted into team records |

## Getting Started

### 1. Install Claude Code

```bash
npm install -g @anthropic-ai/claude-code
```

### 2. Add the Focus Marketplace plugins

These plugins give Claude access to Gmail, Google Calendar, meeting notes, and more.

```bash
# Add the marketplace (one time)
claude plugin marketplace add The-Focus-AI/claude-marketplace
```

Restart Claude Code, then install the plugins you want:

```bash
# Recommended — Gmail and Google Calendar for email/calendar sync
claude plugin install google-skill@focus-marketplace

# Optional — pick what you use
claude plugin install granola-skill@focus-marketplace        # Meeting notes (Granola)
claude plugin install buttondown-skill@focus-marketplace     # Newsletter (Buttondown)
claude plugin install chrome-driver@focus-marketplace        # Browser automation
claude plugin install nano-banana@focus-marketplace          # Image generation (Gemini)
claude plugin install embeddings-search-skill@focus-marketplace  # Semantic document search
```

### 3. Clone and run setup

```bash
git clone https://github.com/The-Focus-AI/ops-hub-template.git my-ops
cd my-ops
claude
```

Then run:

```
/setup
```

The setup wizard will:
- Ask your company name, team, and tech stack
- Offer to connect Gmail and Google Calendar
- Pull in recent emails and calendar events to seed your task list
- Ask about your clients — who they are, where to find info
- Process any PDFs you've dropped into `invoices/`, `scopes/`, or `team/`
- Configure GitHub sync if you have a GitHub org
- Generate your first dashboard

### 4. Daily usage

```bash
cd my-ops
claude
```

Then: `/daily` for your morning briefing, `/weekly` for end-of-week review.

## How It Works

Everything lives in markdown files that Claude reads and writes:

```
my-ops/
├── CLAUDE.md              # Company context — Claude reads this first
├── README.md              # Live dashboard — auto-updated by /daily and /weekly
├── tasks.md               # Task backlog
├── invoices.md            # Invoice tracker ([x] paid, [ ] outstanding)
├── sales.md               # Sales pipeline (hot/active/prospecting)
├── content.md             # Newsletter and content tracking
├── projects/
│   ├── clients/           # One folder per client (overview, weekly reports, meetings)
│   ├── internal/          # Internal projects
│   ├── labs/              # Research and experiments
│   └── product/           # Product development
├── finances/
│   ├── revenue.md         # Revenue log
│   ├── expenses.md        # Expense tracking by category
│   ├── contractors.md     # Contractor rates and hours
│   └── subscriptions.md   # Recurring costs (KEEP/CANCEL/INVESTIGATE)
├── hiring/                # Job postings, applications, interview notes
├── sales/meetings/        # Sales call transcripts
├── team/                  # Contracts and HR docs
├── invoices/              # PDF invoice archive (drop files here)
├── scopes/                # PDF scopes and proposals (drop files here)
└── .claude/commands/      # The slash commands that power everything
```

## Integrations

All integrations are optional. The hub works with just markdown files and git.

| Integration | Plugin | What it enables |
|-------------|--------|----------------|
| Gmail & Calendar | `google-skill` | `/setup` imports emails and events; `/client-update` creates draft emails |
| Google Sheets | `google-skill` | Financial dashboards, project tracking |
| Google Docs | `google-skill` | Read and create documents |
| Meeting notes | `granola-skill` | Auto-import meeting transcripts to client folders |
| Newsletter | `buttondown-skill` | Track subscribers, create drafts, pull stats |
| GitHub | `gh` CLI (built-in) | `/sync` pulls commit activity into weekly reports |
| Browser | `chrome-driver` | Screenshots, web scraping, form filling |
| Image generation | `nano-banana` | Weekly status infographics |
| Document search | `embeddings-search-skill` | Semantic search across all your docs |

## Philosophy

- **Markdown over databases** — Everything is a text file. Diff it, grep it, version it.
- **AI-first** — Designed to be read and maintained by Claude, not a web UI.
- **Convention over configuration** — File naming patterns and folder structure are the schema.
- **Draft-only** — Nothing sends automatically. Claude creates drafts for you to review.
- **Progressive disclosure** — Start with just tasks and invoices. Add integrations as you need them.

## License

MIT
