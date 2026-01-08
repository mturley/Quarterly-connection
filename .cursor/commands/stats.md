# Stats Command

Quick metrics from GitHub and Jira without generating a narrative report.

## Instructions

When the user runs `/stats`:

### Step 1: Load Configuration

Read `config/company-context.json` for GitHub and Jira settings.

### Step 2: Determine Current Quarter

Calculate quarter based on today's date.

### Step 3: Fetch Metrics (ONE PASS)

**GitHub PRs:**
```
mcp_github_search_issues(
  q: "is:pr author:{username} repo:{owner}/{repo} merged:{start_date}..{end_date}",
  perPage: 100
)
```

**Jira Epics:**
```
mcp_mcp-atlassian_jira_search(
  jql: "assignee = \"{jira_email}\" AND issuetype = Epic AND updated >= {start_date}",
  limit: 50
)
```

**Jira Tickets:**
```
mcp_mcp-atlassian_jira_search(
  jql: "assignee = \"{jira_email}\" AND issuetype IN (Story, Task, Bug) AND resolution IS NOT EMPTY AND updated >= {start_date}",
  limit: 100
)
```

**Local Logs:**
Read `data/achievements/{YEAR}/Q{N}_log.md`

### Step 4: Display Stats

```
📊 Q{N} {YEAR} QUICK STATS

💻 GitHub Activity
├─ PRs Merged: {count}
└─ Repositories: {repo_list}

📋 Jira Activity
├─ Epics Owned: {total_epics}
├─ Epics Completed: {completed_epics}
├─ Tickets Resolved: {resolved_tickets}
└─ By Type: {stories} Stories, {tasks} Tasks, {bugs} Bugs

📝 Local Logs
├─ Achievements: {count}
├─ Challenges: {count}
├─ Collaborations: {count}
└─ Total Entries: {total}

💡 Run /report to generate full narrative report
```

## Behavior

- Fetch each data source ONCE
- Do NOT generate any narrative or report
- Display stats and STOP
- Do NOT ask questions or prompt for more input




