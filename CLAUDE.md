# Claude Code Commands Collection

This repository is set up to collect and organize slash commands for Claude Code.

## Repository Structure

```
claude-code-commands-collection/
├── CLAUDE.md          # This file
├── LICENSE            # Repository license
├── .claude/
│   └── commands/      # Directory for slash commands (currently empty)
└── commands/          # Alternative commands directory (currently empty)
```

## About Claude Code Slash Commands

Claude Code supports custom slash commands that allow you to create reusable prompts and workflows. These commands:

- Are stored as Markdown files in `.claude/commands/` (project-level) or `~/.claude/commands/` (personal)
- Support YAML frontmatter for metadata (description, allowed-tools, argument-hint)
- Can use `$ARGUMENTS` placeholder for dynamic input
- Can reference files with `@filename` syntax
- Can execute bash commands with `!command` syntax

## Getting Started

To add slash commands to this collection:

1. Create `.md` files in the `.claude/commands/` directory
2. Add YAML frontmatter with command metadata
3. Write your command prompt using Claude Code's special syntax

### Command File Structure

```markdown
---
description: Brief description of what the command does
allowed-tools: read, write, bash, grep
argument-hint: expected arguments format
---

# Your command prompt here

Use $ARGUMENTS for dynamic values
Reference files with @filename
Execute commands with !command
```

## Documentation

- [Custom Slash Commands Specification](./custom-slash-commands-spec.md) - Complete specification for creating slash commands
- [Official Claude Code Documentation](https://docs.anthropic.com/en/docs/claude-code)
- [Slash Commands Guide](https://docs.anthropic.com/en/docs/claude-code/slash-commands)
- [Claude Code Overview](https://docs.anthropic.com/en/docs/claude-code/overview)