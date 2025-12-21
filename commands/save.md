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
