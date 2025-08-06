# Custom Slash Commands Specification

This document contains the official specification for Claude Code custom slash commands, extracted from the [official documentation](https://docs.anthropic.com/en/docs/claude-code/slash-commands#custom-slash-commands).

## Overview

Custom slash commands allow you to define frequently-used prompts as Markdown files that Claude Code can execute. They provide a way to create reusable workflows and automate common tasks.

## Command Scopes

### 1. Project Commands

- **Location**: `.claude/commands/`
- **Visibility**: Shared with team (can be checked into git)
- **Display**: Marked as "(project)" in help menu
- **Use case**: Team-specific workflows and standards

### 2. Personal Commands

- **Location**: `~/.claude/commands/`
- **Visibility**: Available across all projects
- **Display**: Marked as "(user)" in help menu
- **Use case**: Personal productivity tools and preferences

## Command Syntax

```
/<command-name> [arguments]
```

## File Format

Commands are defined as Markdown files with `.md` extension.

### YAML Frontmatter (Optional)

```yaml
---
allowed-tools: comma-separated list of tools
description: Brief description of the command
argument-hint: expected format for arguments
---
```

#### Frontmatter Options

- **`allowed-tools`**: Restricts which tools Claude can use when executing this command
  - Example: `read, write, bash, grep`
  - Can specify specific bash commands: `Bash(git add:*), Bash(git status:*)`
- **`description`**: Shows in the help menu when listing commands
- **`argument-hint`**: Displays expected argument format to users

## Special Syntax

### 1. Dynamic Arguments: `$ARGUMENTS`

The `$ARGUMENTS` placeholder is replaced with whatever the user types after the command.

**Example:**

```bash
# Create command
echo 'Fix issue #$ARGUMENTS following our coding standards' > .claude/commands/fix-issue.md

# Usage
/fix-issue 123
# Expands to: "Fix issue #123 following our coding standards"
```

### 2. Bash Command Execution: `!command`

Execute bash commands and include their output in the prompt using the `!` prefix.

**Example:**

```markdown
---
allowed-tools: Bash(git add:*), Bash(git status:*), Bash(git commit:*)
description: Create a git commit with context
---

## Current Repository State
- Git status: !`git status`
- Recent changes: !`git diff HEAD`

Create a meaningful commit message for these changes.
```

### 3. File References: `@filename`

Include file contents directly in the prompt using the `@` prefix.

**Example:**

```markdown
---
description: Review code implementation
---

Review the following implementation:
@src/utils/helpers.js

Check for:
- Code quality issues
- Performance optimizations
- Security concerns
```

**Multiple files:**

```markdown
Compare the old and new implementations:
- Old: @src/old-version.js
- New: @src/new-version.js
```

## Namespacing

Commands can be organized in subdirectories, creating namespaced commands:

- File: `.claude/commands/frontend/component.md`
- Command: `/frontend:component`

- File: `.claude/commands/backend/api/endpoint.md`
- Command: `/backend:api:endpoint`

## Extended Thinking

Slash commands can trigger Claude's extended thinking mode by including specific keywords or phrases in the command prompt that indicate complex reasoning is needed.

## Creating Commands

### Quick Examples

```bash
# Create a simple project command
mkdir -p .claude/commands
echo "Analyze this code for performance issues: @$ARGUMENTS" > .claude/commands/optimize.md

# Create a personal command with frontmatter
cat > ~/.claude/commands/review.md << 'EOF'
---
description: Comprehensive code review
allowed-tools: read, grep, bash
argument-hint: <file or directory>
---

Perform a comprehensive code review of @$ARGUMENTS

Focus on:
- Code quality and best practices
- Potential bugs or edge cases
- Performance implications
- Security concerns
- Test coverage
EOF
```

## Best Practices

1. **Keep commands focused**: Each command should do one thing well
2. **Use descriptive names**: Make it clear what the command does
3. **Leverage arguments**: Use `$ARGUMENTS` for flexibility
4. **Combine features**: Mix file references, bash commands, and arguments
5. **Document with frontmatter**: Help users understand command usage
6. **Organize with directories**: Use namespacing for related commands
7. **Test thoroughly**: Ensure commands work as expected before sharing

## Advanced Usage

### Conditional Logic

```markdown
Check the current branch: !`git branch --show-current`
If on main/master, ensure extra caution with changes.
```

### Multiple File Patterns

```markdown
Review all test files:
@**/*test*.js
@**/*spec*.js
```

### Chaining Commands

Commands can reference other commands or build upon each other by creating workflows that span multiple command files.

## Limitations and Considerations

- Commands are executed in the current working directory
- File references are relative to where Claude Code is run
- Bash commands execute with the same permissions as Claude Code
- Large file references may impact performance
- Tool restrictions in frontmatter help prevent unintended actions
