---
title: Check Status
description: Check what Vibeship remembers about your project and current session
---

# Vibeship Status Check

The user wants to see what's being remembered about their project. Show them a clear overview.

## Step 1: Get Memory Status

Call `mind_status()` to check the health of local memory.

## Step 2: Get Session State

Call `mind_session()` to get:
- Current goal
- Current approach
- Active blockers
- Rejected approaches
- Working assumptions
- Recent discoveries

## Step 3: Get Spawner Project Status

Call `spawner_orchestrate` with minimal context to see what the cloud remembers:
- Project recognition
- Loaded skills
- Loaded rules

## Step 4: Present Status Clearly

Format the response like this:

```
## 🧠 Your Project Memory

**Project**: [name from spawner or mind]
**Goal**: [goal from mind session]
**Stack**: [detected stack]

### Local Memory (Mind)
- Decisions remembered: X
- Learnings captured: X
- Problems documented: X
- Memory health: [healthy/needs attention]

### Cloud Memory (Spawner)
- Skills loaded: [list]
- Rules active: [list]
- Project ID: [id]

### Current Session
- Blockers: [list or "None"]
- Assumptions: [list or "None"]
- Last activity: [timestamp]
```

## Step 5: Offer Actions

If there are issues, suggest fixes:
- "Your local memory is getting large. Want me to summarize old entries?"
- "No goal is set for this session. What are you working on?"
- "You have 3 unresolved blockers. Want to tackle them?"

## Keep It Actionable

The status check should lead to action, not just information. Always end with:
- What's going well
- What needs attention
- A suggested next step

## Handling Errors

### If Mind status fails:

```
## Local Memory Status Unknown

**What happened:** Couldn't connect to memory service.

**What I can tell you:**
- Check if `.mind/` folder exists in your project
- If it exists, your memories are safe (just can't read them right now)
- If it doesn't exist, run `/vibeship-init` to set up

**Quick fix:** Restart Claude Code and try `/vibeship-status` again.

**In the meantime:** What are you working on? I can still help!
```

### If Spawner status fails:

```
## Cloud Status Unavailable

**Local memory is working!** Here's what I found:
[Show local memory status]

**Cloud status couldn't load** - this means:
- Can't show loaded skills right now
- Your project data is still safe
- Skills will reload when connection returns

**No action needed** unless you want to fix the connection:
1. Check internet
2. Run `curl https://mcp.vibeship.co/health`
3. Restart Claude Code
```

### If memory is empty:

```
## Fresh Start Detected

**No memories found yet** - and that's okay!

This means either:
- You're new to this project (welcome!)
- Memory was recently cleared
- The `.mind/` folder doesn't exist yet

**To get started:**
1. Run `/vibeship-init` to set up memory
2. Or just start coding - I'll offer to save important decisions as we go

**Pro tip:** Use `/vibeship-save` anytime you make a decision worth remembering.
```

### If memory is very large:

```
## Memory Health Check

**Your memory is getting large** (X entries, Y KB)

**This might slow things down.** Consider:

1. **Summarize old entries:**
   "Hey, can you summarize my old decisions into key points?"

2. **Archive completed projects:**
   Move old `.mind/` to a backup location

3. **Clean up duplicates:**
   I can help identify redundant memories

**Want me to analyze your memory and suggest what to clean up?**
```

### Status display format:

Always use this structure for clarity:

```
## Vibeship Status

### Memory (Local)
| Metric | Value |
|--------|-------|
| Decisions | 12 |
| Learnings | 8 |
| Problems | 3 |
| Health | Healthy |

### Skills (Cloud)
| Loaded | Status |
|--------|--------|
| Next.js App Router | Active |
| Supabase Backend | Active |
| TypeScript Strict | Active |

### Current Session
- **Goal:** Building auth flow
- **Blockers:** None
- **Active for:** 45 minutes

### Recommendations
1. Your session is going well!
2. Consider saving your progress before taking a break
3. Next suggested action: [based on context]
```
