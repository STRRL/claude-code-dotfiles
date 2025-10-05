---
description: Intelligently resolve git merge conflicts by analyzing changes from both branches and preserving features from all sides
allowed-tools: bash, read, write, edit, grep, glob
argument-hint: "[file-path] - optional specific file to resolve, or leave empty to resolve all conflicts"
---

# Resolve Merge Conflicts Intelligently

I'll help you resolve merge conflicts by analyzing changes from both branches and preserving features from all sides.

## Process:

1. **Analyze the conflict state**:
   - Check current merge/rebase status
   - List all conflicted files
   - Understand the branches involved

2. **For each conflicted file**:
   - Get the base version (common ancestor)
   - Get "ours" version (current branch)
   - Get "theirs" version (merging branch)
   - Analyze the differences to understand what each side is trying to accomplish

3. **Intelligent resolution**:
   - Identify the features/changes from each branch
   - Combine both sets of changes when possible
   - Preserve functionality from all branches
   - Ensure code remains syntactically correct

4. **Verification**:
   - Review the resolved files
   - Ensure no conflict markers remain
   - Test if possible (run builds/tests if available)

## Starting conflict resolution...

!git status --porcelain | grep "^UU\|^AA\|^DD"

### Checking merge/rebase status
!git status

### Getting branch information
!git rev-parse --abbrev-ref HEAD
!git log --oneline --graph -n 10 --all

### Analyzing conflicts in detail
!git diff --name-only --diff-filter=U

$ARGUMENTS

For each conflicted file, I will:
1. Examine the conflict markers and understand the changes
2. Get the three-way diff to see the common ancestor
3. Intelligently merge features from both sides
4. Remove conflict markers and create a clean resolution

After resolving, I'll stage the resolved files and provide a summary of the changes preserved from each branch.
