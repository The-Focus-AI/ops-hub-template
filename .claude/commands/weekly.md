# Weekly Review

End-of-week review and planning. This is a conversation, not a report.

## Phase 1: Gather Data

Read current state:
- `README.md` - Dashboard overview
- `invoices.md` - What's paid, what's outstanding
- `tasks.md` - What was planned vs completed
- `sales.md` - Pipeline status
- `projects/clients/*.md` - All client statuses
- `hiring/applications/README.md` - Hiring progress (if active)

Check git activity for the week:
```bash
git log --oneline --since="7 days ago" --all | head -50
```

Find this week's reports:
```bash
ls projects/clients/*/YYYY-W*.md projects/labs/*/YYYY-W*.md projects/product/*/YYYY-W*.md 2>/dev/null | sort -r | head -20
```

<!-- If meeting notes tool configured, check the week's meetings:
```bash
# your-meeting-tool list --days 7
```
-->

Review meeting transcripts for action items and relationship signals:
```bash
find projects/clients/*/meetings -name "*.md" -mtime -7 2>/dev/null
find hiring/meetings -name "*.md" -mtime -7 2>/dev/null
find sales/meetings -name "*.md" -mtime -7 2>/dev/null
```

## Phase 2: Review Together

### What Happened
- Commits and work completed
- Client interactions and outcomes (review meeting transcripts!)
- Hiring interviews conducted
- Sales calls and pipeline progress
- Revenue collected vs invoiced
- Any fires or surprises?

### Client Health Check
Go through each active client:
- How's the relationship? (check recent meeting transcripts for tone/signals)
- Any concerns brewing?
- Next actions clear?
- Commitments made in meetings that need follow-up?

### What Didn't Happen
- Planned items that slipped
- Outreach that didn't go out
- Recurring avoidance patterns

## Phase 3: Plan Next Week

### Priorities
- What MUST happen (hard deadlines, client commitments)
- What unlocks other work
- What's been put off too long

### Energy Check
- What's draining energy?
- What's generating momentum?
- Anything to cut or delegate?

## Phase 4: Update Files

After the review, update:
1. `tasks.md` - Clear completed, add new items
2. Client files - Update any changed statuses or next actions
3. `CLAUDE.md` - If project status changed significantly

## Phase 5: Generate Infographic (Optional)

If image generation is configured (see CLAUDE.md), generate a visual status infographic using your brand colors. The infographic should include:

- Revenue summary (collected, outstanding, pipeline)
- Client project summaries with commit counts
- Labs/product project summaries
- Team overview
- Newsletter stats (if applicable)
- Date range for the week

Save to `assets/weekly-status.png`.

## Phase 6: Update README.md

Regenerate `README.md` with:
1. Infographic at top (if generated)
2. Invoice summary (Paid This Month, Outstanding, Pipeline)
3. Urgent This Week table
4. Recent Activity from weekly reports
5. Client Health Overview
6. Active Client Projects
7. Sales Pipeline
8. Hiring (if active)
9. Marketing & Content
10. Team
11. Revenue Summary
12. Key Files reference

Set "Last updated:" to today's date.

## Output

End with a clear list:
```
NEXT WEEK PRIORITIES:
1. [Priority] - [Client/Project] - [Deadline if any]
2. ...
3. ...

WAITING ON:
- [What] from [Who]

CALENDAR:
- [Day]: [Scheduled items]
```
