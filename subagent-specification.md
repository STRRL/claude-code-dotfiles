# Claude Code Subagent Specification

## Overview

Subagents in Claude Code are specialized AI assistants that can be invoked to handle specific types of tasks. They operate in a separate context window with their own system prompts and tool restrictions, allowing for focused, task-specific behavior.

## What Are Subagents?

Subagents are:
- **Specialized assistants** with deep expertise in specific domains
- **Automatically invokable** based on task context and descriptions
- **Isolated contexts** that don't share conversation history with the main thread
- **Tool-restricted** to only use the tools necessary for their specific purpose
- **Reusable components** that can be shared across projects or users

## File Structure

Subagents are defined as YAML files stored in:
- **Project-level**: `.claude/agents/` (specific to current project)
- **User-level**: `~/.claude/agents/` (available across all projects)

### Basic YAML Structure

```yaml
name: agent-name
description: Brief description of what this agent does and when it should be used
tools: [read, write, edit, grep, glob, bash, websearch]
system_prompt: |
  Detailed instructions for the agent's behavior...
```

## Configuration Fields

### Required Fields

#### `name` (string)
- **Purpose**: Unique identifier for the subagent
- **Format**: Lowercase, hyphenated (e.g., `code-reviewer`, `test-writer`)
- **Constraints**: Must be unique within the project/user scope

#### `description` (string)
- **Purpose**: Describes the agent's purpose and triggers automatic invocation
- **Best Practice**: Be specific about what tasks this agent handles
- **Example**: "Reviews code for quality, best practices, and potential issues. Automatically triggered after significant code changes."

#### `system_prompt` (string)
- **Purpose**: Detailed instructions that define the agent's behavior
- **Format**: Multi-line string using YAML's `|` literal block scalar
- **Should Include**:
  - Clear role definition
  - Specific responsibilities
  - Process/workflow to follow
  - Output format expectations
  - Domain-specific guidelines

### Optional Fields

#### `tools` (array)
- **Purpose**: Restricts which tools the agent can access
- **Default**: Inherits all tools from main thread if not specified
- **Available Tools**:
  - `read` - Read files
  - `write` - Write new files
  - `edit` - Edit existing files
  - `multiedit` - Multiple edits to same file
  - `grep` - Search file contents
  - `glob` - Find files by pattern
  - `ls` - List directory contents
  - `bash` - Execute shell commands
  - `websearch` - Search the web
  - `webfetch` - Fetch web content
  - `todowrite` - Manage task lists

## Building Effective Subagents

### 1. Define Clear Purpose

Each subagent should have a single, well-defined purpose:

```yaml
name: security-auditor
description: Performs security audits and identifies vulnerabilities in code
```

### 2. Write Detailed System Prompts

Structure your system prompt with:

```yaml
system_prompt: |
  You are a [role] specialized in [domain].
  
  Your responsibilities:
  1. [Primary task]
  2. [Secondary task]
  
  Process:
  - [Step 1]
  - [Step 2]
  
  Guidelines:
  - [Guideline 1]
  - [Guideline 2]
  
  Output format:
  - [Format specification]
```

### 3. Restrict Tool Access

Only grant tools necessary for the task:

```yaml
# Documentation writer doesn't need bash access
tools: [read, write, edit, grep, glob]

# Security auditor should be read-only
tools: [read, grep, glob]
```

### 4. Make Agents Proactive

Write descriptions that enable automatic invocation:

```yaml
description: Automatically reviews code after significant changes, identifying bugs and suggesting improvements
```

## Invocation Methods

### 1. Automatic Invocation

Agents are automatically invoked when:
- Task description matches agent's purpose
- Certain keywords trigger the agent
- Context suggests the agent's expertise is needed

### 2. Explicit Invocation

Users can explicitly request an agent:
```
"Use the code-reviewer agent to check this implementation"
```

### 3. Chained Invocation

Agents can be chained for complex workflows:
1. `researcher` explores approaches
2. `planner` creates implementation plan
3. `test-writer` creates test suite

## Best Practices

### DO:
- ✅ Create focused, single-purpose agents
- ✅ Write comprehensive system prompts
- ✅ Use descriptive names and descriptions
- ✅ Limit tool access to minimum required
- ✅ Include output format specifications
- ✅ Version control project-level agents
- ✅ Test agents with various inputs

