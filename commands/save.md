---
title: Save Memory
description: Save a decision, learning, or progress update to your project memory
---

# Save to Project Memory

The user wants to save something to their project memory. Help them capture it properly.

## What to Save

Ask the user (if not already clear) what type of thing they want to save:

1. **Decision** - A choice that was made and why
   - Example: "Decided to use Supabase instead of Firebase because of RLS"

2. **Learning** - Something discovered that's worth remembering
   - Example: "Learned that Next.js middleware runs on every request"

3. **Problem** - An issue encountered and how it was resolved
   - Example: "Webhook signatures were failing because body wasn't raw"

4. **Progress** - A milestone or completion update
   - Example: "Finished the authentication flow"

## How to Save

### For permanent memory (decisions, learnings, problems):

Use `mind_log` with the appropriate type:
```
mind_log("Your message here", type="decision")  // or "learning", "problem", "progress"
```

### Also save to Spawner (for cloud backup):

Use `spawner_remember`:
```
spawner_remember({
  update: {
    decision: { what: "...", why: "..." }
  }
})
```

## Confirm the Save

After saving, confirm to the user:
- What was saved
- Where it was saved (Mind local + Spawner cloud)
- That it will be available next session

Example response:
"Saved your decision to use RLS. I'll remember this next time and it's backed up to the cloud."

## Be Proactive

If you notice the user made an important decision during the conversation that wasn't explicitly saved, offer to save it:

"I noticed you decided to [X] because [Y]. Want me to save that for future reference?"

## Handling Errors

### If Mind MCP fails to save:

```
## Couldn't Save to Local Memory

**What happened:** The memory service didn't respond.

**Your data is NOT lost!** Here's what I captured:
> "[The content they wanted to save]"

**What to do:**
1. Copy the text above (just in case)
2. Try: Restart Claude Code and run `/vibeship-save` again
3. Or manually add to `.mind/MEMORY.md` in your project

**Want me to try saving to cloud backup (Spawner) instead?**
```

### If Spawner fails to save:

```
## Couldn't Backup to Cloud

**Local save succeeded!** Your memory is safe in `.mind/MEMORY.md`

**Cloud backup failed** - this just means:
- No offsite backup this time
- You won't lose anything
- Cloud will sync next time it connects

**No action needed.** Your important stuff is saved locally.
```

### If user's input is unclear:

```
## What Would You Like to Save?

I want to help, but I'm not sure what to capture. Could you tell me:

**What type is it?**
- Decision (a choice you made)
- Learning (something you discovered)
- Problem (an issue and its solution)
- Progress (a milestone reached)

**What's the content?**
Just describe it in a sentence or two.

**Example:** "Decision: Using Supabase for auth because it has built-in RLS"
```

### After successful save:

Always confirm with context:

```
## Saved!

**Type:** Decision
**Content:** "Using Stripe for payments because of better subscription management"

**Where it's stored:**
- Local: `.mind/MEMORY.md`
- Cloud: Spawner backup

**I'll remember this** when you ask about payments, billing, or subscription decisions.
```
