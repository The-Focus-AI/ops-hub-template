# Sync

Pull data from external sources into the operations repo. This command coordinates sync tasks using parallel subagents.

## What It Does

1. **GitHub Activity** - Fetch commits and generate weekly reports for active projects
2. *(Optional)* **Meetings** - Export recent meeting transcripts to project folders
3. *(Optional)* **Newsletter Stats** - Pull subscriber count and recent email stats

## Execution

Launch subagents in parallel. Only the GitHub sync is active by default - uncomment others as needed.

### Subagent 1: Sync GitHub Activity

Use the `general-purpose` subagent with this prompt:

```
Sync GitHub activity and generate weekly reports for active repos.

1. Fetch all repos:
   gh repo list [YOUR_GITHUB_ORG] --limit 100 --json name,updatedAt,pushedAt,description,isArchived

2. For each repo pushed in the last 14 days (and not archived):
   - Fetch commits from last 7 days:
     gh api repos/[YOUR_GITHUB_ORG]/{repo}/commits --jq '.[].commit.message' -X GET -f since={7-days-ago-ISO}

   - If there are commits, create/update weekly report using these mappings:

     | Repo | Destination |
     |------|-------------|
     <!-- Add your repo-to-project mappings here. Examples:
     | my-client-app | projects/clients/client-name/YYYY-W##.md |
     | my-product | projects/product/product-name/YYYY-W##.md |
     | my-experiment | projects/labs/experiment/YYYY-W##.md |
     -->

3. Weekly report format:
   # {Project Name} - Week ## (Date Range)

   ## Summary
   {Brief overview of the week's changes}

   ## Key Changes
   {Grouped by feature/area with bullet points}

   ## Commits
   {Count and notable commits}

   ---
   Generated: {date}

4. Return summary: list of reports generated/updated and any new repos needing categorization.
```

<!-- ====================================================================
OPTIONAL: Sync Meetings
Uncomment this section if you use a meeting notes tool (Granola, Otter, etc.)
======================================================================== -->

<!--
### Subagent 2: Sync Meetings

Use the `general-purpose` subagent with this prompt:

```
Sync meetings from the last 7 days.

1. List meetings:
   # YOUR_MEETING_TOOL_COMMAND list --days 7

2. Check existing meetings in these directories to avoid duplicates:
   - projects/clients/*/meetings/
   - hiring/meetings/
   - sales/meetings/

3. For each NEW meeting not already exported, categorize by these patterns:

   | Pattern | Destination |
   |---------|-------------|
   | "Client Name", Contact Name | projects/clients/client-name/meetings/ |
   | Interview/hiring context | hiring/meetings/ |
   | Sales calls, prospects | sales/meetings/ |

4. Export each meeting:
   # YOUR_MEETING_TOOL_COMMAND export {meeting-id} --output {target-directory}

5. Return summary: count of meetings exported and their destinations.
```
-->

<!-- ====================================================================
OPTIONAL: Sync Newsletter Stats
Uncomment this section if you use a newsletter platform
======================================================================== -->

<!--
### Subagent 3: Sync Newsletter Stats

Use the `general-purpose` subagent with this prompt:

```
Sync newsletter stats.

1. Get subscriber count:
   # YOUR_NEWSLETTER_API_CALL to get subscriber count

2. Get recent emails:
   # YOUR_NEWSLETTER_API_CALL to get recent sent emails with stats

3. Return summary with:
   - Total subscriber count
   - List of recent emails (subject, date, open rate)
```
-->

## Running the Sync

Execute active subagents in parallel:

```
Use the Task tool to launch subagents simultaneously:
1. subagent_type: "general-purpose", description: "Sync GitHub activity"
<!-- 2. subagent_type: "general-purpose", description: "Sync meetings" -->
<!-- 3. subagent_type: "general-purpose", description: "Sync newsletter stats" -->
```

## Output

After all subagents complete, summarize:
- **Weekly Reports**: List of reports generated/updated
- **Meetings**: Count exported, destinations (if enabled)
- **Newsletter**: Subscriber count, recent emails (if enabled)
- **Issues**: Any new repos needing categorization, errors encountered