### DON'T:
- ❌ Create overly broad agents
- ❌ Grant unnecessary tool permissions
- ❌ Use vague descriptions
- ❌ Share sensitive information in prompts
- ❌ Create duplicate agents with similar purposes

## Examples

### Example 1: Test Writer Agent

```yaml
name: test-writer
description: Writes comprehensive unit and integration tests for code
tools: [read, write, edit, glob, grep]
system_prompt: |
  You are an expert test engineer specialized in writing comprehensive tests.
  
  Your responsibilities:
  1. Write unit tests for functions and methods
  2. Create integration tests for components
  3. Ensure edge cases are covered
  4. Achieve high code coverage
  
  Testing approach:
  - Analyze code to understand all execution paths
  - Test happy paths, error conditions, and edge cases
  - Use appropriate mocking strategies
  - Follow AAA pattern (Arrange, Act, Assert)
  
  Best practices:
  - Keep tests independent and idempotent
  - Use descriptive test names
  - One assertion per test when possible
  - Include setup and teardown as needed
  
  Detect and use the existing testing framework in the codebase.
```

### Example 2: PRD Writer Agent

```yaml
name: prd-writer
description: Iteratively collects product requirements through questions, then generates PRD documentation
tools: [read, write, edit]
system_prompt: |
  You are a Product Requirements Document specialist.
  
  Phase 1: Requirement Gathering
  Ask targeted questions about:
  - Problem statement
  - Target users
  - Success criteria
  - Constraints
  
  Phase 2: Documentation
  Generate comprehensive PRD.md with:
  - Executive summary
  - User stories
  - Functional requirements
  - Non-functional requirements
  - Timeline and milestones
  
  Keep questions conversational and focused.
```

### Example 3: Bug Hunter Agent

```yaml
name: bug-hunter
description: Specializes in finding and debugging complex issues in code
tools: [read, grep, glob]
system_prompt: |
  You are an expert debugger specialized in finding bugs.
  
  Debugging approach:
  - Start from error symptoms
  - Trace execution paths
  - Check edge cases
  - Verify assumptions
  
  Common bug patterns:
  - Off-by-one errors
  - Null references
  - Race conditions
  - Type mismatches
  
  Output format:
  - Bug description
  - Root cause analysis
  - Affected locations (file:line)
  - Proposed fix
```

## Advanced Features

### Context Passing

While agents operate in separate contexts, they can:
- Read files created by other agents
- Reference documentation from previous steps
- Build upon research or plans

### Tool Inheritance

If `tools` is not specified, agents inherit all available tools from the main thread. This is useful for general-purpose agents but should be restricted for specialized ones.

### Conditional Invocation

Agents can be configured to trigger on specific conditions:
- After certain file types are modified
- When specific commands are run
- Based on error patterns

## Testing Subagents

To test a subagent:

1. **Create test scenarios** that match the agent's purpose
2. **Invoke explicitly** to verify behavior
3. **Check automatic triggers** work as expected
4. **Verify tool restrictions** are enforced
5. **Test edge cases** and error handling

## Troubleshooting

### Agent Not Triggering
- Check description is specific enough
- Verify agent file is in correct location
- Ensure YAML syntax is valid

### Unexpected Behavior
- Review system prompt for ambiguities
- Check tool permissions
- Verify no conflicts with other agents

### Performance Issues
- Limit tool access to necessary ones
- Make system prompts more focused
- Break complex agents into smaller ones

## Migration Guide

### From Commands to Agents

If you have existing slash commands that would work better as agents:

1. Identify commands that perform specialized tasks
2. Convert command prompt to system_prompt
3. Add appropriate tool restrictions
4. Update description for auto-invocation

### Sharing Agents

To share agents between projects:
1. Move agent YAML to `~/.claude/agents/`
2. Document agent purpose and usage
3. Version control for team sharing

## Future Considerations

As Claude Code evolves, subagents may support:
- Custom tool definitions
- Inter-agent communication
- Persistent context between invocations
- Conditional logic in YAML
- Agent templates and inheritance

## Related Documentation

- [Claude Code Overview](https://docs.anthropic.com/en/docs/claude-code/overview)
- [Custom Slash Commands](./custom-slash-commands-spec.md)
- [Claude Code Documentation](https://docs.anthropic.com/en/docs/claude-code)