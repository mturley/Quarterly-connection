# Report Command

Generate a comprehensive quarterly connection report with data from GitHub, Jira, and local logs.

## Instructions

When the user runs `/report` or `/report Q{N} {YEAR}`, generate a full quarterly report.

### Step 0: Determine Quarter

- If no quarter specified, use current quarter based on today's date
- If specified (e.g., `/report Q3 2025`), use that quarter

**Quarter Date Ranges:**
| Quarter | Start | End |
|---------|-------|-----|
| Q1 | January 1 | March 31 |
| Q2 | April 1 | June 30 |
| Q3 | July 1 | September 30 |
| Q4 | October 1 | December 31 |

### Step 1: Load Configuration

Read `config/company-context.json` to get:
- GitHub username and repositories
- Jira email and project keys
- Company values and priorities
- User profile (name, role, team)

### Step 2: Fetch Data (ONE PASS - Do Not Repeat)

Execute these data fetches in parallel:

**Local Logs:**
- Read `data/achievements/{YEAR}/Q{N}_log.md`

**GitHub PRs (using search_issues for better filtering):**
```
mcp_github_search_issues(
  q: "is:pr author:{username} repo:{owner}/{repo} merged:{start_date}..{end_date}",
  sort: "updated",
  order: "desc",
  perPage: 50
)
```

**Jira Epics:**
```
mcp_mcp-atlassian_jira_search(
  jql: "assignee = \"{jira_email}\" AND issuetype = Epic AND updated >= {start_date} ORDER BY updated DESC",
  limit: 20,
  fields: "summary,status,issuetype,priority,updated,created,resolution"
)
```

**Jira Tickets (Stories/Tasks/Bugs):**
```
mcp_mcp-atlassian_jira_search(
  jql: "assignee = \"{jira_email}\" AND issuetype IN (Story, Task, Bug) AND resolution IS NOT EMPTY AND updated >= {start_date} ORDER BY updated DESC",
  limit: 50,
  fields: "summary,status,issuetype,priority,updated,resolution"
)
```

### Step 3: Present Summary & Ask Reflection Questions

Show what was found:
```
📊 Q{N} {YEAR} Data Summary:
   • Local Logs: {count} entries
   • GitHub PRs: {count} merged
   • Jira Epics: {count} found ({completed} completed)
   • Jira Tickets: {count} resolved
```

Then ask these reflection questions (STOP and wait for answers):

```
Before I generate your report, please answer:

Q1 - Strategic Alignment:
Which 2-3 company values did your contributions most exemplify this quarter?

Q2 - Impact:
What was your single biggest impact or achievement?

Q3 - Growth:
What skill do you want to develop next quarter?
```

### Step 4: Generate Markdown Report (After User Answers)

Use the template structure:

```markdown
# Quarterly Connection Summary: {Name} - Q{N} {YEAR}

**Role:** {role} | **Team:** {team}
**Period:** {start_date} - {end_date}

---

## I. Key Achievements & Impact

{3-5 bullet points using WHAT → WHY → RESULT format}
{Incorporate user's answer to Q2}

## II. Alignment with Company Strategy

### Values Demonstrated
{Connect to company values based on user's Q1 answer}

### Strategic Contribution
{How work supported company priorities}

## III. Growth, Learning & Development

### This Quarter
{Lessons learned, skills developed}

### Next Quarter Goals
{User's Q3 answer about skill development}

## IV. Data-Driven Evidence

### GitHub Contributions
| PR | Repository | Description |
|----|------------|-------------|
{Top 10 merged PRs}

### Jira Epics Owned
{List of epics with status}

### Jira Tickets Completed
{Top 10-15 resolved tickets}

---

*Generated on {today's date}*
```

### Step 5: Generate HTML Report

After markdown, automatically create `Q{N}-{YEAR}-report.html` in the project root.

**HTML Structure:**
- Professional design with company branding colors
- Stats dashboard (PRs merged, Epics owned, Tickets resolved, Epics completed)
- Sections: Key Achievements, Values Alignment, GitHub Contributions, Jira Work, Growth
- Responsive layout
- Print-friendly styles

### Step 6: Confirm Completion

```
✅ Report generated in Markdown and HTML formats.
📄 HTML Report: Q{N}-{YEAR}-report.html

Open the HTML file in a browser to view or print to PDF.
```

## Behavior

- Fetch each data source ONCE only
- Do NOT re-fetch to verify
- STOP after showing summary and asking questions
- Wait for user answers before generating report
- Generate HTML automatically after markdown
- After completion, STOP and wait for user




