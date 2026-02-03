# Client Update Email

Create a DRAFT branded weekly status email for a client.

**CRITICAL:**
- **DRAFT ONLY** - Never send directly. Always create as draft for user review.
- Generate fresh email content from the weekly report. Never reuse previous emails.

## Arguments

- `$ARGUMENTS` - Client name or "all" for all active clients (e.g., "acme-corp", "all")

## Process

### 1. Determine which clients to process

If `$ARGUMENTS` is "all", read the Active Client Projects table from `CLAUDE.md` and process all listed clients.

Otherwise, match the single client name provided.

### 2. For each client, gather information

#### a. Locate client files

```bash
ls -d projects/clients/*/ | grep -i "{client}"
```

#### b. Find latest weekly report

```bash
ls -t ${CLIENT_DIR}*-W*.md | head -1
```

If no weekly report exists, skip this client and note to run `/sync` first.

#### c. Get client contact info

Read the client's main project file (`projects/clients/{client}/{client}.md`) and extract:
- Contact name
- Contact email

#### d. Check for outstanding invoices

Read `invoices.md` and find any **unpaid invoices** for this client (lines with `[ ]`).

### 3. Generate markdown status email

Create a markdown file at `.claude/tmp/{client}-status.md` with this structure:

```markdown
# {Client Name} Weekly Status

**Week of {Date Range from weekly report title}**

---

{If outstanding invoice exists:}
> **Outstanding Invoice:** ${Amount} - {Description} - Sent {Date}

---

{2-3 sentence executive summary synthesized from the weekly report Status section}

## What We Accomplished

{Extract from Activity Summary section, reformatted as bullet points:}
- **{Area}:** {Description}

## Key Meetings & Decisions

{If meetings section exists in weekly report:}
### {Meeting Title} ({Date})
- {Key point 1}
- {Key point 2}

{If no meetings, omit this section}

## In Progress

{Extract from In Progress or Status section:}
- **{Item}:** {Current status}

## Next Week Priorities

{Extract from Next Steps section:}
1. {Priority 1}
2. {Priority 2}

{If blockers exist:}
## Blockers

- {Blocker description}

---

*[COMPANY_NAME] - Generated {Today's date}*
```

### 4. Generate HTML email

Convert the markdown to branded HTML. Save to `.claude/tmp/{client}-status-email.html`.

<!-- Configure your brand colors in CLAUDE.md. Defaults below: -->
Use these brand colors (customize in CLAUDE.md):
- Background: #faf9f6 (or your [BG_COLOR])
- Text/headings: #333333 (or your [PRIMARY_COLOR])
- Accent: #0066cc (or your [ACCENT_COLOR])
- Font: system fonts fallback
- Max-width container: 600px
- Clean, professional styling

Key elements:
- Outstanding invoice: white background, accent left border (subtle, not alarming)
- Summary: white background, primary left border
- Section headers: primary color with bottom border
- Next Week Priorities: inverted (primary background, white text)
- Footer: primary top border, small text

Also generate a plain text version at `.claude/tmp/{client}-status-email.txt` for the body parameter.

### 5. Create email draft

<!-- Requires email integration. See SETUP.md for Gmail setup instructions.
Once configured, uncomment and update the command below:

```bash
your-email-tool draft \
  --to="{contact_email}" \
  --subject="{Client Name} Weekly Status - Week of {dates}" \
  --body="$(cat .claude/tmp/{client}-status-email.txt)" \
  --html="$(cat .claude/tmp/{client}-status-email.html)"
```
-->

For now, the markdown and HTML files are saved to `.claude/tmp/`. Review and send manually.

### 6. Report results

After processing, output a summary:

```
## Client Status Drafts Created

| Client | Recipient | Subject | Status |
|--------|-----------|---------|--------|
| Client Name | email@... | Weekly Status - Week of dates | Draft created |

Files saved to .claude/tmp/. Review and send when ready.
```

## Example Usage

```
/client-update acme-corp          # Single client draft
/client-update all                # All active clients
```
