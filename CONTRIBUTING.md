# Contributing to Vibeship Plugin

Thanks for wanting to contribute! Here's how to get involved.

## Quick Start for Contributors

1. Fork the repo
2. Clone your fork
3. Make changes
4. Test locally (see below)
5. Submit a PR

## Local Development

### Testing the Plugin

```bash
# Validate the plugin structure
claude plugin validate .

# Test MCP connections
claude mcp list
```

### Testing Commands

The slash commands are in `commands/`. Each is a markdown file with YAML frontmatter:

```markdown
---
title: Command Title
description: What this command does
---

Command instructions...
```

### Testing Hooks

Hooks are defined in `hooks/hooks.json`. Test by restarting Claude Code and checking if the session-start hook fires.

## What We're Looking For

### High Priority
- Error handling improvements for MCP failures
- Better fallbacks when cloud services are unavailable
- Additional slash commands for common workflows
- Improved documentation with examples

### Nice to Have
- GIFs/screenshots for the README
- Integration tests
- Support for additional MCP servers

## Code Style

- Keep it simple - this is for vibe coders who ship fast
- Markdown files use standard formatting
- JSON files should be valid (run through jsonlint)
- Test your changes before submitting

## Pull Request Process

1. Update the CHANGELOG.md with your changes
2. Update README.md if you added new features
3. Make sure `claude plugin validate .` passes
4. Describe what you changed and why in the PR

## Questions?

- Open an issue for bugs or feature requests
- Join the Discord: https://discord.gg/vibeship

## License

By contributing, you agree that your contributions will be licensed under the Apache 2.0 License.
