# Daily Review

Morning briefing and dashboard update. Surface priorities, remove friction, keep README.md current.

## Step 1: Gather Data

Read current state:
- `README.md` - Live dashboard
- `tasks.md` - Task backlog
- `invoices.md` - Outstanding payments
- `projects/clients/*.md` - Client statuses
- Recent weekly reports: `projects/clients/*/YYYY-W*.md`

Check git for recent activity:
```bash
git log --oneline --since="yesterday" --all
```

<!-- If meeting notes tool configured, check recent meetings here:
```bash
# your-meeting-tool list --days 2
```
-->

Look at any meeting transcripts from yesterday/today:
```bash
find projects/clients/*/meetings hiring/meetings sales/meetings -name "*.md" -mtime -1 2>/dev/null
```

## Step 2: Analysis

### Pattern Recognition
- What got done yesterday? (git commits, file changes)
- What meetings happened? (check meeting transcripts)
- What's scheduled for today? (meetings, deadlines from client files)
- What's been avoided or slipping?
- Any client health issues flagged?

### Opportunities
- Outstanding invoices that need follow-up
- Sales pipeline items ready to advance
- Client meetings coming up that need prep

### Friction Removal
For each priority:
- What's the exact next action?
- Who needs to be contacted?
- What's blocking progress?

## Step 3: Update README.md

After analysis, update `README.md` with current information. Do NOT regenerate the infographic daily - just update the text sections:

1. Update "Last updated:" date
2. Refresh invoice status (paid/outstanding amounts)
3. Update "Urgent This Week" table
4. Refresh "Recent Activity" section with latest from weekly reports
5. Update client health if anything changed
6. Refresh any stale project statuses

Keep the existing infographic - it gets regenerated weekly via `/weekly`.

## Step 4: Output Briefing

```
BRIEF - [Date]

STATE OF AFFAIRS:
[1-2 sentences on current momentum]

TODAY'S PRIORITIES:
1. [Most important thing] - [why now]
2. [Second priority] - [context]
3. [Third priority] - [context]

MONEY:
- Outstanding: $X awaiting payment
- Ready to invoice: [if any]

SCHEDULED:
- [Any meetings/calls today]

BLOCKERS:
[Anything stuck and why]

ONE THING:
If you do nothing else: [single highest-leverage action]
```

Keep it brief - this is a morning briefing, not a report.
