---
description: "Capture and save a work achievement to the quarterly log. Usage: /qc-log <description> or /qc-log [Category]: <description>"
---

# Log Command

Capture and save work achievements to the quarterly log.

## Instructions

When the user runs this command with content (e.g., `/qc-log Shipped new feature`), process it as follows:

### Step 1: Parse the Input

The user may provide:
- Just a description: `/qc-log Shipped new auth service`
- With category: `/qc-log [Challenge]: Fixed production outage`

The description is passed as the skill argument.

### Step 2: Auto-Categorize (if no category provided)

Analyze the description and assign the most appropriate category:

| Category | Keywords/Patterns |
|----------|-------------------|
| **Achievement** | shipped, completed, launched, delivered, finished, released |
| **Challenge** | fixed, resolved, debugged, overcame, unblocked, solved |
| **Skill Development** | learned, completed training, certified, studied, practiced |
| **Collaboration** | mentored, helped, paired, reviewed, collaborated, supported |
| **Project Update** | progress, update, status, milestone, working on |
| **Recognition** | award, shoutout, praised, recognized, thanked |

Default to **Achievement** if unclear.

### Step 3: Determine File Path

Calculate the current quarter:
- Q1: January 1 - March 31
- Q2: April 1 - June 30
- Q3: July 1 - September 30
- Q4: October 1 - December 31

File path: `data/achievements/{YEAR}/Q{N}_log.md`

### Step 4: Format the Entry

```
[YYYY-MM-DD] | {Category} | {Description}
```

Example:
```
[2025-12-16] | Achievement | Shipped new auth service reducing latency by 40%
```

### Step 5: Append to Log File

- If file doesn't exist, create it with a header:
  ```markdown
  # Q{N} {YEAR} Achievement Log

  [entries go here]
  ```
- Append the new entry to the file
- Do NOT read the file back to verify

### Step 6: Confirm and Stop

```
✅ Logged to Q{N} {YEAR}:
[{date}] | {Category} | {description}

Anything else to add?
```

## Behavior

- ONE write operation to append the entry
- Do NOT read the file back to verify
- Do NOT check company context
- After confirming, STOP and wait for user input
- Keep responses brief and efficient

## Examples

**Input:** `/qc-log Shipped new dashboard feature with 99% test coverage`
**Output:**
```
✅ Logged to Q4 2025:
[2025-12-16] | Achievement | Shipped new dashboard feature with 99% test coverage

Anything else to add?
```

**Input:** `/qc-log [Challenge]: Debugged critical memory leak in production`
**Output:**
```
✅ Logged to Q4 2025:
[2025-12-16] | Challenge | Debugged critical memory leak in production

Anything else to add?
```
