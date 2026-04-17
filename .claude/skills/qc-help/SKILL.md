---
description: Display all available Quarterly Connection commands and how to use them
---

# Help Command

Display all available commands and how to use the Quarterly Connection Strategist.

## Instructions

When the user runs this command, display a comprehensive help guide:

```
QUARTERLY CONNECTION COMMANDS

GETTING STARTED
  /qc-setup             - Configure company values & integrations
  /qc-profile           - Update your name, role, team
  /qc-status            - See current quarter & entry counts

LOGGING
  /qc-log <description> - Add an achievement (auto-categorized)
  /qc-log [Category]: <description>  - Add with specific category
  /qc-logs              - View current quarter's entries
  /qc-logs Q2 2025      - View specific quarter's entries
  /qc-edit              - Edit or delete existing entries

REPORTING
  /qc-preview           - See all data before generating report
  /qc-stats             - Quick metrics (no narrative)
  /qc-report            - Generate full quarterly report
  /qc-report Q3 2025    - Generate report for specific quarter
  /qc-compare Q3 Q4     - Compare two quarters side-by-side

GOALS
  /qc-goals             - View current career goals
  /qc-goals set         - Set new goals for the quarter

EXPORT
  /qc-export            - Get instructions for PDF export

EXAMPLES
  /qc-log Shipped new auth service reducing latency by 40%
  /qc-log [Challenge]: Fixed production outage in 15 minutes
  /qc-report Q3 2024
  /qc-compare Q2 Q3 2025

LOG CATEGORIES
  Achievement - Completed milestones, shipped features
  Challenge - Blockers overcome, problems solved
  Skill Development - New skills learned, training
  Collaboration - Cross-team work, mentorship
  Project Update - Status updates, progress
  Recognition - Awards, positive feedback

Need more details? Just ask about any command!
```

## Behavior

- Display the help text exactly as shown above
- After displaying, STOP and wait for user input
- Do NOT automatically run any other commands
