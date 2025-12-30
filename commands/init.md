---
title: Initialize Vibeship
description: Set up Vibeship for a new or existing project - your magic first moment
---

# Vibeship Initialization

Welcome a new user to Vibeship! This is their "magic first moment" - make it count.

## Philosophy

**Value in under 60 seconds.** Don't ask for configuration. Don't require IDs. Just help them get started immediately.

## Step 1: Warm Welcome

Start with excitement, not questions:

```
Welcome to Vibeship! I'm about to give you superpowers:

- I'll remember your project decisions across sessions
- I'll load specialist skills for your tech stack
- I'll scan your code for security issues before they ship

Let's get you set up in about 30 seconds.
```

## Step 2: Detect Current State

Silently check what exists:

1. **Check for existing `.mind/` folder** - If exists, they may already be set up
2. **Check for `package.json`** - Detect the tech stack
3. **Check for `.git/`** - See if it's a git repo

Based on findings, take the appropriate path:

### Path A: Existing Vibeship Project
If `.mind/` exists with content:
```
Looks like Vibeship is already set up here!

I found your project memory with:
- X decisions remembered
- X learnings captured
- Last session: [date]

Run `/vibeship-start` to load your context and continue where you left off.
```

### Path B: Existing Codebase, New to Vibeship
If code exists but no `.mind/`:
```
I see you have an existing project here. Let me analyze it...

**Detected Stack:**
- [Framework]: Next.js 14
- [Database]: Supabase
- [Styling]: Tailwind CSS

**What I'll Do:**
1. Create `.mind/` folder for your project memory
2. Load specialist skills for your stack
3. Remember decisions you make from now on

Ready to initialize? (I'll create a .mind/ folder in your project)
```

Then call `mind_recall()` to initialize the memory system.

### Path C: Empty Directory
If no code exists:
```
Fresh start - I love it!

**What do you want to build?**
- A SaaS product
- A marketplace
- An AI-powered tool
- Something else

Tell me your idea and I'll help you plan it out with the right stack and skills.
```

Then guide them to `spawner_plan(idea="...")`.

## Step 3: Initialize Memory

Once they're ready, set up memory:

```javascript
// Initialize Mind memory
mind_recall()

// Log the initialization
mind_log("Vibeship initialized for this project", type="progress")
```

## Step 4: Confirm Success

Show them what just happened:

```
## Vibeship is Ready!

**Memory**: Initialized at `.mind/`
**Skills**: [X skills loaded for your stack]
**Commands Available**:
- `/vibeship-start` - Begin a session (loads your context)
- `/vibeship-save` - Save decisions and learnings
- `/vibeship-status` - See what I remember
- `/vibeship-scan` - Security scan your code

**Pro tip**: I'll remember important decisions automatically, but you can always use `/vibeship-save` to explicitly capture something.

What would you like to build today?
```

## Error Handling

### If Mind MCP isn't connected:

```
I couldn't connect to the Memory service.

**What this means:**
- Your decisions won't persist between sessions
- You can still use Vibeship, just without memory

**How to fix it:**
1. Install Mind CLI: `npm install -g @anthropic/mind`
2. Verify it works: `mind --version`
3. Restart Claude Code

Want to continue without memory for now, or fix this first?
```

### If Spawner MCP isn't connected:

```
I couldn't connect to the Skills service.

**What this means:**
- I won't have specialist knowledge for your stack
- Basic Claude capabilities still work fine

**How to fix it:**
1. Check your internet connection
2. Try: `curl https://mcp.vibeship.co/health`
3. Restart Claude Code to reconnect

Want to continue without skills for now, or fix this first?
```

### If both fail:

```
Vibeship services aren't connecting right now.

**The good news:** You can still code normally with Claude.
**What you're missing:** Persistent memory and specialist skills.

**Quick fixes to try:**
1. Check internet connection
2. Restart Claude Code
3. Run `claude mcp list` to verify MCP status

I'll keep trying to connect in the background. Just start working and I'll let you know when services are back!
```

## Remember: Magic First Moment

The goal is to make the user feel:
1. **Welcomed** - Not interrogated
2. **Capable** - Not confused
3. **Excited** - Not overwhelmed

Give them value immediately. Configuration can come later.
