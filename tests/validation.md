# Vibeship Plugin Validation Tests

Use this checklist to validate the plugin before releasing.

## Prerequisites

- [ ] Claude Code 2.0.0+ installed
- [ ] Node.js 18+ installed
- [ ] Internet connection available

## Installation Validation

### Plugin Structure
```bash
# Verify required files exist
ls .claude-plugin/plugin.json    # Plugin manifest
ls .claude-plugin/marketplace.json  # Marketplace registration
ls .mcp.json                     # MCP server configuration
ls hooks/hooks.json              # Session hooks
ls commands/                     # Command directory
```

**Expected:** All files present

### Plugin Validation
```bash
# Validate plugin structure
claude plugin validate .
```

**Expected:** No errors

### MCP Connection
```bash
# Verify MCP servers
claude mcp list
```

**Expected:** Should show mind, spawner, scanner servers

---

## Command Tests

### /vibeship-init

| Test Case | Steps | Expected Result |
|-----------|-------|-----------------|
| Fresh project | Create empty dir, run `/vibeship-init` | Detects empty, offers to help plan |
| Existing code | Run in project with package.json | Detects stack, offers to initialize memory |
| Already initialized | Run in project with `.mind/` | Detects existing setup, suggests `/vibeship-start` |
| No MCP | Disconnect MCP, run `/vibeship-init` | Shows actionable error with alternatives |

### /vibeship-start

| Test Case | Steps | Expected Result |
|-----------|-------|-----------------|
| Normal start | Run in initialized project | Loads memory, greets with context |
| First session | Run after `/vibeship-init` | Sets up session, shows available commands |
| Mind MCP down | Stop mind, run `/vibeship-start` | Shows actionable error, offers to continue |
| Spawner down | Stop spawner, run `/vibeship-start` | Shows actionable error, continues without skills |
| Both down | Stop both, run `/vibeship-start` | Shows combined error, doesn't block user |

### /vibeship-save

| Test Case | Steps | Expected Result |
|-----------|-------|-----------------|
| Save decision | "Save: decided to use RLS" | Saves to memory, confirms with context |
| Save learning | "Save learning: Next.js caches by default" | Saves as learning type |
| Unclear input | "Save this" | Asks for clarification with examples |
| Mind MCP down | Stop mind, try to save | Shows error, offers cloud backup alternative |
| Success confirmation | Any successful save | Shows what was saved and where |

### /vibeship-status

| Test Case | Steps | Expected Result |
|-----------|-------|-----------------|
| Normal status | Run after some activity | Shows memory stats, skills, session info |
| Empty memory | Run in fresh project | Shows "fresh start" message with guidance |
| Large memory | Add many entries, check status | Shows health warning with cleanup suggestions |
| Mind down | Stop mind, check status | Shows partial status with troubleshooting |
| Full status | Everything working | Shows formatted tables with recommendations |

### /vibeship-scan

| Test Case | Steps | Expected Result |
|-----------|-------|-----------------|
| Scan GitHub repo | Provide valid public repo URL | Starts scan, shows progress, returns results |
| Scan local project | Run in project with GitHub remote | Detects remote, scans it |
| No vulnerabilities | Scan clean project | Shows "no issues" with confidence note |
| Critical issues | Scan project with known issues | Shows prioritized list with fix guidance |
| Scanner down | Stop scanner, try to scan | Shows alternatives (local tools, web interface) |
| Invalid URL | Provide bad URL | Shows clear error with format guidance |
| Long scan | Scan large repo | Shows progress, offers status check |

---

## Error Handling Tests

### Connection Failures

| Scenario | Expected Behavior |
|----------|-------------------|
| Mind MCP timeout | Actionable error, offer to continue |
| Spawner MCP timeout | Actionable error, basic mode available |
| Scanner MCP timeout | Alternatives offered (local tools) |
| All MCP down | Combined error, user not blocked |

### User Input Errors

| Scenario | Expected Behavior |
|----------|-------------------|
| Empty input | Ask for clarification with examples |
| Invalid format | Show correct format with examples |
| Unknown command | Suggest closest valid command |

---

## Integration Tests

### Memory Persistence

1. Run `/vibeship-init`
2. Run `/vibeship-save` with a decision
3. Close Claude Code
4. Reopen Claude Code
5. Run `/vibeship-start`

**Expected:** Saved decision is recalled

### Skill Loading

1. Create Next.js project with `package.json`
2. Run `/vibeship-start`

**Expected:** Next.js-related skills loaded

### Security + Memory Integration

1. Run `/vibeship-scan` on a repo
2. Scan finds issues
3. Offer to save findings to memory

**Expected:** Findings saved for future reference

---

## Performance Checks

| Operation | Target Time |
|-----------|-------------|
| `/vibeship-init` | < 5 seconds |
| `/vibeship-start` | < 10 seconds |
| `/vibeship-status` | < 5 seconds |
| `/vibeship-save` | < 3 seconds |
| `/vibeship-scan` start | < 10 seconds (scan async) |

---

## Edge Cases

- [ ] Unicode in project names
- [ ] Spaces in file paths
- [ ] Very long memory content
- [ ] Rapid successive commands
- [ ] Concurrent sessions (same project)

---

## Sign-off

| Validator | Date | Version | Result |
|-----------|------|---------|--------|
| | | | |
