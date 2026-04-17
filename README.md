# Quarterly Connection Strategist

An AI-powered quarterly review system that works with Claude Code. Log your work naturally throughout the quarter, then generate polished, data-backed reports by pulling directly from GitHub and Jira.

---

## Prerequisites

Before using this repo, you need:

1. **[Claude Code](https://claude.ai/code)** — this is a Claude Code project (CLI, desktop app, or VS Code extension)
2. **GitHub CLI (`gh`)** — for fetching merged PRs ([install guide](https://cli.github.com/))
3. **MCP: Atlassian** — for fetching Jira tickets (configured in Claude Code settings)

> Without GitHub CLI or Jira MCP tools, logging and manual reporting still work — you just won't get auto-fetched data.

---

## Quick Start

### Step 1 — Open in Claude Code

Clone or download this repo and open the folder in Claude Code (or `cd` into it in the CLI).

### Step 2 — Configure

In the Claude Code chat, type:

```
/qc-setup
```

The agent walks you through:
- Company name (auto-fetches values from the web)
- Your name, role, and team
- GitHub username and repositories to track
- Jira email and project keys

All saved to `config/company-context.json`.

### Step 3 — Set Goals

```
/qc-goals set
```

Define what you want to accomplish this quarter. Stored alongside your config.

### Step 4 — Log Throughout the Quarter

Capture wins as they happen — don't wait until report time:

```
/qc-log Shipped new API gateway, reducing response times by 45%
/qc-log [Challenge]: Debugged race condition in payment system affecting prod
/qc-log [Collaboration]: Mentored two engineers on testing patterns
```

The AI auto-categorizes entries and saves them to `data/achievements/{YEAR}/Q{N}_log.md`.

### Step 5 — Generate Your Report

At quarter end:

```
/qc-report
```

The agent fetches your GitHub PRs and Jira tickets, combines them with your logs, then writes a polished Markdown + HTML report.

---

## All Commands

Commands use the `/qc-` prefix as Claude Code skills.

### Setup & Profile

| Command | What it does |
|---------|-------------|
| `/qc-setup` | Configure company, GitHub, Jira, and your profile |
| `/qc-profile` | Update your name, role, or team |
| `/qc-status` | Show current quarter dates and log entry counts |
| `/qc-goals` | View career goals for this quarter |
| `/qc-goals set` | Set new short-term and long-term goals |
| `/qc-help` | Show this command list inside the chat |

### Logging

| Command | What it does |
|---------|-------------|
| `/qc-log <text>` | Add an achievement (auto-categorized) |
| `/qc-log [Category]: <text>` | Add with a specific category |
| `/qc-logs` | View this quarter's entries |
| `/qc-logs Q2 2025` | View a specific quarter's entries |
| `/qc-edit` | Edit or delete existing entries |

**Log categories:** Achievement · Challenge · Skill Development · Collaboration · Project Update · Recognition

### Reporting

| Command | What it does |
|---------|-------------|
| `/qc-preview` | Fetch all data and show it — without generating the report |
| `/qc-stats` | Quick metrics only (no narrative) |
| `/qc-report` | Full report for the current quarter |
| `/qc-report Q3 2025` | Full report for a specific quarter |
| `/qc-compare Q3 Q4` | Side-by-side metric comparison |
| `/qc-export` | Instructions for saving the HTML report as PDF |

---

## Report Flow

```
/qc-report
   │
   ├─ Step 1: Load config (company, GitHub, Jira credentials)
   │
   ├─ Step 2: Fetch data in parallel
   │           ├─ GitHub: merged PRs via gh CLI
   │           ├─ Jira: epics and resolved tickets via Atlassian MCP
   │           └─ Local: achievement log entries
   │
   ├─ Step 3: Show data summary
   │
   ├─ Step 4: Generate Markdown report
   │
   └─ Step 5: Generate HTML report → {QUARTER}-{YEAR}-report.html
```

The HTML report is print-optimized. Open it in Chrome and use Cmd+P → Save as PDF.

---

## Project Structure

```
Quarterly-connection/
├── CLAUDE.md                             # Agent persona + command routing
├── .claude/
│   └── skills/                           # One file per command — single source of truth
│       ├── qc-report.md
│       ├── qc-log.md
│       ├── qc-setup.md
│       ├── qc-stats.md
│       ├── qc-preview.md
│       └── ... (13 commands total)
├── config/
│   └── company-context.json              # Your profile, company values, GitHub/Jira creds
├── data/
│   ├── achievements/
│   │   ├── 2025/                         # Q4_log.md etc.
│   │   └── 2026/                         # Q1_log.md etc.
│   └── templates/
│       ├── quarterly-report-template.md
│       └── quarterly-report-template.html
├── Q1-2026-report.html                   # Generated — open in browser
└── .gitignore
```

---

## How the Agent Works

This project is structured as a **Claude Code agent** with skills:

```
CLAUDE.md
   Persona, rules, and a routing table.
   No command logic lives here.
      │
      ▼
.claude/skills/qc-*.md
   One file per command. Each file owns its full behavior:
   steps, error handling, and an explicit STOP signal.
      │
      ▼
External Tools (gh CLI + Atlassian MCP)
   Called once per session when a command requires it.
   Results are never re-fetched to "verify."
```

### Why this structure

- **`CLAUDE.md` is short on purpose.** The longer the system prompt, the less reliably the AI follows instructions at the end. It stays fully in context.
- **Commands are self-contained.** Updating `/qc-report` means editing one file, not hunting through a large rules file.
- **Error handling is explicit.** Every command specifies what to do when GitHub returns 0 results, Jira is unreachable, or a log file doesn't exist yet — never silently fails, never aborts.

---

## Tips for Better Reports

**Log often, not at the end of the quarter.**
Five minutes after you ship something is the best time to log it. At report time, the details will have faded.

**Be specific about impact.**

| Instead of | Write |
|-----------|-------|
| `Fixed a bug` | `Fixed auth bug affecting 10K users, reduced support tickets by 60%` |
| `Reviewed PRs` | `Reviewed 8 PRs for new feature, caught 2 breaking API changes before merge` |
| `Attended meeting` | `Led architecture review for BFF layer, unblocked 3 downstream teams` |

**Use the right category.** The auto-categorizer is good, but explicit categories make filtering cleaner:
```
/qc-log [Skill Development]: Completed Golang fundamentals course
/qc-log [Recognition]: Team shoutout for leading production incident response
```

---

## Recommended Workflow

**Start of quarter (30 min)**
```
/qc-goals set       ← What do you want to accomplish?
```

**Weekly (5 min)**
```
/qc-log <your wins this week>
/qc-status          ← See how many entries you have
```

**Mid-quarter (15 min)**
```
/qc-stats           ← Check GitHub/Jira numbers
/qc-goals           ← Review progress against goals
```

**End of quarter (30 min)**
```
/qc-preview         ← See all data before writing
/qc-report          ← Generate the full report
/qc-export          ← Save as PDF for your manager
```

---

## Customization

**Add a new command:** Create `.claude/skills/qc-your-command.md` with a `description` frontmatter field, steps, error handling, and a STOP signal at the end. Add a row to the routing table in `CLAUDE.md`.

**Change the report design:** Edit `data/templates/quarterly-report-template.html`. The CSS variables at the top control all colors and fonts.

**Track multiple repos:** Update `config/company-context.json` → `github.repositories` with additional `{ "owner": "...", "repo": "..." }` entries.

**Use with a different company:** Run `/qc-setup` again — it overwrites the config and fetches new company values.

---

## Philosophy

- **Evidence over assertion** — every claim in the report is backed by a PR, ticket, or log entry
- **Consistent beats perfect** — a quick `/qc-log` today is worth more than a thorough one next month
- **Local and private** — all data lives in markdown files on your machine
- **AI augments, you narrate** — the agent gathers and structures; you provide the reflection

---

*Built with Claude Code + MCP Tools · MIT License*
