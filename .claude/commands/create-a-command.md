---
description: Create a new Claude Code slash command following best practices
allowed-tools: write, read, bash
argument-hint: <command-name> <purpose>
---

# Create a New Claude Code Command

I'll help you create a new slash command for Claude Code. The command name is: `$ARGUMENTS`

First, let me understand what this command should do:

1. What is the primary purpose of this command? (If not clear from the arguments provided)
2. Should this be a project command (.claude/commands/) or personal command (~/.claude/commands/)?
3. Are there any specific tools this command needs to use? (read, write, bash, grep, etc.)
4. Does this command need to accept arguments from the user?
5. Should this command reference any specific files or execute any bash commands?

Based on your requirements, I'll create a properly formatted command file that follows the Claude Code specification:

## Command Structure I'll Create:

- **YAML Frontmatter**: Including description, allowed-tools, and argument-hint if needed
- **Command Content**: Using appropriate special syntax ($ARGUMENTS, @files, !commands)
- **Best Practices**: Following naming conventions and organizational patterns

Let me analyze the purpose you've provided and create the appropriate command file.

If the command purpose isn't clear from `$ARGUMENTS`, I'll ask you clarifying questions to ensure the command meets your needs exactly.

## Steps:

1. Parse the command name and purpose from arguments
2. Determine appropriate tools and restrictions
3. Create the command file with proper frontmatter
4. Include relevant special syntax based on the command's purpose
5. Save to the appropriate location (.claude/commands/ for project commands)

Creating your command now...