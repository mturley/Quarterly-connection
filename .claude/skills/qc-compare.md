---
description: "Compare metrics between two quarters side-by-side. Usage: /qc-compare Q3 Q4 or /qc-compare Q4 2024 Q1 2025"
---

# Compare Command

Compare metrics between two quarters.

## Instructions

When the user runs this skill with arguments like `Q3 Q4` or `Q2 Q3 2025`:

### Step 1: Parse Quarters

Extract two quarters to compare from the skill arguments:
- `Q3 Q4` - Compare Q3 and Q4 of current year
- `Q1 Q2 2024` - Compare Q1 and Q2 of 2024
- `Q4 2024 Q1 2025` - Compare across years

### Step 2: Fetch Data for Both Quarters

For each quarter, fetch (can be parallel):

**GitHub PRs** (for each tracked repo):
```bash
gh search prs --author={username} --repo={owner}/{repo} --merged={START}..{END} --json number --limit 100
```

**Jira Epics** — use `mcp__atlassian__searchJiraIssuesUsingJql`
**Jira Tickets** — use `mcp__atlassian__searchJiraIssuesUsingJql`
**Local log entries** — read log files

### Step 3: Display Comparison

```
QUARTER COMPARISON: Q{A} vs Q{B} {YEAR}

Metric                Q{A}      Q{B}      Change
──────────────────────────────────────────────────
PRs Merged            8         13        +62%
Epics Owned           6         10        +67%
Epics Completed       3         7         +133%
Tickets Resolved      18        25        +39%
Log Entries           6         12        +100%

HIGHLIGHTS

Biggest Improvement: Epics Completed (+133%)
Consistent Growth: All metrics improved
Strong Quarter: Q{B} shows significant progress

Tips:
  Your PR output increased - great code velocity!
  Epic completion rate improved substantially
  Consider logging more frequently to capture all wins
```

### Change Indicators

- Increase (positive)
- Decrease (negative)
- No change

### Step 4: Stop

After displaying comparison, STOP and wait for user.

## Behavior

- Fetch data for both quarters (can be parallel)
- Calculate percentage changes
- Display comparison table
- Do NOT automatically suggest next steps
- STOP after displaying
