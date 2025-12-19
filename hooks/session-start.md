---
event: session_start
description: Automatically load memory context when a session begins
---

# Session Start Hook

When a new Claude Code session starts, automatically load the user's project memory.

## What This Hook Does

1. **Calls `mind_recall()`** - Loads context from previous sessions
2. **Surfaces reminders** - Shows any pending reminders set in previous sessions
3. **Detects session gaps** - If significant time passed, promotes important SESSION.md items to MEMORY.md

## Expected Behavior

When the user starts Claude Code in a project with the VibeShip plugin:

1. Mind automatically loads
2. User sees what was remembered from last time
3. Any due reminders are displayed
4. Session is ready to continue from where they left off

## If Mind Is Not Available

If the Mind MCP isn't connected:
- Skip silently (don't error)
- User can still work, just without persistent memory
- Suggest running `/vibeship-start` manually if they want to troubleshoot

## No Prompting

This hook should be invisible to the user. Don't output anything unless:
- There are pending reminders to show
- There's critical context they need to know about
- Something went wrong that needs attention
