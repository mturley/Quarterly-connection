# 📊 Quarterly Connection Strategist

> An AI-powered personal planning system for quarterly reviews using Cursor and markdown files.

Transform your work data into compelling quarterly narratives. Log achievements naturally, and the AI organizes everything and generates polished reports.

---

## 🚀 Quick Start

### 1. Open in Cursor AI

Open this project folder in **Cursor AI** (not VS Code).

### 2. Run Setup

Type in the chat:

```
/setup
```

The agent will guide you through:

- 🏢 Company name → Auto-fetches values & priorities
- 👤 Your name, role, team
- 💻 GitHub username & repositories to track
- 📧 Jira email & project keys

### 3. Start Logging

Throughout the quarter, capture your wins:

```
/log Shipped new API gateway, reducing response times by 45%
```

### 4. Generate Your Report

At quarter end:

```
/report
```

The AI fetches GitHub PRs, Jira tickets, combines with your logs, asks reflection questions, and generates a beautiful HTML report.

---

## 📝 Commands

All commands work in Cursor chat. Type `/` to see available commands.

### Getting Started

| Command    | What It Does                       |
| ---------- | ---------------------------------- |
| `/help`    | Show all commands with examples    |
| `/setup`   | Configure company & integrations   |
| `/profile` | Update your name, role, team       |
| `/status`  | See current quarter & entry counts |

### Logging Achievements

| Command                   | What It Does                       |
| ------------------------- | ---------------------------------- |
| `/log <text>`             | Add achievement (auto-categorized) |
| `/log [Category]: <text>` | Add with specific category         |
| `/logs`                   | View current quarter's entries     |
| `/logs Q2 2025`           | View specific quarter              |
| `/edit`                   | Edit or delete entries             |

**Categories:** Achievement, Challenge, Skill Development, Collaboration, Project Update, Recognition

### Reporting

| Command           | What It Does                   |
| ----------------- | ------------------------------ |
| `/preview`        | See all data before generating |
| `/stats`          | Quick metrics only             |
| `/report`         | Full report (current quarter)  |
| `/report Q3 2024` | Report for specific quarter    |
| `/compare Q3 Q4`  | Compare two quarters           |
| `/export`         | PDF export instructions        |

### Goal Tracking

| Command      | What It Does       |
| ------------ | ------------------ |
| `/goals`     | View current goals |
| `/goals set` | Set new goals      |

---

## 🗂️ Project Structure

```
Quarterly-connection/
├── .cursor/
│   └── commands/              # Cursor AI slash commands
│       ├── help.md
│       ├── setup.md
│       ├── log.md
│       ├── report.md
│       └── ...
├── .cursorrules               # Agent behavior & anti-loop safeguards
├── config/
│   └── company-context.json   # Company values, user profile, integrations
├── data/
│   ├── achievements/
│   │   └── 2025/
│   │       └── Q4_log.md      # Your achievement logs
│   └── templates/
│       ├── quarterly-report-template.md
│       └── quarterly-report-template.html
└── Q4-2025-report.html        # Generated HTML report
```

---

## 🔧 How It Works

### The Magic

1. **You Just Talk** - No forms, just describe your work naturally
2. **AI Organizes** - Auto-categorizes and stores your entries
3. **Data Integration** - Pulls from GitHub & Jira via MCP tools
4. **Narrative Generation** - Creates compelling, evidence-backed reports

### Report Generation Flow

```
/report
    ↓
┌─────────────────────────────────────┐
│ 1. Fetch GitHub PRs (merged)        │
│ 2. Fetch Jira Epics & Tickets       │
│ 3. Load local achievement logs      │
└─────────────────────────────────────┘
    ↓
┌─────────────────────────────────────┐
│ 4. Present summary                  │
│ 5. Ask 3 reflection questions       │
│    - Which values did you exemplify?│
│    - Biggest impact?                │
│    - Skills to develop?             │
└─────────────────────────────────────┘
    ↓
┌─────────────────────────────────────┐
│ 6. Generate Markdown report         │
│ 7. Generate HTML report             │
└─────────────────────────────────────┘
```

---

## 📋 Report Output

The generated report includes:

1. **Key Achievements & Impact** - What you did → Why it mattered → Result
2. **Alignment with Company Strategy** - Connection to values and priorities
3. **Growth & Development** - Lessons learned, next quarter goals
4. **Data-Driven Evidence** - GitHub PRs and Jira tickets as proof

### Output Files

- **Markdown** - Displayed in chat
- **HTML** - `Q4-2025-report.html` - Beautiful, printable report

---

## 💡 Tips for Best Results

### Log Frequently

Don't wait until end of quarter. Log achievements as they happen:

```
/log Shipped feature X with 40% performance improvement
```

### Be Specific with Impact

❌ `Fixed bug`

✅ `Fixed critical auth bug affecting 10K users, reducing support tickets by 60%`

### Include Metrics

- Percentage improvements
- Time saved
- Users affected
- Cost reductions

### Use Categories

```
/log [Challenge]: Debugged race condition in payment system
/log [Collaboration]: Mentored 2 junior engineers on testing
/log [Skill Development]: Completed AWS certification
```

---

## 📅 Recommended Workflow

### Start of Quarter

```
/goals set          # Define what you want to accomplish
```

### Weekly (5 minutes)

```
/log <your wins>    # Capture achievements as they happen
/status             # Quick check on entry count
```

### Mid-Quarter

```
/stats              # Check GitHub/Jira metrics
/goals              # Review goal progress
```

### End of Quarter

```
/preview            # Review all data
/report             # Generate full report
/export             # Save as PDF
```

---

## 🔌 MCP Tool Integration

This tool uses Cursor's MCP (Model Context Protocol) for data fetching:

### GitHub

- Searches merged PRs by author and date range
- Filters by repository

### Jira

- Searches Epics, Stories, Tasks, Bugs
- Filters by assignee and date range

**Note:** MCP tools must be configured in Cursor for full functionality. Without them, you can still use local logging and manual report generation.

---

## 🛠️ Customization

### Adding Custom Commands

Create a new file in `.cursor/commands/your-command.md` with instructions for the AI.

### Modifying Report Template

Edit `data/templates/quarterly-report-template.md` or `quarterly-report-template.html`.

### Updating Company Context

Run `/setup` again or edit `config/company-context.json` directly.

---

## 🤝 Philosophy

- **Consistency > Perfection** - Quick daily updates beat perfect weekly ones
- **AI Augments, Not Replaces** - You describe, AI organizes
- **Evidence-Based** - Every claim backed by data
- **Private & Yours** - All data in local markdown files

---

## 📜 License

MIT - Use freely for personal career development.

---

_Built with ❤️ using Cursor AI + MCP Tools_

_Inspired by [personal-planner](https://github.com/Gkrumbach07/personal-planner)_
