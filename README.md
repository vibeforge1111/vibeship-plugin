# Vibeship Plugin for Claude Code

**Ship faster with an AI that actually remembers your project.**

Stop re-explaining your codebase every session. Vibeship gives Claude Code persistent memory, specialist skills for your stack, and security scanning - all in one install.

## Why Vibeship?

You're vibe coding - shipping fast, iterating quickly, building products. But every new Claude session starts from zero. You waste time re-explaining decisions, re-discovering gotchas, re-learning your own codebase.

**Vibeship fixes this.**

- **Memory** - Claude remembers your project across sessions. Decisions, learnings, problems - all persisted.
- **Skills** - Claude loads specialized knowledge for your stack. Next.js + Supabase? It knows the sharp edges.
- **Security** - Scan for vulnerabilities before you ship. Get AI-generated fixes.

## Quick Start (2 minutes)

### Option 1: Marketplace Install (Recommended)

```bash
# Add the Vibeship marketplace
claude plugin marketplace add vibeforge1111/vibeship-plugin

# Install the plugin
claude plugin install vibeship@vibeforge1111
```

### Option 2: Manual Install

```bash
# Clone the repo
git clone https://github.com/vibeforge1111/vibeship-plugin.git

# Copy to plugins directory
# macOS/Linux
cp -r vibeship-plugin ~/.claude/plugins/

# Windows
xcopy vibeship-plugin %USERPROFILE%\.claude\plugins\vibeship-plugin /E /I
```

Restart Claude Code. You're ready to ship.

## Slash Commands

### `/vibeship-init`
**Start here for new projects.** Your magic first moment with Vibeship:
- Detects your existing codebase and tech stack
- Sets up memory for your project
- Gets you productive in under 60 seconds

### `/vibeship-start`
Start a Vibeship session. Loads your project memory and greets you with context.

### `/vibeship-save`
Save something important to memory:
- Decisions you made and why
- Learnings you want to remember
- Problems you encountered and how you solved them
- Progress milestones

### `/vibeship-status`
Check what's being remembered:
- Local memory health
- Cloud skills loaded
- Current session state
- Any blockers or issues

### `/vibeship-scan`
Run a security scan on your code:
- Scan current project or any GitHub repo
- See vulnerabilities by severity
- Get AI-generated fixes
- Look up CVE/CWE details

## How It Works

### Memory (Mind MCP)
Local persistent memory stored in your project:
- `.mind/MEMORY.md` - Permanent cross-session memory
- `.mind/SESSION.md` - Current session notes

### Skills (Spawner MCP)
Cloud-hosted specialist knowledge:
- Stack-specific gotchas and best practices
- Validation rules for your tech choices
- Onboarding guidance for new projects

### Security (Scanner MCP)
Code scanning powered by:
- Opengrep (SAST)
- Trivy (dependencies)
- Gitleaks (secrets)
- npm audit (Node packages)

## Requirements

- Claude Code 2.0.0 or later
- Node.js 18+ (for mcp-remote)
- Internet connection (for Spawner and Scanner)

## Privacy

**Local Memory (Mind)**: Stored only on your machine in `.mind/` folder. Add to `.gitignore` if you don't want to version it.

**Cloud Skills (Spawner)**: Your project context is sent to `mcp.vibeship.co` to load relevant skills. No code is stored.

**Security Scans (Scanner)**: Repository URLs are sent to `scanner.vibeship.co`. Scan results are stored for 30 days.

## Troubleshooting

### MCP servers not connecting
Check that `npx` is available and you have internet access:
```bash
npx -y mcp-remote https://mcp.vibeship.co/mcp
```

### Memory not persisting
Make sure the `.mind/` folder is writable. Check `mind_status()` for health info.

### Scanner authentication for private repos
Run `/vibeship-scan` and follow the auth flow to scan private repositories.

### Mind CLI not found
Mind requires separate installation. See: https://github.com/anthropics/mind

## Support

- Issues: https://github.com/vibeforge1111/vibeship-plugin/issues
- Docs: https://vibeship.co/docs
- Discord: https://discord.gg/vibeship

## License

Apache 2.0 - See [LICENSE](LICENSE) file.
