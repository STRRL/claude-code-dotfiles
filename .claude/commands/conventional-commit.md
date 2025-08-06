---
description: Create a conventional commit following the Conventional Commits 1.0.0 specification
allowed-tools: bash
argument-hint: <type>[scope]: <description> [optional body] [optional footer]
---

# Create a Conventional Commit

I'll help you create a commit following the Conventional Commits 1.0.0 specification.

## Checking current changes

!git status --short
!git diff --cached --stat

## Analyzing changes

Based on the changes, I'll create a commit message following this structure:

```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

### Conventional Commit Types

- **feat**: A new feature (correlates with MINOR in SemVer)
- **fix**: A bug fix (correlates with PATCH in SemVer)
- **docs**: Documentation only changes
- **style**: Changes that don't affect code meaning (white-space, formatting, etc)
- **refactor**: Code change that neither fixes a bug nor adds a feature
- **perf**: Code change that improves performance
- **test**: Adding or correcting tests
- **build**: Changes to build system or dependencies
- **ci**: Changes to CI configuration files and scripts
- **chore**: Other changes that don't modify src or test files
- **revert**: Reverts a previous commit

### Breaking Changes

- Add ! after type/scope for breaking changes (e.g., feat!: or feat(api)!:)
- OR include BREAKING CHANGE: in the footer

## Creating the commit

Based on the changes and any specific requirements in "$ARGUMENTS", I'll:

1. Determine the appropriate commit type
2. Identify if a scope is needed
3. Write a clear, concise description
4. Add body details if the changes are complex
5. Include any necessary footers (BREAKING CHANGE, Refs, etc.)

Then execute the commit with:
!git add -A
!git commit -m "$(cat <<'EOF'
<generated commit message here>

🤖 Generated with [Claude Code](https://claude.ai/code)

Co-Authored-By: Claude <noreply@anthropic.com>
EOF
)"

The commit will follow all Conventional Commits 1.0.0 rules:

- Type prefix is required
- Description immediately follows colon and space
- Body (if included) starts one blank line after description
- Footer (if included) starts one blank line after body
- Breaking changes are clearly indicated
