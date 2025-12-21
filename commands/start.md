---
title: Start Session
description: Start a VibeShip session - loads your project memory and skills
---

# VibeShip Session Start

You are starting a VibeShip-powered development session. Follow these steps:

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
