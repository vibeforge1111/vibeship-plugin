---
title: Start Session
description: Start a Vibeship session - loads your project memory and skills
---

# Vibeship Session Start

You are starting a Vibeship-powered development session. Follow these steps:

## Step 1: Load Memory Context

First, call `mind_recall()` to load the user's project context from previous sessions.

If this returns context, acknowledge what was loaded:
- Project goal
- Last session summary
- Any pending reminders
- Current blockers

## Step 2: Detect Project Context

Call `spawner_orchestrate` with:
- `cwd`: The current working directory
- `files`: List of files in the project (from `ls` or file listing)
- `mind_memory`: Content from `.mind/MEMORY.md` if it exists
- `mind_session`: Content from `.mind/SESSION.md` if it exists

## Step 3: Greet Based on Path

Based on the orchestration result:

### If path = "resume"
Greet warmly with project context:
"Welcome back to **[project name]**! Last time we [summary]. Ready to continue?"

### If path = "analyze"
Acknowledge the new codebase:
"I've analyzed your codebase. Detected [stack]. I've loaded skills for [technologies]. What would you like to build?"

### If path = "brainstorm"
Help them start fresh:
"No existing project detected. Tell me what you want to build and I'll help you plan it out!"

## Step 4: Set the Tone

Remind the user they can:
- Ask `/vibeship-save` to capture decisions
- Ask `/vibeship-status` to check what's remembered
- Just start building - you'll handle the rest

Keep it conversational and helpful. This is the start of a productive session!

## Handling Connection Issues

Always provide **actionable guidance**, not just error messages.

### If Mind MCP fails:

```
## Memory Unavailable

**What's happening:** I can't connect to your local memory service.

**What this means for you:**
- I won't remember decisions from previous sessions
- This session still works, just without history
- Nothing is lost - your `.mind/` folder is still there

**How to fix it (pick one):**
1. **Quick fix:** Restart Claude Code (often resolves connection issues)
2. **Check installation:** Run `mind --version` in terminal
3. **Reinstall:** `npm install -g @anthropic/mind`

**Want to continue anyway?** I can still help you code - just tell me what you're working on!
```

Proceed without memory - the session can still work, just without persistence.

### If Spawner MCP fails:

```
## Skills Unavailable

**What's happening:** I can't reach the Vibeship skills server.

**What this means for you:**
- I won't have specialist knowledge for your stack
- Core Claude capabilities work perfectly
- No data is lost

**How to fix it (pick one):**
1. **Check internet:** Can you reach other websites?
2. **Test connection:** `curl https://mcp.vibeship.co/health`
3. **Restart:** Close and reopen Claude Code

**Want to continue anyway?** I'm still a capable coding assistant - let's build!
```

Proceed without skills - core Claude capabilities still work.

### If both fail:

```
## Vibeship Services Unavailable

**What's happening:** Neither memory nor skills services are connecting.

**What this means:**
- You can still code normally with Claude
- Memory won't persist this session
- Specialist skills won't load

**Quick troubleshooting:**
1. Check internet connection
2. Run `claude mcp list` to see MCP status
3. Restart Claude Code

**The most common fix:** Simply restart Claude Code. This resolves 90% of connection issues.

**Ready to work anyway?** Just tell me what you're building!
```

Never block the user - always offer a path forward.
