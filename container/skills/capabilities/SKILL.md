---
name: capabilities
description: Show what this NanoClaw instance can do — installed skills, available tools, and system info. Read-only. Use when the user asks what the bot can do, what's installed, or runs /capabilities.
---

# /capabilities — System Capabilities Report

Generate a structured read-only report of what this NanoClaw instance can do.

## How to gather the information

Run these commands and compile the results into the report format below.

### 1. Installed skills

List skill directories available to you:

```bash
ls -1 /home/node/.claude/skills/ 2>/dev/null || echo "No skills found"
```

Each directory is an installed skill. The directory name is the skill name (e.g., `agent-browser` → `/agent-browser`).

### 2. Available tools

You always have access to:
- **Core:** Bash, Read, Write, Edit, Glob, Grep
- **Web:** WebSearch, WebFetch
- **Other:** TodoWrite, ToolSearch, Skill
- **MCP:** mcp__nanoclaw__* — list the ones you actually have (e.g. send_message, send_file, add_reaction, edit_message, ask_user_question, install_packages, add_mcp_server, create_agent)
- **CLI:** `ncl` — scheduled tasks (`ncl tasks list/create/update/pause/resume/cancel`), agent config

### 3. Container tools

```bash
which agent-browser 2>/dev/null && echo "agent-browser: available" || echo "agent-browser: not found"
which python3 2>/dev/null && echo "python3: available" || echo "python3: not found"
```

### 4. Agent info

```bash
ls /workspace/agent/CLAUDE.md /workspace/agent/CLAUDE.local.md 2>/dev/null && echo "Agent instructions: yes" || echo "Agent instructions: no"
ls /workspace/extra/ 2>/dev/null && echo "Extra mounts: $(ls /workspace/extra/ 2>/dev/null | wc -l | tr -d ' ')" || echo "Extra mounts: none"
```

## Report format

Present the report as a clean, readable message. Example:

```
📋 *NanoClaw Capabilities*

*Installed Skills:*
• /agent-browser — Browse the web, fill forms, extract data
• /capabilities — This report
(list all found skills)

*Tools:*
• Core: Bash, Read, Write, Edit, Glob, Grep
• Web: WebSearch, WebFetch
• MCP: send_message, send_file, …
• CLI: ncl tasks

*Container Tools:*
• agent-browser: ✓
• python3: ✓

*System:*
• Agent instructions: yes/no
• Extra mounts: N directories
```

Adapt the output based on what you actually find — don't list things that aren't installed.

**See also:** `/status` for a quick health check of session, workspace, and tasks.
