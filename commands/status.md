---
description: Check what VibeShip remembers about your project and current session
---

# VibeShip Status Check

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
