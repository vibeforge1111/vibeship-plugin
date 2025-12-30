---
title: Security Scan
description: Run a security scan on your project or a GitHub repository
---

# Vibeship Security Scan

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

## Handling Errors

### If Scanner MCP isn't connected:

```
## Scanner Unavailable

**What happened:** Can't connect to the security scanning service.

**You have alternatives!**

| Option | How | Best For |
|--------|-----|----------|
| **Local SAST** | `npx opengrep scan .` | Quick code analysis |
| **Dependency check** | `npm audit` or `trivy fs .` | Known vulnerabilities |
| **Web scanner** | Visit scanner.vibeship.co | Full GitHub repo scan |
| **Restart** | Close/reopen Claude Code | Connection issues |

**Want me to run a local scan instead?** I can use opengrep or npm audit right now.
```

### If scan takes too long:

```
## Scan Still Running

**Scan ID:** [id]
**Started:** [time ago]
**Status:** Processing...

**Large repos take longer.** Here's what's happening:
1. Cloning repository
2. Running security analyzers (opengrep, trivy, gitleaks)
3. Aggregating results

**While you wait:**
- Continue coding - I'll notify you when done
- Check status: `/vibeship-scan status [id]`
- Cancel if needed: `/vibeship-scan cancel [id]`

**Typical scan times:**
- Small repo (<1000 files): 1-2 minutes
- Medium repo: 3-5 minutes
- Large repo: 10+ minutes
```

### If scan finds nothing:

```
## No Vulnerabilities Found

**Great news!** The scan completed with no security issues detected.

**What was checked:**
- Static code analysis (opengrep)
- Dependency vulnerabilities (trivy)
- Secret detection (gitleaks)
- npm audit findings

**Keep in mind:**
- Automated scans catch common issues
- They don't find everything
- Consider manual security review for sensitive code

**Confidence level:** High for known patterns, moderate for logic flaws.
```

### If scan finds critical issues:

```
## Critical Vulnerabilities Found

**Action Required!** Found [X] critical security issues.

### Top Priority Fixes:

| # | Issue | File | Impact |
|---|-------|------|--------|
| 1 | SQL Injection | db/query.js:42 | Data breach risk |
| 2 | Hardcoded secret | config.js:15 | Credential exposure |

### Immediate Steps:

1. **Don't deploy** until these are fixed
2. **Rotate any exposed secrets** immediately
3. Ask me: "Help me fix the SQL injection in db/query.js"

### Get Help:

- `/vibeship-scan fix 1` - AI-generated fix for issue #1
- `/vibeship-scan explain [CWE-ID]` - Learn about the vulnerability type
- "Review my auth code for security issues" - Manual review

**I can help fix each issue.** Which one should we tackle first?
```

### If repo URL is invalid:

```
## Invalid Repository

**Couldn't access:** [url]

**This might be because:**
- The URL has a typo
- The repo is private (scanner needs public access)
- The repo doesn't exist

**For private repos:**
1. Make sure the repo exists on GitHub
2. Check if it's set to public
3. Or push to a public fork for scanning

**Correct format:** `https://github.com/owner/repo`

**Want to scan the current local project instead?**
```

## Remember the Results

After scanning, offer to save important findings to memory:
```
mind_log("Security scan found 3 critical XSS vulnerabilities in auth flow", type="problem")
```

This helps track what's been found and fixed over time.
