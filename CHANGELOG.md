# Changelog

All notable changes to the Vibeship plugin will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.1.0] - 2024-12-30

### Added
- **`/vibeship-init` command**: New onboarding command for first-time users
  - Magic first moment - value in under 60 seconds
  - Automatic stack detection for existing codebases
  - Guided setup for empty directories
  - Clear pathways for new vs existing projects

- **Validation test suite**: `tests/validation.md`
  - Comprehensive test cases for all commands
  - Error handling test scenarios
  - Integration tests for memory persistence
  - Performance benchmarks

### Improved
- **Enhanced error messages across all commands**
  - Actionable guidance instead of technical errors
  - Clear "what happened / what to do" format
  - Alternatives offered when services unavailable
  - Never blocks user - always provides path forward

- **`/vibeship-start`**: Better connection failure handling with troubleshooting steps
- **`/vibeship-save`**: Clearer confirmation of what was saved and where
- **`/vibeship-status`**: Formatted tables, health warnings, cleanup suggestions
- **`/vibeship-scan`**: Prioritized critical issues, inline fix guidance

### Design Principles Applied
- MCP Product Design: Progressive disclosure, sensible defaults
- MCP Developer: Atomic tools, actionable errors
- User-first error handling throughout

## [1.0.0] - 2024-12-21

### Added
- **Mind Integration**: Local persistent memory across Claude Code sessions
  - `mind_recall()` - Load context from previous sessions
  - `mind_log(msg, type)` - Log decisions, learnings, problems, progress
  - `mind_session()` - Get current session state
  - `mind_blocker()` - Log blockers and auto-search for solutions
  - `mind_search()` - Query memories
  - `mind_remind()` - Set reminders
  - `mind_checkpoint()` - Force memory sync
  - `mind_status()` - Check memory health
  - Two-layer memory system (SESSION.md ephemeral, MEMORY.md permanent)

- **Spawner Integration**: Cloud skills, validation, and project orchestration
  - `spawner_orchestrate` - Detect stack and load appropriate skills
  - `spawner_remember` - Sync memories to cloud backup
  - Automatic skill loading based on project context

- **Scanner Integration**: Security scanning and vulnerability analysis
  - `scanner_scan` - Start security scans on local or remote repos
  - `scanner_status` - Monitor scan progress
  - `scanner_lookup_cve` - Get CVE details
  - `scanner_lookup_cwe` - Get CWE details
  - Severity breakdown and AI-powered fix suggestions

- **Slash Commands**:
  - `/vibeship-start` - Initialize session with memory + skills
  - `/vibeship-save` - Capture decisions, learnings, problems
  - `/vibeship-status` - View memory health and session state
  - `/vibeship-scan` - Run security scans

- **Hooks**:
  - `session-start` - Automatically load memory on Claude Code startup

- **Documentation**:
  - README with installation instructions
  - CLAUDE.md with developer guidance
  - Apache 2.0 license

### Security
- All data handling documented in README
- Local-first approach with optional cloud sync
- No secrets stored in memory files

[1.1.0]: https://github.com/vibeforge1111/vibeship-plugin/releases/tag/v1.1.0
[1.0.0]: https://github.com/vibeforge1111/vibeship-plugin/releases/tag/v1.0.0
