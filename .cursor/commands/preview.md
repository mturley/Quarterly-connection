# Preview Command

Fetch and display all data that would go into a report, without generating the report.

## Instructions

When the user runs `/preview`:

### Step 1: Load Configuration

Read `config/company-context.json` for settings.

### Step 2: Determine Current Quarter

Calculate quarter based on today's date.

### Step 3: Fetch All Data (ONE PASS)

Fetch GitHub PRs, Jira Epics, Jira Tickets, and Local Logs.

### Step 4: Display Detailed Preview

```
🔍 REPORT PREVIEW - Q{N} {YEAR}

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
📝 LOCAL LOGS ({count} entries)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

[2025-12-15] | Achievement | Entry 1...
[2025-12-14] | Challenge | Entry 2...
[2025-12-12] | Collaboration | Entry 3...
{show all entries or first 10 with "...and X more"}

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
💻 GITHUB PRS ({count} merged)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

• #{number}: {title}
• #{number}: {title}
• #{number}: {title}
{show all PRs}

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
📋 JIRA EPICS ({count} found)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

• {KEY}-123: {Summary} [{Status}]
• {KEY}-456: {Summary} [{Status}]
{show all epics}

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
📋 JIRA TICKETS ({count} resolved)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

• {KEY}-789: {Summary} [{Type}]
• {KEY}-012: {Summary} [{Type}]
{show first 15 with "...and X more" if needed}

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

✅ Ready to generate report. Say "/report" to continue.
```

## Behavior

- Fetch all data ONCE
- Display detailed preview
- Do NOT automatically generate report
- STOP and wait for user to say /report




