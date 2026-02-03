# Setup Guide

How to set up your operations hub from this template.

---

## Quick Start

1. **Edit CLAUDE.md** - Replace all `[PLACEHOLDERS]` with your company info:
   - `[COMPANY_NAME]` - Your company name
   - `[GITHUB_ORG]` - Your GitHub organization
   - `[STACK]` - Your tech stack (e.g. "TypeScript, pnpm, Vercel/Supabase")

2. **Add your first client** - See "Adding Clients" below

3. **Try `/daily`** - Should read your files and produce a morning briefing

4. **Try `/push`** - Commits and pushes your changes

That's it. Everything else is optional.

---

## Adding Clients

### 1. Create the client directory

```bash
mkdir -p projects/clients/acme-corp/meetings
```

### 2. Copy and fill in the client file

```bash
cp projects/clients/_template.md projects/clients/acme-corp/acme-corp.md
```

Edit the file with your client's details: contact info, status, scope, repos.

### 3. Update CLAUDE.md

Add a row to the **Active Client Projects** table:

```markdown
| Acme Corp | Jane Smith | Phase 1 - Active |
```

### 4. Update invoices.md

Add a section for the client:

```markdown
## Acme Corp

- [ ] Invoice #1, $X,000, Phase 1 - Description, sent YYYY-MM-DD
```

That's all. The `/daily` and `/weekly` commands will now include this client in their reports.

---

## Tracking Files

### tasks.md
Your task backlog. Organized by urgency:
- **Urgent** - Must do this week
- **Active Work** - In progress
- **On Deck** - Coming soon
- **Completed** - Done items (clear weekly)

### invoices.md
Master invoice log. Convention:
- `[x]` = Paid
- `[ ]` = Outstanding/pending

### sales.md
Sales pipeline organized by temperature:
- **Hot** - Active conversations, likely to close
- **Active** - In progress, needs nurturing
- **Prospecting** - Early stage

### content.md
Newsletter/content tracking. Stats, archive, and pipeline.

---

## GitHub Integration

The `/sync` command can pull commit activity from your GitHub repos.

### Setup

1. Install the GitHub CLI: `brew install gh` (or see [cli.github.com](https://cli.github.com))
2. Authenticate: `gh auth login`
3. Edit `.claude/commands/sync.md`:
   - Replace `[YOUR_GITHUB_ORG]` with your GitHub org name
   - Add your repo-to-project mappings in the mapping table

### Repo Mapping Format

In `sync.md`, add your repos to the mapping table:

```markdown
| repo-name | projects/clients/client-name/YYYY-W##.md |
| another-repo | projects/product/product-name/YYYY-W##.md |
```

---

## Optional Add-Ons

### Meeting Notes Integration

If you use a meeting notes tool (Granola, Otter, Fireflies, etc.):

1. Edit `.claude/commands/sync.md` - Uncomment the "Sync Meetings" section
2. Configure the routing table to map meeting participants to client folders
3. Add the CLI command or API call for your meeting notes tool

### Newsletter Integration

If you use Buttondown, ConvertKit, or similar:

1. Edit `.claude/commands/sync.md` - Uncomment the "Sync Newsletter Stats" section
2. Add your API key storage location and API calls
3. Uncomment the Newsletter skill in `CLAUDE.md`

### Email Integration (for /client-update)

The `/client-update` command generates branded HTML emails. To actually create Gmail drafts:

1. Set up Gmail API OAuth (requires a Google Cloud project)
2. Update `.claude/commands/client-update.md` with your email sending tool
3. Configure brand colors in `CLAUDE.md`

### Infographic Generation

The `/weekly` command has an optional infographic generation phase:

1. Set up an image generation tool (e.g. DALL-E, Gemini, Midjourney API)
2. Configure your brand colors in `CLAUDE.md`
3. The weekly command will use them to generate a visual status

---

## File Naming Conventions

| Pattern | Example | Usage |
|---------|---------|-------|
| Client directories | `projects/clients/acme-corp/` | Lowercase, hyphenated |
| Client overview | `projects/clients/acme-corp/acme-corp.md` | Matches directory name |
| Weekly reports | `projects/clients/acme-corp/2026-W05.md` | ISO week number |
| Meeting transcripts | `projects/clients/acme-corp/meetings/meeting-name.YYYY-MM-DD.md` | Date-suffixed |
| Interview transcripts | `hiring/meetings/Name.interview.YYYY-MM-DD.md` | Name + date |
| Financial reports | `finances/reports/YYYY-MM.md` | Year-month |
| Invoice PDFs | `invoices/client-name-invoice-N.pdf` | Client + number |

---

## Customization

### Adding Commands

Create a new `.md` file in `.claude/commands/`:

```markdown
---
description: What this command does
allowed-tools: [Bash]
---

# Command Name

Instructions for Claude...
```

Then use it with `/your-command-name`.

### Modifying the Dashboard

The README.md structure is maintained by `/daily` (text updates) and `/weekly` (full regeneration). To change the dashboard layout:

1. Edit the section headings in README.md
2. Update the corresponding update logic in `.claude/commands/daily.md` (Step 3)
3. Update the regeneration logic in `.claude/commands/weekly.md` (Phase 6)

### Adding Project Categories

The template comes with `clients/`, `internal/`, `labs/`, and `product/`. To add more:

1. Create the directory: `mkdir -p projects/new-category`
2. Add a `.gitkeep` file
3. Update the Key Files table in `CLAUDE.md`
4. Update `/sync` if you want GitHub activity tracked there
