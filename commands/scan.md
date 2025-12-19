---
description: Run a security scan on your project or a GitHub repository
---

# VibeShip Security Scan

The user wants to scan code for security vulnerabilities. Help them run a comprehensive scan.

## Step 1: Determine What to Scan

Ask (if not clear) what they want to scan:

1. **Current project** - Scan the codebase they're working in
2. **GitHub repository** - Scan a specific repo URL
3. **Specific files** - Focus on particular files or directories

## Step 2: Start the Scan

Use `scanner_scan` tool:
```
scanner_scan({
  repo_url: "https://github.com/owner/repo",
  branch: "main"  // optional
})
```

For local projects, you'll need to:
- Check if project has a GitHub remote
- Use that URL for scanning
- Or explain that local-only scanning requires pushing to GitHub first

## Step 3: Monitor Progress

The scan runs asynchronously. Use `scanner_status` to check progress:
```
scanner_status({ scan_id: "..." })
```

Keep the user informed:
- "Scan started! ID: xxx"
- "Scanning... 45% complete"
- "Scan finished! Found X issues."

## Step 4: Present Results

When scan completes, show a clear summary:

```
## 🔍 Security Scan Results

**Repository**: [repo name]
**Scan ID**: [id]
**Completed**: [timestamp]

### Summary
- 🔴 Critical: X
- 🟠 High: X
- 🟡 Medium: X
- 🟢 Low: X

### Top Issues

1. **[Severity] [Issue Title]**
   - File: `path/to/file.js:42`
   - CWE: CWE-79 (Cross-Site Scripting)
   - Description: [brief explanation]

2. ...

### Next Steps
- Use `/vibeship-scan fix` to get AI-generated fixes
- Use `/vibeship-scan details [finding-id]` to learn more about a specific issue
```

## Step 5: Offer Follow-up Actions

Based on results, offer to:
- Look up CVE/CWE details: `scanner_lookup_cve`, `scanner_lookup_cwe`
- Get AI-generated fixes: `scanner_get_fix`
- Generate master fix prompt: `scanner_master_prompt`

## Handling No Scanner MCP

If scanner tools aren't available (MCP not connected):

```
Scanner isn't connected yet. You can:
1. Wait for the Scanner MCP endpoint (coming soon)
2. Run Opengrep locally: `npx opengrep scan .`
3. Visit scanner.vibeship.co to scan your GitHub repo directly
```

## Remember the Results

After scanning, offer to save important findings to memory:
```
mind_log("Security scan found 3 critical XSS vulnerabilities in auth flow", type="problem")
```

This helps track what's been found and fixed over time.
