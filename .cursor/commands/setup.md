# Setup Command

Initialize and configure the Quarterly Connection Strategist with company context and integrations.

## Instructions

When the user runs this command, guide them through a setup flow:

### Step 1: Check Existing Configuration

1. Read `config/company-context.json`
2. If exists and initialized, show current config and ask if they want to update
3. If not exists, start fresh setup

### Step 2: Gather Information

Ask for each piece of information ONE AT A TIME:

**Company Information:**
```
🏢 What company do you work for?
```
- After they respond, do ONE web search: "{company name} company values mission culture"
- Extract core values and strategic priorities
- Show what was found and ask for confirmation

**User Profile:**
```
👤 What is your name?
📋 What is your role/title?
🏠 What team are you on?
```

**GitHub Integration:**
```
💻 What is your GitHub username? (for filtering PRs)
📦 What repositories should I track? 
   (Format: owner/repo, e.g., "opendatahub-io/odh-dashboard")
   You can list multiple, separated by commas.
```

**Jira Integration:**
```
📧 What is your Jira email address?
🎫 What Jira project keys should I search? 
   (Optional, e.g., "RHOAIENG, RHAIENG")
```

### Step 3: Save Configuration

Save all gathered information to `config/company-context.json` in this structure:

```json
{
  "company": {
    "name": "{company_name}",
    "initialized": true,
    "last_updated": "{today's date}"
  },
  "core_values": [
    {"name": "Value 1", "description": "Description..."}
  ],
  "strategic_priorities": {
    "year": 2025,
    "priorities": ["Priority 1", "Priority 2"]
  },
  "user_profile": {
    "name": "{name}",
    "role": "{role}",
    "team": "{team}",
    "jira_email": "{email}",
    "jira_projects": ["{project1}", "{project2}"]
  },
  "github": {
    "author": "{username}",
    "repositories": [
      {"owner": "{owner}", "repo": "{repo}"}
    ]
  }
}
```

### Step 4: Confirm

```
✅ Setup complete! Your configuration has been saved.

📊 Ready to track:
   • GitHub: {username} @ {repo list}
   • Jira: {email} @ {project list}
   • Company: {company_name}

Try these commands next:
   /log - Add your first achievement
   /status - Check current quarter info
   /report - Generate your quarterly report
```

## Behavior

- Ask questions ONE at a time
- Do ONE web search for company values (not multiple)
- Save configuration ONCE
- After saving, STOP and wait for user
- Do NOT automatically run other commands after setup



