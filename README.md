# VibeShip Plugin for Claude Code

AI-powered development with persistent memory, specialist skills, and security scanning.

## What This Plugin Does

**Memory** - Claude remembers your project across sessions. Decisions, learnings, problems, and progress are all saved automatically.

**Skills** - Claude loads specialized knowledge for your tech stack. Building with Next.js + Supabase? It knows the gotchas.

**Security** - Scan your code for vulnerabilities. Get AI-generated fixes for what's found.

## Installation

Copy this plugin folder to your Claude Code plugins directory:

```bash
# macOS/Linux
cp -r vibeship-plugin ~/.claude/plugins/

# Windows
xcopy vibeship-plugin %USERPROFILE%\.claude\plugins\vibeship-plugin /E /I
```

Restart Claude Code. The plugin loads automatically.

## Slash Commands

### `/vibeship-start`
Start a VibeShip session. Loads your project memory and greets you with context.

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

### Scanner not available
The Scanner MCP endpoint is coming soon. For now, use the web interface at scanner.vibeship.co.

## Support

- Issues: https://github.com/vibeship/vibeship-plugin/issues
- Docs: https://vibeship.co/docs
- Discord: https://discord.gg/vibeship

## License

MIT
